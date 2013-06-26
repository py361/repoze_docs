Repoze Components
=================

The Repoze project consists of of the following software components.

WSGI Applications
-----------------

- `repoze.bfg <http://bfg.repoze.org/>`_

  'repoze.bfg' is a WSGI web framework inspired by Zope, Pylons,
  and Django.  It uses Zope libraries to do much of its work.

- `repoze.obob <http://svn.repoze.org/repoze.obob/trunk/>`_

  'repoze.obob' is a stripped-down object publisher that acts as
  a WSGI application.  It is responsible for:

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

  repoze.obob is currently more of a "publisher driver" than a
  publisher.  Most of the actual work is done by "bob" modules
  which obob drives (repoze.zope2 is a "bob").

  'repoze.obob' is used by 'repoze.zope2', but is otherwise not
  being actively developed at this point.

- `repoze.zope2 <http://svn.repoze.org/repoze.zope2/trunk/>`_

  'repoze.zope2' is a "bob" helper module that implements an
  analogue of the Zope 2 ZPublisher, with some major
  simplifications and cleanups.  Its core mission is to allow
  publishing existing Zope2 applications in a WSGI environment
  that externalizes some of the features of "classic" Zope2 into
  middleware.

  'repoze.zope2' is capable of publishing all known Zope
  applications, including applications which rely on WebDAV and
  XML-RPC, as well as all known Plone applications.

- `repoze.plone <http://svn.repoze.org/repoze.plone/trunk/>`_

  'repoze.plone' is a meta-egg which depends on all Plone
  component eggs as well as repoze.zope2.

- `repoze.grok <http://svn.repoze.org/repoze.grok/trunk/>`_

  'repoze.grok' is a "bob" helper module that implements an
  analogue of the Zope 3 publication machinery in order to serve
  up Grok applications.

- `repoze.kiss <http://svn.repoze.org/repoze.kiss/trunk/>`_

  'repoze.kiss' is a "bob" module which publishes content
  (files, images, templates) from the filesystem, using the
  'repoze.zope2' helper.  It runs this website.

- `repoze.mmwsgi <http://svn.repoze.org/repoze.mmwsgi/trunk/>`_

  'repoze.mmwsgi' is a WSGI wrapper that allows Mailman to be
  run simply under a WSGI server.

WSGI Middleware
---------------

- `repoze.bitblt <http://svn.repoze.org/repoze.bitblt/trunk/>`_

  'repoze.bitblt' is a WSGI middleware component which
  automatically scales images according to the 'width' and 'height'
  property in an HTML img tag.

- `repoze.squeeze <http://svn.repoze.org/repoze.squeeze/trunk>`_

  This package provides a WSGI middleware component which
  "squeezes" HTML documents by merging browser resources
  (javascript and stylesheets).

- `repoze.tm2 <http://svn.repoze.org/repoze.tm2/trunk/>`_

  'repoze.tm2' is WSGI middleware that implements a transaction
  policy.  It uses the 'transaction' module (shipped with ZODB)
  to commit or abort (if there is an exception) a transaction
  after each WSGI request.

  Applications may register callbacks with 'repoze.tm2' (e.g.,
  to close a connection, mainly).  This behavior used to be
  hardcoded in Zope's publisher.  'repoze.tm2' is useful in any
  web application that requires transactions.

- `repoze.retry <http://svn.repoze.org/repoze.retry/trunk/>`_

  'repoze.retry' is WSGI middleware that retries a WSGI request
  some configurable number of times if any child application
  raises a ZODB ConflictError.  This behavior used to be
  hardcoded in Zope's publisher.  repoze.retry is currently only
  useful in the context of an application which uses ZODB.

  TODO: investigate whether any useful RDBMS analogue exists
  (e.g., see the 'storm' mailing list).

- `repoze.vhm <http://svn.repoze.org/repoze.vhm/trunk/>`_

  'repoze.vhm' is WSGI middleware which normalizes
  specially-mangled URLs (or individual header values) into
  ordinary paths, with the additional information stored in the
  environment for use in generating dynamic URLs.  It is an
  analogue / replacement for the Zope2 Virtual Host Monster.

- `repoze.errorlog <http://svn.repoze.org/repoze.errorlog/trunk/>`_

   'repoze.errorlog' implements a WSGI middleware filter which
   intercepts exceptions and writes them to a Python 'logging'
   module channel (or the 'wsgi.errors' filehandle, if no
   channel is configured).  It also allows the browsing of
   limited exception history via a browser UI.

- `repoze.profile <http://svn.repoze.org/repoze.profile/trunk/>`_

  'repoze.profile' provides a WSGI middleware component which
  aggregates Python profiling data across all requests to a WSGI
  application.  It provides an HTML UI for viewing profiling
  data.

- `repoze.who <http://docs.repoze.org/who>`_

  'repoze.who' is an identification and authentication framework
  for arbitrary WSGI applications.  It acts as WSGI middleware.
  It is inspired by Zope 2's Pluggable Authentication Service
  (PAS) but it is not dependent on Zope in any way.

- `repoze.what <http://docs.repoze.org/what>`_

  'repoze.what' is an authorization framework for WSGI
  applications, based on 'repoze.who'.

- `repoze.tempita <http://svn.repoze.org/repoze.tempita/trunk/>`_

  'repoze.tempita' is WSGI middleware egress filter which
  conditionally causes the body returned by the application
  to be run through the `Tempita <http://pythonpaste.org/tempita/>`_
  templating engine, using replacement values defined within the
  'repoze.tempita' Paste middleware configuration.

- `repoze.browserid <http://svn.repoze.org/repoze.browserid/trunk/>`_

  'repoze.browserid' is WSGI middleware loosely based on the
  Zope 2 concept of "browser ids", which are cookies which
  represent a browser, for use by sessioning libraries.

- `repoze.zodbconn <http://svn.repoze.org/repoze.zodbconn/trunk/>`_

  Library which manages ZODB databases and WSGI middleware which
  makes a ZODB connection available to downstream applications.

- `repoze.decsec <http://svn.repoze.org/repoze.decsec/trunk/>`_

  Declarative ACL-based security via middleware for WSGI
  applications.  Not widely used.

- `repoze.debug <http://svn.repoze.org/repoze.debug/trunk/>`_

  Middleware which can help with in-production forensic debugging.

Libraries
---------

- `repoze.evolution <http://docs.repoze.org/evolution>`_

  'repoze.evolution' is a package which allows you to keep
  persistent data structures (data in a relational database, on
  the filesystem, in a persistent object store, etc) in sync
  with changes made to software.  It does so by allowing you to
  create and use a package full of monotonically named "evolve"
  scripts which modify the data; each script brings the data up
  to some standard of a software version.

- `repoze.catalog <http://docs.repoze.org/catalog>`_

  An indexing and searching system based on 'zope.index'.

- `repoze.session <http://docs.repoze.org/session>`_

  A sessioning system (server side state for web applications)
  based on ZODB.

- `repoze.formapi <http://svn.repoze.org/repoze.formapi/trunk/>`_

  The ``repoze.formapi`` provides a form library which
  integrates with HTML forms instead of abstracting them away.
  It provides a small framework to take you through the entire
  process of rendering a form, provide default values, validate
  and execute form actions.

- `repoze.monty <http://svn.repoze.org/repoze.monty/trunk/>`_

  'repoze.monty' is a library that, given a WSGI environment
  dictionary (and a 'wsgi.input' file pointer if the request is
  a POST request), will return a dictionary back containing
  "converted" form/query string elements.  The form and query
  string elements contained in the request are converted into
  simple Python types when the form element names are decorated
  with special suffixes.

- `repoze.urispace <http://docs.repoze.org/urispace>`_

  'repoze.urispace' implements the URISpace 1.0 spec, as proposed
  to the W3C by Akamai.  Its aim is to provide an implementation
  of that language as a vehicle for asserting declarative metadata
  about a resource based on pattern matching against its URI.

- 'zopelib' (no SVN)

  'zopelib' is the entire set of Zope "software home"
  'Products'-namespace packages packaged as a
  setuptools-compatible package.  The script that allows for
  this is checked into `Repoze's CVS repository <http://tinyurl.com/3cfelw .>`_
  That script is meant to be dropped into a checkout of a Zope "software home"
  and run from there to repeatably package Zope 2 as an sdist or
  bdist.

- 'cmflib' (no SVN)

  'cmflib' is the Zope CMF packaged as a setuptools-compatible
  package.  It includes all the Zope 'Products'-namespace
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

- 'plonelibs' (no SVN)

  'plonelibs' is a setuptools-compatible repackaging of the
  packages that ship in Plone 3's "lib/python" directory.

- 'ploneproducts' (no SVN)

  'ploneproducts' is a setuptools-compatible repackaging of the
  'Products'-namespace packages that ship in Plone 3.

  It depends on separately released-managed distributions of
  Products.PluggableAuthService and Products.PluginRegistry.

- 'PIL' (no SVN)

  'PIL' is a repackaging of the
  `Python Imaging Library <http://www.pythonware.com/products/pil/>`_
  as a setuptools-compatible package.

Buildout-related
----------------

The following are `zc.buildout <http://www.buildout.org>`_ recipes and
configuration files:

- Buildouts for
  `repoze.bfg <http://svn.repoze.org/buildouts/repoze.bfg>`_

- Buildouts for
  `repoze.zope2 <http://svn.repoze.org/buildouts/repoze.zope2>`_

- Buildouts for
  `repoze.plone <http://svn.repoze.org/buildouts/repoze.plone>`_

- `repoze.recipe.egg <http://svn.repoze.org/repoze.recipe.egg/trunk>`_

  'repoze.recipe.egg' is a fork of
  `zc.recipe.egg <http://pypi.python.org/pypi/zc.recipe.egg , a>`_
  zc.builout recipe.  It does exactly what zc.recipe.egg does,
  except it also automatically installs scripts from dependent
  eggs.  This software is deprecated.

Miscellany
----------

These components are (mostly) unsupported "convenience" things:

- `repoze.django <http://svn.repoze.org/repoze.django/trunk/>`_

  A mechanism to run Django under a Paste server.

- `repoze.trac <http://svn.repoze.org/repoze.trac/trunk/>`_

  A mechanism to run Trac under a Paste server.

- `whoplugins <http://svn.repoze.org/whoplugins>`_

  Contributed 'repoze.who' plugins.
