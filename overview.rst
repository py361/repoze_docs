Overview of the Repoze Project
==============================

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

- The packages in the ``repoze.`` namespace require
  `setuptools <https://bitbucket.org/pypa/setuptools/>`_
  for installation.

- None of the ``repoze.*`` software has been tested under any version
  of Windows.  It has only been tested under UNIX variants (Linux
  and Mac OS X at the time of this writing).

Technology Dependencies
-----------------------

Many Repoze components depend on `Paste <http://www.pythonpaste.org>`_,
as well as `setuptools <https://bitbucket.org/pypa/setuptools/>`_
and the `WSGI specification <http://www.python.org/dev/peps/pep-0333/>`_.
Repoze reimplements and reuses some technologies originated within
`Zope <http://www.zope.org/>`_.

Licensing
---------

The original bits that make up Repoze are released under a
BSD-style `license <http://www.repoze.org/LICENSE.txt>`_.

Some non-original parts of Repoze are licensed under the `ZPL
<http://www.zope.org/Resources/ZPL>`_ (another BSD-style license).

Resources
---------

- Github organization: https://github.com/repoze/

- Mailing lists: http://lists.repoze.org/

- Blog: http://blog.repoze.org/

- IRC channel: irc://irc.freenode.net/#repoze

Legacy Resources
----------------

- Subversion repository (via ViewCVS): http://www.repoze.org/viewcvs/

- Subversion repository (via http): http://svn.repoze.org/

.. note::
   Currently-maintained packages have their repositories on Github under the
   `repoze organiztion <https://github.com/repoze/>`_.

- (Old) Repoze bug tracker: http://bugs.repoze.org/.

.. note::
   Currently-maintained packages have their issue trackers located with
   their repositories on Github.

- Repoze Python package repositories: http://dist.repoze.org/

.. note::
   The packages on ``dist.repoze.org`` were added to deal with some
   no-longer-relevant issues on the `PyPI <http://pypi.python.org/pypi>`_
   index.  They are no longer being updated.

Contributing
-------------

The preferred mechanism for contributons is via pull requests on the
project's Github repository.

To obtain write access to any oft, you will be required to sign a
`contributor's agreement <http://repoze.org/contributing.html>`_.
