Working with Mercurial
======================

.. todo:

   Add notes on general Mercurial info, links to docs, etc.

.. _branching-hg:

How-to: Branch using the Mercurial mirror
-----------------------------------------

The Repoze project hosts a Mercurial mirror of the Repoze SVN repository:

 http://hg.repoze.org/

The mirror is updated periodically as commits are made to the SVN repository.
You may use this mirror to obtain a Mercurial checkout directly, for example:

.. code-block:: sh

   $ hg clone http://hg.repoze.org/chameleon/


.. _branching-hg-svn:

How-to: Branch directly from Subversion
---------------------------------------

Recent versions of Mercurial and the `hgsubversion plugin
<http://bitbucket.org/durin42/hgsubversion/overview/>`_ allow the
developer to interoperate with a project whose main repository is in
Subversion.  Using this plugin, you can check out the branch from its
native HTTP URL:

.. code-block:: sh

   $ cd ~/repoze
   $ hg clone svn+http://svn.repoze.org/repoze.who

You may check out any subdirectory of the Repoze SVN repository that
has the typical SVN "branches", "tags" and "trunk" layout.  The
branches, tags, and trunk will be imported into the resulting local hg
repository in a sensible manner.

Inside the checkout, you can commit as usual using ``hg``, but you
won't be able to ``hg push`` the code back to Subversion unless you
use an ``svn+ssh`` checkout URL (see :ref:`svn-write-access`).

.. _submitting-patches-hg:

How-to: Submit a patch from your Mercurial branch
-------------------------------------------------

From your Mercurial branch, you can use ``hg diff`` to create a patch file,
and then submit it just as in :ref:`submitting-patches-svn` above.  

Mercurial has another built-in plugin, ``hg email`` (aka
``patchbomb``) , which you can use to automate submitting the patch
via e-mail:

.. code-block:: sh

   $ hg email --subject="Cool feature" \
        --attach --bundle --to=repoze-dev@lists.repoze.org

Please see the `patchbomb documentation
<http://mercurial.selenic.com/wiki/PatchbombExtension>`_ for directions on
configurint your mail transport properly.

How-to:  Push your Mercurial branch to a public server
------------------------------------------------------

As an alternative to uploading a patch from your Mercurial branch (or
e-mailing it), you can also publish your branch to a server where it
can be cloned over HTTP for others to use, as well as for review and
merging by the package maintainer.

Let's ssume that you have been hacking on :mod:`repoze.who`, and want to
publish your 'saml-2.0' feature branch in hopes of landing it in the next
release.  Let's also assume that you have an account on
`Bitbucket <http://bitbucket.org/>`_, and want to publish your branch there.
First, create the new empty repository on Bitbucket's `Create a Repository
page <http://bitbucket.org/repo/create/>`_.  Give the repository the name
``repoze.who-saml_2.0``, add a description, and hit submit.

Then, from your terminal, push your branch to the new repository:

.. code-block:: sh

   $ hg push http://bitbucket.org/<userid>/repoze.who-saml_2.0

Replace ``<userid>`` with your Bitbucket account ID.


Pushing to other services
#########################

According to Wikipedia's `Mercurial article
<http://en.wikipedia.org/wiki/Mercurial(software)>`_,
a number of other code-hosting services support Mercurial branches.  You should
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

How-to: Request a Merge
-----------------------

After pushing your branch, you can include its URL in an e-mail you send
to the maintainer, requesting a merge of your branch, or in a comment or
description of an issue in the tracker.
