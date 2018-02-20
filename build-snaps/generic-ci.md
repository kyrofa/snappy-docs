---
layout: base
title: Building, pushing, and releasing snaps from automated systems
---

Snapcraft not only provides the ability to build snaps, but also acts as the CLI front-end to the store. This includes pushing and releasing snaps to various channels, as well as opening and closing channels.

One benefit of this is that you can connect your continuous integration (CI) infrastructure to the store by building a snap and pushing/releasing it automatically whenever changes are made. This lets your users more quickly help you test changes.

How to do this differs depending on the CI system being used, and two common systems are supported via their own tutorials: [Travis] and [Circle CI]. But what if you're not using one of those CI systems? What if you're running your own?


## Step 1: Export a login capable of pushing/releasing your snap

Snaps are always registered to a specific account. Only that account, and any account that has been added as a collaborator on that snap, can administer the snap: upload new revisions, release into different channels, and so on. Since we need to conduct these operations from an automated system, we need to somehow provide a way for that system to authenticate in such a manner to gain these capabilities.

Hard-coding your credentials and scripting the run of `snapcraft login` is always an option, but it's rarely a good idea. Rather than exposing your password (and power!) in this way, Snapcraft lets you export a login that is limited in its capabilities to a file with the `snapcraft export-login` command. You can think of it as a login “token”.

For example, if our snap name was “my-snap”, we could export a login limited to _only_ pushing revisions of _only_ that snap to _only_ the edge channel by using the following command:

    $ snapcraft export-login --snaps my-snap --channels edge --acls package_upload credentials
    Enter your Ubuntu One e-mail address and password.
    If you do not have an Ubuntu One account, you can create one at https://dashboard.snapcraft.io/openid/login
    Email: email@example.com
    Password:

    Login successfully exported to 'credentials'. This file can now be used with
    'snapcraft login --with credentials' to log in to this account with no password
    and have these capabilities:
    
    snaps:       ['hello-kyrofa']
    channels:    ['edge']
    permissions: ['package_upload']
    
    This exported login is not encrypted. Do not commit it to version control!

As the output of the command mentions, anyone (including our CI system) can run `snapcraft login --with credentials` to login with those credentials and gain those capabilities.


## Step 2: Encrypt exported-login

So, we have a file that contains an exported login that can be used by anyone to become “us” with the capabilities we defined. As the output of that command mentioned, this file is _not_ encrypted, so committing it to version control would be a terrible mistake. Before we do that, we should encrypt it. This can easily be done by just using openssl:

    $ sudo apt install openssl
    $ openssl aes-256-cbc -e -in credentials -out credentials.enc
    enter aes-256-cbc encryption password:
    Verifying - enter aes-256-cbc encryption password:

Now our login is safely encrypted in the `credentials.enc` file with the password we selected. We should now remove the unencrypted one:

    $ rm credentials

Keep track of the password you used, you'll need it later. You could now commit this file to version control to be used in CI.


## Step 3: Make sure your CI is building snaps

Before a snap can be pushed/released, it needs to be built. Where that logic needs to go, and what it needs to look like, depends on which CI system being used. But each rendition typically follows the same two steps:

1. Install Snapcraft. Ideally this would be the snap:

        $ sudo snap install snapcraft
   
   However, it could also be the deb if your CI system is based on Xenial or later:
   
        $ sudo apt install snapcraft

2. Build the snap. In most cases, just run `snapcraft`. This will result in a .snap file being created.


## Step 4: Push/release the built snap

Now that the snap has been built, we can push and release it however we like (we’re using the `edge` channel here). Again, what exactly this looks like depends on the CI system being used, but here are the broad strokes:

1. Install Snapcraft. (This may not be necessary if this step is running on the same instance as Step 3, where we already installed Snapcraft.)

2. Install openssl, which we need to decrypt the credentials we encrypted and comitted in Step 2:

        $ sudo apt install openssl

3. Decrypt the credentials we encrypted and committed in Step 2. This involves making the password to decrypt the credentials available to the CI system. Many CI systems have support for adding environment variables via a web interface, allowing you to keep the password secret. Let’s use the variable `$SNAPCRAFT_CREDENTIALS_KEY`:

        $ openssl aes-256-cbc -d \
              -in credentials.enc \
              -out credentials \
              -k $SNAPCRAFT_CREDENTIALS_KEY

   Now the exported login is available in the `credentials` file.

4. Log in using the exported login:

        $ snapcraft login --with credentials

5. Push/release the snap:

        $ snapcraft push *.snap --release edge


## Conclusion

Building and pushing snaps from your CI is as simple as exporting a login to use, building the snap, logging in with the exported login, and pushing the built snap.

You can export a login for other purposes as well. For example, perhaps you have a CI system that runs a suite of tests and automatically promotes a snap that passes the test from `edge` to `beta`. You can export a login with capabilities that allow only this and no more.

By default the exported login expires after a year, at which time a new login must be exported. You can request that it expires sooner by using the `--expires` option. For example:

    $ snapcraft export-login --snaps my-snap --channels edge --acls package_upload --expires="2019-01-01T00:00:00" credentials
