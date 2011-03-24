****************************************************
multipy -- Install any Python or all Pythons locally
****************************************************

*multipy* is a shell utility that helps you install and manage
multiple local Python installations:

* Downloads source tarballs for the newest version of any Python X.Y,
* compiles the source, and
* installs everything under a single directory hierarchy.

By default, the install location is ``~/multipy``.

*multipy* is a single shell script. It requires a POSIX compliant
shell, ``wget``, ``tar`` and ``gzip`` to download and extract source
tarballs, and compiler, development headers and libraries to compile
Python. No existing Python installation is required.


Usage
=====

Install Python 2.7 and 3.2::

    $ multipy install 2.7 3.2

Install all supported Python versions (2.4 and up)::

    $ multipy install all

List installed Python versions::

    $ multipy list

Remove Python 2.7::

    $ multipy remove 2.7

Custom installation directory::

    $ multipy -b /path/to/pythons install 3.2

Show help::

    $ multipy -h


Files
=====

In the following, the top directory of the multipy tree is denoted by
``$basedir``. The default is ``basedir=$HOME/multipy``.

When Python X.Y is being installed, the source tarball of the newest
release Python X.Y.Z is first downloaded to ``$basedir/sources``. The
source is then extracted to a temporary directory under
``$basedir/tmp`` and compiled. Finally, the result is installed to
``$basedir/pythons/X.Y/``.


Copyright
=========

Copyright (C) 2011 Petri Lehtinen. Licensed under the MIT license.
