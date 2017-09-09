
---
title: "Common source options"
---

Unless the part plugin overrides this behaviour, a part can use these
`source` keys in its definition. They tell snapcraft where to pull source
code for that part, and how to unpack it if necessary.

  - `source`: url-or-path

    A URL or path to some source tree to build. It can be local
    (`./src/foo`) or remote (`https://foo.org/...`), and can refer to a
    directory tree or a tarball or a revision control repository
    (`git:...`).

  - `source-type`: git, bzr, hg, svn, tar, or zip

    In some cases the source string is not enough to identify the version
    control system or compression algorithm. The source-type key can tell
    snapcraft exactly how to treat that content.

  - `source-depth`: `<integer>`

    By default clones or branches with full history, specifying a depth
    will truncate the history to the specified number of commits.

  - `source-branch`: `<branch-name>`

    Snapcraft will checkout a specific branch from the source tree. This
    only works on multi-branch repositories from git and hg (mercurial).

  - `source-commit`: `<commit>`

    Snapcraft will checkout the specific commit from the source tree revision
    control system.

  - `source-tag`: `<tag>`

    Snapcraft will checkout the specific tag from the source tree revision
    control system.

  - `source-subdir`: path

    Snapcraft will checkout the repository or unpack the archive referred to
    by the `source` keyword into `parts/<part-name>/src/` but it will only
    copy the specified subdirectory into `parts/<part-name>/build/`

  - `source-checksum`: `<algorithm>/<digest>`

    Snapcraft will verify that the source downloaded matches the checksum
    provided, and halt the build with an error if not.

Note that plugins might well define their own semantics for the `source`
keywords, because they handle specific build systems, and many languages
have their own built-in packaging systems (think CPAN, PyPI, NPM). In those
cases you want to refer to the help text for the specific plugin.

    snapcraft help <plugin>
