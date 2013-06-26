Hacking on Repoze Components
============================

.. _coding-standards:

Coding Standards
----------------

As a general rule, projects in the ``repoze`` repositories abide by the
following standards:

- `PEP 8 coding style <http://www.python.org/dev/peps/pep-0008/>`_. In
  particular, *Python code should never exceed 80 columns*.

- Project trunks should be kept in "ready-to-release" state:  all unit
  tests pass, changelogs are kept update, etc.

- 100% test coverage before release, as reported by the :mod:`nose`
  test runner with the :mod:`coverage` add-on:

  .. code-block: sh

     $ /path/to/nosetests
     ............................................
     Name               Stmts   Exec  Cover   Missing
     ------------------------------------------------
     ...
     ------------------------------------------------
     TOTAL                522    522   100%   
     ----------------------------------------------------------------------
     Ran 44 tests in 0.201s

     OK

  
- Tests should be runnable using the default :mod:`setuptools` test runner:

  .. code-block: sh

     $ /path/to/python setup.py test

- Full documentation of features and APIs.

- Solid release management, including releases to PyPI corresponding to
  "pristine" tags, detailed change logs, etc.

While some older projects may not be completely in line with this
culture, we are committed to moving them all closer with any change.
As a corollary:  if you are suubmitting a patch to a project in this
repository, and you want expedite its acceptance, ensure that your patch
maintains or improves the target project's conformance to these goals.

.. _layout-conventions:

Layout and Conventions
----------------------

Each project should consist of a single, top-level project folder in
Subverion, containing three conventional folders:  ``trunk``, where the
majority of development work occurs, ``tags``, containing the "pristine"
tags made when releasing the project, and ``branches``, containing both
"maintenance" branches where bug fixes to a released version might be
made, and "development" branches, for work which would otherwise de-
stabilize the trunk.

Because we are mostly working on Python code here, the trunk and folders
under the ``tags`` or ``branches`` folders are normally arranged as a
:mod:`distutils` project, e.g.::

  <directory>
  - setup.py
  - README.txt
  - CHANGES.txt
  + docs/
    - Makefile
    - conf.py
    - index.rst
    - api.rst
    + .static/
    + .build/
    + .templates/
  + package/
    - __init__.py
    + subpacakge/
      - __init__.py
      - module.py
      + tests/
        - __init__.py
        - test_module.py
      + templates/
        - template.pt

For an example of this layout, see http://svn.repoze.org/template/trunk/ .


.. _dvcs-overview:

Distributed Version Control Systems
===================================

Under Subversion, the version repository is kept on a central server:
each developer has a working subset checked out from that server onto
her own machine.

Using a distributed version control systems (DVCS), each developer clones
the entire repository onto her machine.  Although it may take more space or
bandwidth, having this clone allows the developer a lot of flexibility and
freedom:  she can hack, make commits, etc., to her local clone without
needing network access, or even permission to write back to the source server! 

.. note::

   Actively-supported Repoze projects are now hosted on Github under the
   `Repoze organization <https://github.com/organizations/repoze>`_


.. _tool_specific:

Using Specific VCS Tools with Repoze Projects
=============================================

For the actively maintained components maintained on Github, use the
"normal" git / Github workflow:

- Fork the repository.

- Hack on a clone of your fork in a branch.

- When ready, push your branch and submit a pull request.

We advise that you *not* hack on the ``master`` branch of your fork,
so that you can sync more easily as changes are pushed to the upstream
Repoze repository.

.. toctree::
   :maxdepth: 2

   svn
   git
