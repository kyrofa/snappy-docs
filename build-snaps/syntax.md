---
layout: base
title: The snapcraft syntax
---

The `snapcraft.yaml` file is the main entry point to create a snap through
Snapcraft.

The main building blocks of a snap are [parts](#parts). They are mainly used to declare pieces of code that will be pulled into your snap package. In addition to parts, there are required keys that define the metadata for the snap package.

What follows is a list of all the keys the `snapcraft.yaml` file can contain.

* Keys on the same level can be declared in any order, but are grouped and ordered in this document to clarify their purpose.
* Required keys are in **bold**.

## Top-level metadata

By convention at the top of the file, the following keys are consumed by the store to present your package to users and inform snapd about your snap.

<ul>
  <li style="margin-bottom: 0;"><a href="#name" style="font-weight: bold;"><code>name</code></a></li>
  <li style="margin-bottom: 0;font-weight: bold;"><a href="#version" style="font-weight: bold;"><code>version</code></a></li>
  <li style="margin-bottom: 0;font-weight: bold;"><a href="#summary" style="font-weight: bold;"><code>summary</code></a></li>
  <li style="margin-bottom: 0;font-weight: bold;"><a href="#description" style="font-weight: bold;"><code>description</code></a></li>
  <li style="margin-bottom: 0;"><a href="#type"><code>type</code></a></li>
  <li style="margin-bottom: 0;"><a href="#confinement"><code>confinement</code></a></li>
  <li style="margin-bottom: 0;"><a href="#icon"><code>icon</code></a></li>
  <li style="margin-bottom: 0;"><a href="#grade"><code>grade</code></a></li>
  <li style="margin-bottom: 0;"><a href="#assumes"><code>assumes</code></a></li>
  <li style="margin-bottom: 0;"><a href="#epoch"><code>epoch</code></a></li>
  <li style="margin-bottom: 0;"><a href="#architectures"><code>architectures</code></a></li>
</ul>

## Top-level YAML subsections

### Apps and daemons

The "`apps`" YAML subsection exposes apps and daemons from your package to the host system, declares their permissions and run conditions.

<ul>
  <li style="margin-bottom: 0;"><a href="#apps"><code>apps</code></a>
    <ul>
      <li style="margin-bottom: 0;"><a href="#app-name">&lt;app name&gt;</a> <small><em><a href="/build-snaps/metadata">(examples)</a></em></small>
        <ul>
          <li style="margin-bottom: 0;"><a href="#command"><code>command</code></a></li>
          <li style="margin-bottom: 0;"><a href="#plugs"><code>plugs</code></a></li>
          <li style="margin-bottom: 0;"><a href="#desktop"><code>desktop</code></a></li>
          <li style="margin-bottom: 0;"><a href="#daemon"><code>daemon</code></a></li>
          <li style="margin-bottom: 0;"><a href="#stop-command"><code>stop-command</code></a></li>
          <li style="margin-bottom: 0;"><a href="#stop-timeout"><code>stop-timeout</code></a></li>
          <li style="margin-bottom: 0;"><a href="#post-stop-command"><code>post-stop-command</code></a></li>
          <li style="margin-bottom: 0;"><a href="#restart-condition"><code>restart-condition</code></a></li>
          <li style="margin-bottom: 0;"><a href="#sockets"><code>sockets</code></a>
            <ul>
              <li style="margin-bottom: 0;"><a href="#listen-stream"><code>listen-stream</code></a></li>
              <li style="margin-bottom: 0;"><a href="#socket-mode"><code>socket-mode</code></a></li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </li>
</ul>

### Parts declarations

The "`parts`" YAML subsection declares individual pieces of code to be imported -- and possibly built or modified -- in your snap at packaging time.

<ul>
  <li style="margin-bottom: 0;"><a href="#parts" style="font-weight: bold;"><code>parts</code></a>
    <ul>
      <li style="margin-bottom: 0;"><a href="#part-name" style="font-weight: bold;">&lt;part name&gt;</a> <small><em><a href="/build-snaps/parts">(examples)</a></em></small>
        <ul>
          <li style="margin-bottom: 0;"><a href="#plugin" style="font-weight: bold;"><code>plugin</code></a></li>
          <li style="margin-bottom: 0;"><a href="#plugin-options">[plugin options]</a></li>
          <li style="margin-bottom: 0;"><a href="#source"><code>source</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-type"><code>source-type</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-checksum"><code>source-checksum</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-depth"><code>source-depth</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-branch"><code>source-branch</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-commit"><code>source-commit</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-tag"><code>source-tag</code></a></li>
          <li style="margin-bottom: 0;"><a href="#source-subdir"><code>source-subdir</code></a></li>
          <li style="margin-bottom: 0;"><a href="#after"><code>after</code></a></li>
          <li style="margin-bottom: 0;"><a href="#build-packages"><code>build-packages</code></a></li>
          <li style="margin-bottom: 0;"><a href="#stage-packages"><code>stage-packages</code></a></li>
          <li style="margin-bottom: 0;"><a href="#organize"><code>organize</code></a></li>
          <li style="margin-bottom: 0;"><a href="#filesets"><code>filesets</code></a></li>
          <li style="margin-bottom: 0;"><a href="#stage"><code>stage</code></a></li>
          <li style="margin-bottom: 0;"><a href="#prime"><code>prime</code></a></li>
          <li style="margin-bottom: 0;"><a href="#prepare"><code>prepare</code></a></li>
          <li style="margin-bottom: 0;"><a href="#build"><code>build</code></a></li>
          <li style="margin-bottom: 0;"><a href="#install"><code>install</code></a></li>
          <li style="margin-bottom: 0;"><a href="#build-attributes"><code>build-attributes</code></a></li>
        </ul>
      </li>
    </ul>
  </li>
</ul>

## Keys description

### name

The name of the resulting snap.

* Type: string
* Required: yes
* Example:

      name: hello-world



### version

The version of the resulting snap.

* Type: string
* Required: yes
* Example:

      version: 1.2.3+git

### summary

A 78 characters max sentence to present your snap.

* Type: string
* Required: yes
* Example:

      summary: hello-world prints the user name on the command line.

### description

The description for the snap, this can and is expected to be a longer
presentation of the snap.

* Type: string
* Required: yes
* Examples:

      description: A longer description of the hello-world snap.

      description: |
       The description can also be
       multi-line when using a pipe.

### type

The type of snap. Valid values are `app`, `core`, `gadget` and `kernel`. Defaults to `app`.

* Type: string
* Example:

      type: app

### confinement

The type of confinement supported by the snap. Can be "strict" , "devmode" or "classic". See [Confinement](/reference/confinement) for details.

* Type: string
* Example:

      confinement: strict

### icon

The path to the icon that will be used for the snap.

* Type: string
* Example:

      icon: meta/gui/icon.png

### grade

This defines the quality grade of the snap. It can be either "devel" (i.e.
a development version of the snap, so not to be published to the "stable" or
"candidate" channels) or "stable" (i.e. a stable release or release
candidate, which can be released to all channels).

* Type: string
* Example:

      grade: stable

### assumes

A list of features that must be supported by the core in order for this snap
to install.

* Type: list

### epoch

The epoch to which this revision of the snap belongs. This is used to specify
upgrade paths. For example, `0` is epoch 0; `1*` is the upgrade path from 0 to
1; `1` is epoch 1, etc.

* Type: string

### architectures

The architectures on which this snap runs. This defaults to the host architecture unless `--target-arch` is specified, in which case it defaults to the target architecture. One may specify multiple architectures if that's supported (for example, a 32-bit snap might run on both i386 and amd64 using `[amd64, i386]`, or a snap that is shell-only might run on all architectures, using `all`).

* Type: list
* Example:

      architectures: [amd64, i386]

As in the example, one may simply specify architectures in a flat list, in which case any version of this snap built on any architecture will end up stating that it runs on that set of architectures.

If the architectures on which this snap runs needs to depend on the build environment, this keyword supports Snapcraft's [advanced grammar](#advanced-grammar). For example, say the snap only runs on i386 and amd64 if it's built on i386, but to otherwise use the host architecture, use:

    - on i386: [amd64, i386]

Building on this, perhaps this snap could also run on both armhf and arm64 if built on armhf:

    - on i386: [amd64, i386]
    - on armhf: [armhf, arm64]

Perhaps this snap doesn't build on any architecture other than armhf. You can indicate that with the following:

    - on armhf: [armhf]
    - else fail

In this case, Snapcraft will error out whenever one tries to build this snap on anything other than armhf.


### apps

A map of keys for app names. These are either daemons or command line
accessible binaries.

* Type: YAML subsection
* [Examples](/build-snaps/metadata#declaring-app-commands)

### &lt;app name&gt;

The name of an app contained in the snap, that will be exposed to the host system.

If the app name matches the snap name, the app will be executed when the name of the snap is called.
Otherwise, the executable will have the snap name and a dot prefixed to the app name.

* Type: string
* Example:

      name: foo
      apps:
        foo:
          ...
        bar:
          ...

  This 'foo' snap will expose two executables to the host, `foo` and `foo.bar`.

### command

Specifies the internal command to expose. If the app is a `daemon` this
command is used to start the service.

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo

### plugs

The list of interfaces the app should have access to. See [Interfaces](/core/interfaces) for details on plugs and the [list of available interfaces](/reference/interfaces).

* Type: list
* Example:

      apps:
        foo:
          command: usr/bin/foo
          plugs: [home, network, x11]

### desktop

The path to the desktop file for this app.

* Type: string
* [Examples](/build-snaps/metadata#fixed-assets)


### daemon

When present, this key integrates the executable as a system service.

Valid values are `forking`, `oneshot`, `notify` and `simple`.

If set to `simple`, it is expected that the command configured is the main
process.

If set to `oneshot`, it is expected that the command configured
will exit once it's done (won't be a long-lasting process).

If set to `forking`, it is expected that the configured command will call
fork() as part of its start-up. The parent process is expected to exit
when start-up is complete and all communication channels are set up. The child continues to run as the main daemon process. This is the
behavior of traditional UNIX daemons.

If set to `notify`, it is expected that the command configured will send a signal to systemd to indicate that it's running.

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo
          daemon: simple

### stop-command

Requires `daemon` to be declared and represents the command to run to
stop the service.

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo
          daemon: simple
          stop-command: usr/bin/end-foo

### stop-timeout

Requires `daemon` to be declared.

It is the length of time with unit (`10ns`, `10us`, `10ms`, `10s`, `10m`)
that the system will wait for the service to stop before terminating it
via `SIGTERM` (and `SIGKILL` if that doesn't work).

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo
          daemon: simple
          stop-command: usr/bin/end-foo
          stop-timeout: 5s

### post-stop-command

Optional command to run after the daemon stops.

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo
          daemon: simple
          stop-command: usr/bin/end-foo
          post-stop-command: usr/bin/cleanup-foo

### restart-condition

Condition to restart the daemon under. Valid values are `on-failure`, `on-success`, `on-abnormal`, `on-abort`, `always` and `never`. Defaults to `on-failure`.

See the [systemd.service manual](https://www.freedesktop.org/software/systemd/man/systemd.service.html#Restart=) on `Restart` for details.

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo
          daemon: simple
          restart-condition: always

### sockets

If the daemon is socket activated, this section contains a map declaring sockets that will activate the service.
If this section is declared, the application needs to declare the `network-bind` plug.

* Type: YAML subsection

### listen-stream

The socket abstract name or socket path. Valid formats are: `<port>`, `[::]:<port>`, `[::1]:<port>` and `127.0.0.1:<port>` for TCP sockets, `$SNAP_DATA/<path>`, `$SNAP_COMMON/<path>` and `@snap.<snap name>.<suffix>` for Unix sockets.

* Type: string
* Example:

      apps:
        foo:
          command: usr/bin/foo
          plugs: [home, network-bind]
          daemon: simple
          sockets:
            listen-stream: 8080

### socket-mode

For Unix sockets, the file permission (e.g. `0644`).

* Type: integer
* Example:

      apps:
        foo:
          command: usr/bin/foo
          plugs: [home, network-bind]
          daemon: simple
          sockets:
            listen-stream: $SNAP_DATA/foo_data
            socket-mode: 0644

### parts

A map of part names to their own part configuration.

Each part is independent from the others but you can control in which order they are processed using the [`after`](#after) key.

* Type: YAML subsection
* Required: yes
* Example:

      parts:
        foo:
          ...
        bar:
          ...

* [Learn more](/build-snaps/parts)

### &lt;part name&gt;

A name for an individual part to start a part declaration, it's always a subsection of `parts`.

* Type: YAML subsection
* Required: yes

### plugin

Declares the plugin name that will manage this part. Snapcraft will pass
to it all the other user-specified part options.

* Type: string
* Required: yes
* Example:

      parts:
        foo:
          plugin: python

* [Learn more](/build-snaps/plugins)

### [plugin options]

Each plugin comes with a set of specific keys. For example, the `python` plugin has a `python-version` key, allowing you to choose Python `2` or `3`.

See the [plugins reference](/reference/plugins) or `snapcraft help <plugin name>` for plugin-specific documentation and usage examples.

### source

A URL or path to some source tree to build. It can be local
('./src/foo') or remote ('https://foo.org/...'), and can refer to a
directory tree or a tarball or a revision control repository
('git:...').

* Type: string
* Examples:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
        bar:
          plugin: dump
          source: bar-0.1.tar

As in the example, one may simply specify a string, in which case that source
will be used regardless of the build environment.

If the source needs to be dependent on the build environment, this
keywords supports Snapcraft's [advanced grammar](#advanced-grammar). For
example, you can require a specific source to be used on amd64, and another for
i386:

    - on amd64: https://my/amd64/source
    - on i386: https://my/i386/source

If your project requires a source that is only available for amd64, you can fail
if you're not building on amd64:

    - on amd64: https://my/amd64/source
    - else fail

### source-type

In some cases the source string is not enough to identify the version
control system or compression algorithm. The `source-type` key can tell
Snapcraft exactly how to treat that content.

* Supported values: `git`, `bzr`, `hg`, `svn`, `tar`, `deb`, `rpm`, or `zip`
* Example:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
          source-type: git

### source-checksum

Snapcraft will use the digest specified to verify the integrity of the
source.

The source-type needs to be a file (tar, zip, deb or rpm) and
the algorithm either `md5`, `sha1`, `sha224`, `sha256`, `sha384`, `sha512`, `sha3_256`,
`sha3_384` or `sha3_512`.

* Format: `<algorithm>`/`<digest>`
* Example:

      parts:
        foo:
          plugin: python
          source: ./assets/foo-1.2.tar
          source-checksum: sha256/3f8cc3fe72b575bdf428e1ef862999fc4a4126396d564686be23508c149eeb6b

### source-depth

By default clones or branches with full history, specifying a depth
will truncate the history to the specified number of commits.

* Type: integer
* Example:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
          source-depth: 1

### source-branch

Snapcraft will checkout a specific branch from the source tree. This
only works on multi-branch repositories from git and hg (mercurial).

* Type: string
* Example:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
          source-branch: switch-to-bar

### source-commit

Snapcraft will checkout the specific commit from the source tree revision
control system.

* Format: commit ID
* Example:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
          source-commit: 9ce63a95f610d52f85e330192436aef6f73b8c06

### source-tag

Snapcraft will checkout the specific tag from the source tree revision
control system.

* Format: tag
* Example:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
          source-tag: v2

### source-subdir

When building, Snapcraft will set the working directory to be this
subdirectory within the source.

* Format: path
* Example:

      parts:
        foo:
          plugin: python
          source: https://github.com/bar/foo.git
          source-subdir: src/

### after

Snapcraft will make sure that it builds all of the listed parts in `after`, before
it tries to build this part. Essentially these listed dependencies for
this part, useful when the part needs a library or tool built by another
part.

If such a dependency part is not defined in this `snapcraft.yaml`, it must
be defined in the shared [parts library](https://wiki.ubuntu.com/Snappy/Parts),
where snapcraft will retrieve the definition of the part.

* Type: list
* Example:

      parts:
        foo:
          plugin: python
          after: [bar]
        bar:
          plugin: dump
          after: [desktop/gtk3, ffmpeg]

### build-packages

A list of packages to install on the build host before building
the part.

The files from these packages typically will not go into the
final snap unless they contain libraries that are direct dependencies of
binaries within the snap (in which case they'll be discovered via `ldd`),
or they are explicitly described in [`stage-packages`](#stage-packages).

* Type: list
* Example:

      parts:
        foo:
          plugin: python
          build-packages:
          - libmpeg2-4-dev
          - libogg-dev
          - libvorbis-dev

As in the example, one may simply specify packages in a flat list, in which case
the packages will installed on the host regardless of the build environment.

If the set of packages needs to be dependent on the build environment, this
keywords supports Snapcraft's [advanced grammar](#advanced-grammar). For
example, say you only wanted to install `foo` if building on amd64 (and not
install `foo` otherwise):

    - on amd64: [foo]

Building on that, say you wanted to install `bar` if building on an arch other
than amd64:

    - on amd64: [foo]
    - else: [bar]

You can nest these for more complex behaviors:

    - on amd64: [foo]
    - else:
      - on i386: [bar]
      - on armhf: [baz]

If your project requires a package that is only available on amd64, you can
fail if you're not building on amd64:

    - on amd64: [foo]
    - else fail

As another example of using the grammar, say you wanted to install `foo`, but it
wasn't available for all architectures. Assuming your project builds without it,
you can make it an optional build package:

    - try: [foo]

You can also add alternatives:

    - try: [foo]
    - else: [bar]

Again, you can nest these for more complex behaviors:

    - on amd64: [foo]
    - else:
      - try: [bar]

Your packages can also depend on the target architecture:

    - to armhf: [foo]

Host and target architecture can also be written as a compound statement in
one line for a specific combination:

    - on amd64 to armhf: [foo]

And all the same alternations work with it naturally:

    - on amd64: [foo]
    - to armhf: [bar]
    - else:
      - try: [baz]


### stage-packages

A list of packages to be downloaded and unpacked to join the part before it's
built. Note that these packages are not installed on the host. Like the rest of
the part, all files from these packages will make it into the final snap unless
filtered out via the [`prime`](#prime) key.

* Type: list
* Example:

      parts:
        foo:
          plugin: python
          stage-packages:
            - libtheora0
            - libvorbis0a
            - libvorbisfile3

As in the example, one may simply specify packages in a flat list, in which case
the packages will be fetched and unpacked regardless of build environment.

If the set of packages needs to be dependent on the build environment, this
keywords supports Snapcraft's [advanced grammar](#advanced-grammar). For
example, say you only wanted to stage `foo` if building on amd64 (and not stage
`foo` otherwise):

    - on amd64: [foo]

Building on that, say you wanted to stage `bar` if building on an arch
other than amd64:

    - on amd64: [foo]
    - else: [bar]

You can nest these for more complex behaviors:

    - on amd64: [foo]
    - else:
      - on i386: [bar]
      - on armhf: [baz]

If your project requires a package that is only available on amd64, you can
fail if you're not building on amd64:

    - on amd64: [foo]
    - else fail

If on the other hand you want a package only when building for a certain
target architecture:

    - to armhf: [spam]

Or even more specifically from amd64 to armhf:

    - on amd64 to armhf: [eggs]

This can also be written on separate lines:

    - on amd64:
      - to armhf:
        - eggs

The body of the '`try`' clause is taken into account only when all packages
contained within it are valid. If not, if it's immediately followed by
'`else`' clauses they are tried in order, and one of them must be satisfied.
A '`try`' clause with no '`else`' clause is considered satisfied even if it
contains invalid packages.

For example, say you wanted to stage `foo`, but it wasn't available for all
architectures. Assuming your project builds without it, you can make it an
optional stage package:

As another example of using the grammar, say you wanted to stage `foo`, but it
wasn't available for all architectures. Assuming your project builds without it,
you can make it an optional stage package:

    - try: [foo]

You can also add alternatives:

    - try: [foo]
    - else: [bar]

Again, you can nest these for more complex behaviors:

    - on amd64: [foo]
    - else:
      - try: [bar]

### organize

Snapcraft will rename files according to this YAML subsection. The
content of the `organize` section consists of old path keys, and their
new values after the renaming.

This can be used to avoid conflicts between parts that use the same
name, or to map content from different parts into a common conventional
file structure.

* Format: YAML subsection
* Example:

      parts:
        foo:
          plugin: python
          organize:
            usr/oldfilename: usr/newfilename
            usr/local/share/: usr/share/

The key is the internal part filename, the value is the exposed filename
that will be used during the staging process. You can rename whole
subtrees of the part, or just specific files.

Note that the path is relative (even though it is "`usr/local`") because
it refers to content underneath `parts/<part-name>/install` which is going
to be mapped into the `stage` and `prime` areas.

### filesets

When we map files into the `stage` and `prime` areas on the way to putting
them into the snap, it is convenient to be able to refer to groups of
files as well as individual files.  Snapcraft lets you name a fileset
and then use it later for inclusion or exclusion of those files from the
resulting snap.

For example, consider man pages of header files: you might want them
in, or you might want to leave them out, but you definitely don't want
to repeatedly have to list all of them either way.

This section is thus a YAML map of fileset names (the keys) to a list of
filenames. The list is built up by adding individual files or whole
subdirectory paths (and all the files under that path) and wildcard
globs, and then pruning from those paths.

The wildcard `*` globs all files in that path. Exclusions are denoted by
an initial `-`.

As seen in the example you could add `usr/local/*` then remove `usr/local/man/*`:

* Format: map of lists
* Example:

      parts:
        foo:
          plugin: python
          filesets:
            allbutman: [ usr/local/*, -usr/local/man/* ]
            manpages: [ usr/local/man ]

File names are relative to the part install directory in
`parts/<part-name>/install`. If you have used [`organize`](#organize) to rename files
then the filesets will be built up from the names after organization.

### stage

A list of files from a part install directory to copy into `stage/`.
Rules applying to the list here are the same as those of filesets.
Referencing of fileset keys is done with a `$` prefixing the fileset key,
which will expand with the value of such key.

* Format: list of file paths and filesets
* Example:

      parts:
        foo:
          plugin: python
          stage:
            - usr/lib/*    # Everything under parts/<part-name>/install/usr/lib
            - -usr/lib/libtest.so    # Excludng libtest.so
            - $manpages    # Including the 'manpages' fileset

### prime

A list of files from a part install directory to copy into `prime/`.
This key takes exactly the same form as the [`stage`](#stage) key  but the
files identified here will go into the ultimate snap (because the
`prime/` directory reflects the file structure of the snap with no
extraneous content).

* Format: list of files and filesets
* Example:

      parts:
        foo:
          plugin: python
          prime:
            - dist/linux/*
            - src/foo.desktop
            - $manpages

### prepare

If present, the shell script defined here is run before the `build` step
of the plugin starts. The working directory is the base build
directory for the given part. The defined script is run with `/bin/sh`.

* Type: shell script
* Example:

      parts:
        foo:
          plugin: make
          prepare: |
            cd scripts
            ./bootstrap.sh

* [Learn more](scriptlets)

### build

If present, the shell script defined here is run instead of the `build`
step of the plugin. The working directory is the base build directory
for the given part. The defined script is run with `/bin/sh`.

* Type: shell script
* Example:

      parts:
        foo:
          plugin: make
          build: |
           make project
           make test
           make special-install

* [Learn more](scriptlets)

### install

If present, the shell script defined here is run after the `build` step
of the plugin has finished. The working directory is the base build
directory for the given part. The defined script is run with `/bin/sh`.

* Type: shell script
* Example:

      parts:
        foo:
          plugin: make
          install: |
           sed -i 's|/usr/bin|$SNAP/usr/bin|g' my-bin-artifact.sh
           mv my-bin-artifact.sh $SNAPCRAFT_PART_INSTALL/bin/my-bin-build.sh

* [Learn more](scriptlets)

### build-attributes

A list of special attributes that affect the build of this specific part:

`no-system-libraries`: do not automatically copy required libraries from the system to satisfy
  the dependencies of this part. This might be useful if one knows these
  dependencies will be satisfied in other manner, e.g. via content
  sharing from other snaps.

`no-install`: do not run the install target provided by the plugin's build system.

`debug`: plugins that support the concept of build types build in Release mode
  by default. Setting the 'debug' attribute requests that they instead
  build in Debug mode.

* Type: list
* Example:

      parts:
        foo:
          plugin: kbuild
          build-attributes: [debug, no-system-libraries]

## Advanced grammar

Several fields in the YAML support being dependent on the architecture or
the operating system. They do so by supporting Snapcraft's advanced grammar.
This grammar is made up of YAML lists.


### Formal definition

The grammar is made up of three nestable statements: '`on`', '`to`' and '`try`'.


#### The `on` statement

    - on <selector>[,<selector>...]:
        <grammar>|<primitive>
    - else[ fail]:
        <grammar>|<primitive>

`<primitive>` may be either a list or a scalar. The type to use depends on the
keyword.

The body of the '`on`' clause is taken into account if every (AND, not OR)
selector is true for the build environment. Currently the only
selectors supported are host architectures (e.g. `amd64`).

If the '`on`' clause doesn't match and is immediately followed by an '`else`'
clause, the '`else`' clause must be satisfied. An '`on`' clause without an
'`else`' clause is considered satisfied even if no selector matched. The
'`else fail`' form allows erroring out if an '`on`' clause was not matched.


#### The `to` statement

    - [on <selector>[,<selector>...] ]to <selector>[,<selector>...]:
        <grammar>|<primitive>
    - else[ fail]:
        <grammar>|<primitive>

`<primitive>` may be either a list or a scalar. The type to use depends on the
keyword.

The body of the '`to`' clause is taken into account if every (AND, not OR)
selector is true for the target environment. Currently the only
selectors supported are target architectures (e.g. `armhf`).

If the '`to`' clause doesn't match and is immediately followed by an '`else`'
clause, the '`else`' clause must be satisfied. A '`to`' clause without an
'`else`' clause is considered satisfied even if no selector matched. The
'`else fail`' form allows erroring out if a '`to`' clause was not matched.

Optionally an '`on`' statement can precede a `'to'` in the same line to form
a compound statement. Used this way, the selectors of both statements have to
be true. That is to say, both the build environment and the target have to
be true for the body of the clause to be taken into account.


#### The `try` statement

    - try:
        <grammar>|<primitive>
    - else:
        <grammar>|<primitive>

`<primitive>` may be either a list or a scalar. The type to use depends on the
keyword.

The body of the '`try`' clause is taken into account only when all primitives
contained within it are valid (primitive validity is determined on a
keyword-specific basis). If they are not all valid, and are immediately
followed by '`else`' clauses, those are tried in order, and one of them must be
satisfied. A '`try`' clause with no '`else`' clause is considered satisfied even
if it contains invalid primitives.
