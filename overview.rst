An Overview of the Repoze Project
=================================

Early Developments
------------------

The Repoze project began in September, 2007, as a response to the perception
that the Zope community was stuck in a "ghetto", isolated from the rest of
the Python web development world.  The project had two main goals:

- Help make interesting features of the Zope development ecosystem
  available and interesting to the wider Python web developer community.

- Make the cool new features offered by that community accessible to
  Zope developers.

One primary focus for this early work was making the core Zope2 application
server usable inside the new de facto standards of eggs (for distributions
of Python projects) and WSGI (for connecting Python web servers interoperably
with Python web applications).

Part of that task involved mapping the features of Zope's "publisher"
(the framework mapping URLs and request variables onto Python code) onto
the WSGI world.  As a result of that work, important features of the
publisher machinery became usable outside of Zope as WSGI middleware:

- :mod:`repoze.tm` and :mod:`repoze.tm2` made it possible to use Zope's
  model of transaction-per-request cleanly onto any web application which
  uses the :mod:`transaction` package originally developed as part of
  :mod:`ZODB`.

- :mod:`repoze.retry` made it possible to map the feature of the publisher
  which retries requests which would otherwise fail due to conflicts in
  an optimistic concurrency model, e.g. as raised by ZODB or Postgres.

While disentangling these features of the Zope publisher into components
which could be re-used outside of Zope, it became clear that there was a
smaller, more cohesive model for doing the real business of the publisher.
The initial implementation of such a generic package (see :mod:`repoze.obob`
in the repository) formed the basis for :mod:`repoze.zope2`, an almost-
compabible implementation of the Zope2 publisher as a well-behaved WSGI
application.  This package delegates a number of the hard-wired features
of the Zope2 publisher (transaction and retry handling, virtual hosting, 
etc.) to the equivalent Repoze middleware components.

Later Developments
------------------

Since its inception, the Repoze project has overstepped the bounds of
its original goals.  Instead of acting strictly as a clearinghouse
which makes Zope technologies available to a larger Python community,
the Repoze community is now producing its own components.  These
components may only be inspired by Zope technology, or may have no
analogue in the Zope world.

For example:

- Chris McDonough set out to re-implement the Zope publisher model as
  a leaner, lighter weight web framework, now called `BFG
  <http://bfg.repoze.org>`_.

- Tres Seaver created `Compoze <http://docs.repoze.org/compoze>`_
  which provides various tools for working with Python "egg"
  distributions and package indexes.

And so on.

See `docs.repoze.org <http://docs.repoze.org>`_ for documentation for
all the components produced so far by the Repoze project.

See `svn.repoze.org <http://svn.repoze.org>`_ for all the source code
produced by the Repoze project.

