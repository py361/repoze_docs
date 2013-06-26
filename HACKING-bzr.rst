Working with Bazaar
===================

`bzr <http://bazaar-vcs.org/>`_ is one of the current generation of
distributed version control systems (DVCS).

- a `five minute overview
  <http://doc.bazaar.canonical.com/latest/en/mini-tutorial/>`_ of using 
  Bazaar.

- the `Bazaar User Guide
  <http://doc.bazaar.canonical.com/latest/en/user-guide/index.html>`_

.. _branching-bzr:

How-to: Branch using the Bazaar mirror
--------------------------------------

The repoze project maintains a "mirror" of its Subversion repository as
a collection of Bazaar branches:

  http://bzr.repoze.org/

The mirror is updated periodically as commits are made to the SVN repository.
You can create a branch from the URLs there as with any other web-hosted
Bazaar branch:

.. code-block:: sh

   $ bzr branch http://bzr.repoze.org/repoze.who/trunk repoze.who-trunk

Because all ``repoze`` projects are hosted in a centralized repository,
the DVCS needs to pull down lots of information about revisions which aren't
directly related to the branch you want to work on.  In order to keep this
overhead down, especially if you plan to work on multiple ``repoze`` projects,
you can create a "shared repository" for your branches before checking
any of them out:

.. code-block:: sh

   $ mkdir ~/repoze
   $ cd ~/repoze
   $ bzr init-repo
   $ bzr branch http://bzr.repoze.org/repoze.who/trunk repoze.who-trunk


.. _branching-bzr-svn:

How-to:  Branch with Bazaar directly from Subversion
----------------------------------------------------

Recent versions of bzr and the `bzr-svn plugin
<http://doc.bazaar.canonical.com/plugins/en/svn-plugin.html>`_ allow the
developer to interoperate with a project whose main repository is in
Subversion.  Using this plugin, you can check out the branch from its
native HTTP URL:

.. code-block:: sh

   $ cd ~/repoze
   $ bzr co svn+http://svn.repoze.org/repoze.who-trunk who-trunk

Inside that branch, you can commit as usual using ``bzr``, but you
won't be able to ``bzr push`` the code back to Subversion unless you
use an ``svn+ssh`` checkout URL (see :ref:`svn-write-access`).


.. _submitting-patches-bzr:

How-to: Submit a patch from your Bazaar branch
----------------------------------------------

From your Bazaar branch, you can use ``bzr diff`` to create a patch file,
and then submit it just as in :ref:`submitting-patches-svn` above.  

Bazaar has another feature, ``bzr send``, which you can use to automate
submitting the patch, either via e-mail:

.. code-block:: sh

   $ bzr send --message="Cool feature" --mail-to=repoze-dev@lists.repoze.org

or as a file to be uploaded to the bug tracker:

.. code-block:: sh

   $ bzr send --message="Cool feature" -o /tmp/repoze.who-my_cool_feature.patch


.. _pushing-branches-bzr:

How-to:  Push your Bazaar branch to a public server
---------------------------------------------------

As an alternative to uploading a patch from your Bazaar branch (or
e-mailing it), you can also publish your branch to a server where it
can be cloned over HTTP for others to use, as well as for review and
merging by the package maintainer.

Let's ssume that you have been hacking on :mod:`repoze.who`, and want to
publish your 'saml-2.0' feature branch in hopes of landing it in the next
release.  Let's also assume that you have an account on
`Launchpad <http://launchpad.net/>`_, and want to publish your branch there.

.. code-block:: sh

   $ bzr launchpad-login <userid>
   $ bzr push lp:~<userid>/+junk/repoze.who-saml_2.0

Replace ``<userid>`` with your Launchpad account ID.

.. note::
   
   The ``+junk`` name is a signal that your branch is not affiliated with
   any existing Launchpad project), and not a value judgement about the
   code.

Pushing to other services
#########################

According to Wikipedia's `Bazaar article
<http://en.wikipedia.org/wiki/Bazaar_(software)>`_,
a number of other code-hosting services support Bazaar branches.  You should
be able to publish your branch to any of them in a similar way.

Pushing to your own server
##########################

You should be able to pubish your branch on any public webserver where you
have space available, using the SSH protocol.  E.g., assume that you have
an account on ``example.com``, where the contents of your home directory's
``htdocs`` directory are published under your userid:

.. code-block:: sh

   $ bzr push ssh://example.com/home/<youraccount>/htdocs/<branch-name>

You can then use http://example.com/~youraccount/branch-name to make the
branch available to others.

How-to: Request a merge
-----------------------

After pushing your branch, you can include its URL in an e-mail you send
to the maintainer, requesting a merge of your branch, or in a comment or
description of an issue in the tracker.
