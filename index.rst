The Repoze Project
==================

The Repoze project is a collection of technologies which bridges the
`WSGI <http://www.python.org/dev/peps/pep-0333/>`_ and
`Zope <http://www.zope.org>`_ worlds.  The project's goals:

- Make it possible for non-Zope Python developers to selectively
  use Zope features in a WSGI environment.

- Help Zope developers integrate their applications into a WSGI
  environment.

Problems Addressed
------------------

Some of the things that Zope does are useful enough to be
applicable to non-Zope-based WSGI applications: transaction
management, virtual hosting, form marshalling, declarative access
control, etc.  But currently it's not easy for Python web
developers who aren't fluent in Zope to make use of these
features, because they aren't always decomposed into individually
reusable pieces.

At the same time, WSGI deployment of Python applications has
become a defacto standard in the wider Python world.  At the time
of the project's inception, it was reasonably difficult to serve up
Zope (particularly Zope 2) via a WSGI server.

.. note::

   The current release line (2.13.x) of Zope2 has landed changes
   originally made here to support WSGI natively.

Solutions Provided
------------------

The Repoze project provides components which reimplement core Zope features
as WSGI middleware (repoze.vhm, repoze.retry, repoze.tm2), and WSGI
applications (repoze.zope2, repoze.grok).  The Repoze project also reuses
existing WSGI middleware (Paste) and servers where possible.

The bits of Repoze that reimplement core Zope features can be ignored or
used as necessary in non-Zope contexts.

Software Requirements and Limitations
-------------------------------------

- The packages in the 'repoze.' namespace require
  "setuptools":http://peak.telecommunity.com/DevCenter/setuptools
  for installation.

- None of the 'repoze.*' software has been tested under any version
  of Windows.  It has only been tested under UNIX variants (Linux
  and Mac OS X at the time of this writing).

Technology Dependencies
-----------------------

The Repoze components are heavily dependent on Ian Bicking's
`Paste <http://www.pythonpaste.org>`_, Phillip Eby's `setuptools
<http://peak.telecommunity.com/DevCenter/setuptools>`_
and of course the `WSGI specification
<http://www.python.org/dev/peps/pep-0333/>`_ also
written by Phillip Eby.  Repoze reimplements and reuses some
technologies originated within `Zope <http://www.zope.org/>`_.

Licensing
---------

The original bits that make up Repoze are released under a
BSD-style `license <http://www.repoze.org/LICENSE.txt>`_.

Some non-original parts of Repoze are licensed under the `ZPL
<http://www.zope.org/Resources/ZPL>`_ (another BSD-style license).

Resources
---------

- Mailing lists: http://lists.repoze.org/

- Blog: http://blog.repoze.org/

- Repoze bug tracker: http://bugs.repoze.org/

- Subversion repository (via ViewCVS): http://www.repoze.org/viewcvs/

- Subversion repository (via http): http://svn.repoze.org/

- Repoze Python package repositories: http://dist.repoze.org/

- IRC channel: irc://irc.freenode.net/#repoze

Contributing
-------------

Patches may be sent to the `repoze-dev maillist
<http://lists.repoze.org/mailman/listinfo/repoze-dev>`_ or
put into the `bug tracking system <http://bugs.repoze.org/>`_.
Patches sent to the list may be lost, so putting them in the bug
tracking system is better.

To obtain write access to the Repoze version control system, you
will be required to sign a `contributor's agreement
<http://repoze.org/contributing.html>`_.

Contents:

.. toctree::
   :maxdepth: 2

   history
   hacking

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
