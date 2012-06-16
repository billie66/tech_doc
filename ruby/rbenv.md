## Use rbenv to manage ruby versions

### Install the latest version of rbenv in ubuntu 10.10

1. Check out rbenv into `~/.rbenv`.

        $ cd
        $ git clone git://github.com/sstephenson/rbenv.git .rbenv

2. Add `~/.rbenv/bin` to your `$PATH` for access to the `rbenv`
   command-line utility.

        $ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc

3. Add rbenv init to your shell to enable shims and autocompletion.

        $ echo 'eval "$(rbenv init -)"' >> ~/.bashrc

4. Restart your shell so the path changes take effect. You can now
   begin using rbenv.

        $ exec $SHELL

5. Install `ruby-build`

        $ mkdir -p ~/.rbenv/plugins
        $ cd ~/.rbenv/plugins
        $ git clone git://github.com/sstephenson/ruby-build.git

The [ruby-build](https://github.com/sstephenson/ruby-build) project
provides an `rbenv install` command that simplifies the process of
installing new Ruby versions to:

        $ rbenv install 1.9.2-p290

6. Rebuild the shim binaries. You should do this any time you install
   a new Ruby binary (for example, when installing a new Ruby version,
   or when installing a gem that provides a binary).

        $ rbenv rehash

### Usage

Like `git`, the `rbenv` command delegates to subcommands based on its
first argument. The most common subcommands are:

#### global

Sets the global version of Ruby to be used in all shells by writing
the version name to the `~/.rbenv/version` file. This version can be
overridden by a per-project `.rbenv-version` file, or by setting the
`RBENV_VERSION` environment variable.

    $ rbenv global 1.9.2-p290

The special version name `system` tells rbenv to use the system Ruby
(detected by searching your `$PATH`).

When run without a version number, `rbenv global` reports the
currently configured global version.

#### rbenv local

Sets a local per-project Ruby version by writing the version name to
an `.rbenv-version` file in the current directory. This version
overrides the global, and can be overridden itself by setting the
`RBENV_VERSION` environment variable or with the `rbenv shell`
command.

    $ rbenv local rbx-1.2.4

When run without a version number, `rbenv local` reports the currently
configured local version. You can also unset the local version:

    $ rbenv local --unset

#### rbenv shell

Sets a shell-specific Ruby version by setting the `RBENV_VERSION`
environment variable in your shell. This version overrides both
project-specific versions and the global version.

    $ rbenv shell jruby-1.6.4

When run without a version number, `rbenv shell` reports the current
value of `RBENV_VERSION`. You can also unset the shell version:

    $ rbenv shell --unset

Note that you'll need rbenv's shell integration enabled (step 3 of
the installation instructions) in order to use this command. If you
prefer not to use shell integration, you may simply set the
`RBENV_VERSION` variable yourself:

    $ export RBENV_VERSION=jruby-1.6.4

#### rbenv versions

Lists all Ruby versions known to rbenv, and shows an asterisk next to
the currently active version.

    $ rbenv versions
      1.8.7-p352
      1.9.2-p290
    * 1.9.3-rc1 (set by /Users/sam/.rbenv/global)
      jruby-1.6.4
      rbx-1.2.4
      ree-1.8.7-2011.03

#### rbenv version

Displays the currently active Ruby version, along with information on
how it was set.

    $ rbenv version
    1.8.7-p352 (set by /Volumes/37signals/basecamp/.rbenv-version)

#### rbenv rehash

Installs shims for all Ruby binaries known to rbenv (i.e.,
`~/.rbenv/versions/*/bin/*`). Run this command after you install a new
version of Ruby, or install a gem that provides binaries.

    $ rbenv rehash

#### rbenv which

Displays the full path to the binary that rbenv will execute when you
run the given command.

    $ rbenv which irb
    /Users/sam/.rbenv/versions/1.9.2-p290/bin/irb

#### rbenv whence

Lists all Ruby versions with the given command installed.

    $ rbenv whence rackup
    1.9.3-rc1
    jruby-1.6.4
    ree-1.8.7-2011.03

