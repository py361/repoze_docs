Current Repoze Components
=========================

The Repoze project consists of of the following software components under
active maintenance.

WSGI Middleware
---------------

- ``repoze.tm2``

  WSGI middleware that implements a transaction policy.  It uses the
  `transaction <https://pypi.python.org/pypi/transaction>`_ module 
  to commit or abort (if there is an exception) a transaction
  after each WSGI request.

  Applications may register callbacks with ``repoze.tm2`` (e.g.,
  to close a connection, mainly).  This behavior used to be
  hardcoded in Zope's publisher.  ``repoze.tm2`` is useful in any
  web application that requires transactions.

  Github:  https://github.com/repoze/repoze.tm2

- ``repoze.retry``

  WSGI middleware that retries a WSGI request some configurable number
  of times if any child application raises a "retriable" exceptin
  (e.g., ZODB's ``ConflictError``, or the equivalent PostgreSql
  "repeatable read" error).  This behavior used to be hardcoded in
  Zope's publisher.

  Github:  https://github.com/repoze/repoze.retry

- ``repoze.profile``

  WSGI middleware component which aggregates Python profiling data across
  all requests to a WSGI application.  It provides an optional HTML UI for
  viewing profiling data.

  Github: https://github.com/repoze/repoze.profile

- ``repoze.who``

  Identification and authentication framework for arbitrary WSGI applications.
  Can be used as WSGI middleware, or as a library within application code.
  It is inspired by Zope 2's Pluggable Authentication Service
  (PAS) but it is not dependent on Zope in any way.

  Github: https://github.com/repoze/repoze.who

- ``repoze.vhm``

  WSGI middleware which normalizes specially-mangled URLs (or individual
  header values) into ordinary paths, with the additional information
  stored in the environment for use in generating dynamic URLs.  It is an
  analogue / replacement for the Zope2 Virtual Host Monster.

  Github: https://github.com/repoze/repoze.vhm

- ``repoze.errorlog``

  WSGI middleware filter which intercepts exceptions and writes them to
  a Python ``logging`` module channel (or the ``wsgi.errors`` filehandle,
  if no channel is configured).  It also provides an optional HTML UI 
  for browsing limited exception history.

  Github: https://github.com/repoze/repoze.errorlog

- ``repoze.zodbconn``

  Library which manages ZODB databases and WSGI middleware which
  makes a ZODB connection available to downstream applications.

  Github: https://github.com/repoze/repoze.zodbconn

- ``repoze.debug``

  Middleware which can help with in-production forensic debugging.

  Github: https://github.com/repoze/repoze.debug

Libraries
---------

- ``repoze.evolution``

  Allows a developer to keep persistent data structures (data in a
  relational database, on the filesystem, in a persistent object store,
  etc.) in sync with changes made to software.  It provides a framework
  for developers to create and use a package full of monotonically named
  "evolve" scripts which modify the data; each script brings the data up
  to some standard of a software version.

  Github: https://github.com/repoze/repoze.evolution

- ``repoze.catalog``

  An indexing and searching system based on ``zope.index``.

  Github: https://github.com/repoze/repoze.catalog

- ``repoze.session``

  A sessioning system (server side state for web applications)
  based on ZODB.

  Github: https://github.com/repoze/repoze.session

- ``repoze.formapi``

  A form library which integrates with HTML forms instead of abstracting
  them away.  It provides a small framework to take you through the entire
  process of rendering a form, provide default values, validate
  and execute form actions.

  Github: https://github.com/repoze/repoze.formapi

- ``repoze.bitblt``

  WSGI middleware component which
  automatically scales images according to the ``width`` and ``height``
  property in an HTML img tag.

  Github: https://github.com/repoze/repoze.bitblt

- ``repoze.squeeze``

  This package provides a WSGI middleware component which
  "squeezes" HTML documents by merging browser resources
  (javascript and stylesheets).

  Github: https://github.com/repoze/repoze.squeeze

Obsolete Repoze Components
==========================

These components are no longer actively maintained:  in most cases,
they have been obsoleted by newer software.

WSGI Applications
-----------------

- ``repoze.bfg``


  ``repoze.bfg`` is a WSGI web framework inspired by Zope, Pylons,
  and Django.  It uses Zope libraries to do much of its work.

  Obsoleted by Pyramid (see http://trypyramid.com/).

  Website:  http://bfg.repoze.org/

- ``repoze.obob``

  A stripped-down object publisher that acts as a WSGI application.
  It is responsible for:

  o selecting the "root" object of the graph for a given request
    / URL;

  o traversing from that root object along the "edges" defined
    by the URL path elements to find the "published object";

  o invoking the published object to obtain the body;

  o mapping response headers and body, along with the result
    from calling the published object, into appropriate WSGI
    output;

  o serializing / encoding the response based on the type of the
    request (e.g., JSON / XML-RPC).

  ``repoze.obob`` is currently more of a "publisher driver" than a
  publisher.  Most of the actual work is done by "bob" modules
  which obob drives (repoze.zope2 is a "bob").

  ``repoze.obob`` is used by ``repoze.zope2``, but is otherwise not
  being actively developed at this point.

  Obsoleted by Pyramid (see http://trypyramid.com/).

  SVN:  http://svn.repoze.org/repoze.obob/trunk/

- ``repoze.zope2``

  A "bob" helper module that implements an analogue of the Zope 2
  ZPublisher, with some major simplifications and cleanups.  Its core
  mission is to allow publishing existing Zope2 applications in a
  WSGI environment that externalizes some of the features of "classic"
  Zope2 into middleware.

  ``repoze.zope2`` is capable of publishing all known Zope
  applications, including applications which rely on WebDAV and
  XML-RPC, as well as all known Plone applications.

  Obsoleted by `Zope 2.13.x release <https://pypi.python.org/pypi/Zope2>`_

  SVN: http://svn.repoze.org/repoze.zope2/trunk/

- ``repoze.plone``

  A meta-egg which depends on all Plone component eggs as well as
  ``repoze.zope2``.

  Obsoleted by `Plone4 release <https://plone.org/products/plone>`_

  SVN: http://svn.repoze.org/repoze.plone/trunk

- ``repoze.grok``

  A "bob" helper module that implements an analogue of the Zope 3
  publication machinery in order to serve up Grok applications.
  
  Abandoned.

  SVN: http://svn.repoze.org/repoze.grok/trunk/

- ``repoze.mmwsgi``

  WSGI wrapper that allows Mailman to be run simply under a WSGI server.
  
  Abandoned.

  SVN: http://svn.repoze.org/repoze.mmwsgi/trunk/

- ``repoze.kiss``

  A "bob" module which publishes content (files, images, templates) from the
  filesystem, using the ``repoze.zope2`` helper.
  
  Runs the http://www.repoze.org/ website.

  SVN: http://svn.repoze.org/repoze.kiss/trunk/

WSGI Middleware
---------------

- ``repoze.what``

  An authorization framework for WSGI applications, based on ``repoze.who``.
  
  Abandoned (after moving to Github).

  Github: https://github.com/repoze/repoze.what

- ``repoze.browserid``

  ``repoze.browserid`` is WSGI middleware loosely based on the
  Zope 2 concept of "browser ids", which are cookies which
  represent a browser, for use by sessioning libraries.
  
  Abandoned (after moving to Github).

  Github: https://github.com/repoze/repoze.browserid

- ``repoze.tempita``

  ``repoze.tempita`` is WSGI middleware egress filter which
  conditionally causes the body returned by the application
  to be run through the `Tempita <http://pythonpaste.org/tempita/>`_
  templating engine, using replacement values defined within the
  ``repoze.tempita`` Paste middleware configuration.  Abandoned.

  SVN: http://svn.repoze.org/repoze.tempita/trunk/

- ``repoze.decsec``

  Declarative ACL-based security via middleware for WSGI applications.
  
  Not widely used.

  SVN: http://svn.repoze.org/repoze.decsec/trunk/


Libraries
---------

- ``repoze.monty``

  A library that, given a WSGI environment dictionary (and a ``wsgi.input``
  file pointer if the request is a POST request), will return a dictionary
  containing "converted" form/query string elements.  The form and query
  string elements contained in the request are converted into
  simple Python types when the form element names are decorated
  with special suffixes.

  SVN: http://svn.repoze.org/repoze.monty/trunk/

- ``repoze.urispace``

  A library implementig the URISpace 1.0 spec, as proposed
  to the W3C by Akamai.  Its aim is to provide an implementation
  of that language as a vehicle for asserting declarative metadata
  about a resource based on pattern matching against its URI.

  SVN: http://svn.repoze.org/repoze.urispace/trunk/

  Docs: http://docs.repoze.org/urispace/

Buildout-related
----------------

The following are ``zc.buildout`` (see http://www.buildout.org) recipes and
configuration files:

- Buildouts for ``repoze.bfg``: http://svn.repoze.org/buildouts/repoze.bfg/

- Buildouts for ``repoze.zope2``:  http://svn.repoze.org/buildouts/repoze.zope2/

- Buildouts for ``repoze.plone`` http://svn.repoze.org/buildouts/repoze.plone/

- ``repoze.recipe.egg``

  A fork of the ``zc.recipe.egg`` `zc.builout`` recipe.  (see
  http://pypi.python.org/pypi/zc.recipe.egg).  It does exactly what 
  ``zc.recipe.egg`` does, except it also automatically installs scripts
  from dependent eggs.  This software is deprecated.

  SVN: http://svn.repoze.org/repoze.recipe.egg/trunk

Miscellany
----------

These components are (mostly) unsupported "convenience" things:

- ``repoze.django``

  A mechanism to run Django under a Paste server.

  SVN: http://svn.repoze.org/repoze.django/trunk/

- ``repoze.trac``

  A mechanism to run Trac under a Paste server.

  SVN: http://svn.repoze.org/repoze.trac/trunk/

- ``whoplugins``

  Contributed ``repoze.who`` plugins.

  SVN: http://svn.repoze.org/whoplugins/

Re-packaged Software
--------------------

- ``zopelib`` (no SVN)

  ``zopelib`` is the entire set of Zope "software home"
  ``Products``-namespace packages packaged as a
  setuptools-compatible package.  The script that allows for
  this is checked into `Repoze's CVS repository <http://tinyurl.com/3cfelw .>`_
  That script is meant to be dropped into a checkout of a Zope "software home"
  and run from there to repeatably package Zope 2 as an sdist or
  bdist.

- ``cmflib`` (no SVN)

  ``cmflib`` is the Zope CMF packaged as a setuptools-compatible
  package.  It includes all the Zope ``Products``-namespace
  packages that are present in the classic CMF distribution
  (Products.CMFActionIcons, Products.CMFCalendar,
  Products.CMFCore, Products.CMFDefault, Products.CMFTopic,
  Products.CMFUid, Products.DCWorkflow) save for one: it has a
  dependency on an independently release-managed distribution of
  Products.GenericSetup.  It was generated by using a
  "setup.py",
  http://svn.zope.org/Sandbox/chrism/eggcmf/2.1.0/setup.py?view=markup
  checked into a location which depends on
  `externals in Zope Corporation's SVN repository <http://svn.zope.org/Sandbox/chrism/eggcmf/>`_

- ``plonelibs`` (no SVN)

  ``plonelibs`` is a setuptools-compatible repackaging of the
  packages that ship in Plone 3's "lib/python" directory.

- ``ploneproducts`` (no SVN)

  ``ploneproducts`` is a setuptools-compatible repackaging of the
  ``Products``-namespace packages that ship in Plone 3.

  It depends on separately released-managed distributions of
  Products.PluggableAuthService and Products.PluginRegistry.

- ``PIL`` (no SVN)

  ``PIL`` is a repackaging of the
  Python Imaging Library (see http://www.pythonware.com/products/pil/)
  as a setuptools-compatible package.

  Obsoleted by Pillow (https://pypi.python.org/pypi/Pillow).
