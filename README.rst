***************************************************
multipy -- Install multiple Python versions locally
***************************************************

*multipy* is a shell utility that helps you install and manage
multiple local Python installations. It downloads source tarballs for
the newest version of any Python X.Y, compiles the source, and
installs everything under a single directory hierarchy. By default,
the install location is ``~/multipy``.

distribute_ is also installed along with each Python version, as well
as an activate script in the spirit of virtualenv_, for easier shell
integration.

*multipy* is a single shell script. It requires a POSIX compliant
shell, ``wget``, ``tar`` and ``gzip`` to download and extract source
tarballs, and a compiler, development headers and libraries to compile
Python. No existing Python installation is required. *multipy* should
work on any Unix-like system that Python can be compiled on.

Python versions 2.4 and up can be installed (including all 3.x
releases).


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

Use a custom installation directory::

    $ multipy -b /path/to/somewhere install 3.2

Tweak ``PATH`` to "activate" the local Python 2.5::

    $ . $(multipy activate 2.5)

After this, e.g. ``python`` and ``easy_install`` can be used without
an absolute path. To leave this mode, use ``deactivate``.

Show the directory where Python 3.1 has been installed::

    $ multipy path 3.1
    /home/you/multipy/pythons/3.1

Show help::

    $ multipy -h

Here's a list of supported command line options::

    -b BASEDIR   The base directory [default: ~/multipy]
    -k           Keep temporary files and logs after installation
    -n           Don't install distribute
    -j N         Compile with N jobs in parallel

Upon startup, multipy tries to source ``~/.multipyrc`` and
``~/.config/multipyrc``. The following variables can be assigned in
these files::

    Variable:         Command-line option:

    basedir=BASEDIR   -b BASEDIR
    keep_tmp=1        -k
    no_distribute=1   -n
    jobs=2            -j 2


Under the hood
==============

By default, the top directory of the multipy is
``basedir=$HOME/multipy``. This can be changed with the ``-b`` option
or in the config files discussed in the last section.

When Python X.Y is installed, the following things happen:

* The source tarball of the newest release Python X.Y.Z is first
  downloaded to ``$basedir/sources``. For example, when writing this,
  the newest version of Python 2.7 is 2.7.1. Installing older point
  releases is not supported.

* The source is then extracted to a temporary directory under
  ``$basedir/tmp`` and compiled. The result is installed to
  ``$basedir/pythons/X.Y/``. This is the standard ``configure``,
  ``make``, ``make install`` procedure.

* The newest release of distribute_ is downloaded to
  ``$basedir/sources`` (if not already there). It's extracted to a
  directory under ``$basedir/tmp`` and ``python setup.py install`` is
  run with the Python version that was installed in the previous step.
  (This step can be skipped using the ``-n`` option.)

* An ``activate`` script is installed to the ``bin/`` directory of the
  Python installation.

* Finally, ``$basedir/tmp`` is removed (this can be disabled with the
  ``-k`` option).

If anything goes wrong, ``$basedir/tmp`` is left in place, and logs of
each step are available as ``$basedir/tmp/*.log``.

The source tarballs are left in the ``$basedir/sources`` directory for
future use, but you can safely remove them if you want to free up some
disk space.


Copyright
=========

Copyright (C) 2011-2013 Petri Lehtinen. Licensed under the MIT license.


.. _distribute: http://pypi.python.org/pypi/distribute
.. _virtualenv: http://pypi.python.org/pypi/virtualenv
