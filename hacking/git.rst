Working with Git
================

.. todo:

   Add notes on general Git info, links to docs, etc.

.. _branching-git:

How-to: Branch using the Git mirror
-----------------------------------

The Repoze project hosts a Git mirror of the Repoze SVN repository:

  http://git.repoze.org/

The mirror is updated periodically as commits are made to the SVN
repository.  You may use this mirror to obtain a Git checkout
directly, for example:

.. code-block:: sh

   $ git clone http://git.repoze.org/chameleon/.git

.. note::

   The ``.git`` in the URL follows the slash:  this is an odditiy
   of the current mirroring strategy, and may be subject to change.


.. _branching-git-svn:

How-to: Branch with Git directly from Subversion
------------------------------------------------

Git ships with a ``git svn`` `subcommand
<http://www.kernel.org/pub/software/scm/git/docs/git-svn.html>`_ which
allows a developer to interoperate with a project whose main repository
is in Subversion.  Using this plugin, you can clone the branch from its
native HTTP URL:

.. code-block:: sh

   $ cd ~/repoze
   $ git svn --stdlayout clone svn+http://svn.repoze.org/repoze.who

You may check out any subdirectory of the Repoze SVN repository that
has the typical SVN "branches", "tags" and "trunk" layout.  The
branches, tags, and trunk will be imported into the resulting local Git
repository in a sensible manner.

Inside the checkout, you can commit as usual using ``git``, but you
won't be able to ``git svn dcommit`` the code back to Subversion unless
you use an ``svn+ssh`` checkout URL (see :ref:`svn-write-access`).

.. _submitting-patches-git:

How-to: Submit a patch from your Git branch
-------------------------------------------

From your Git branch, you can use ``git format-patch`` to create a series
of patch files, and then submit them via e-mail or the issue tracker,
just as in :ref:`submitting-patches-svn`.

.. code-block:: sh

   $ git format-patch origin -CM --subject="Cool feature" \
        --to=repoze-dev@lists.repoze.org --from=your.email@example.com

Git has another built-in plugin, ``git send-email`` , which you can use to
automate submitting the patch files via e-mail:

.. code-block:: sh

   $ git send-email origin -CM --subject="Cool feature" \
        --to=repoze-dev@lists.repoze.org --from=your.email@example.com \
        --smtp-server=locahost --smtp-server-port=25

Please see the `git-send-email documentation
<http://www.kernel.org/pub/software/scm/git/docs/git-send-email.html>`_
for directions on how to configure your mail transport properly.

How-to:  Push your Git branch to a public server
------------------------------------------------

As an alternative to uploading a patch from your Git branch (or
e-mailing it), you can also publish your branch to a server where it
can be cloned over HTTP for others to use, as well as for review and
merging by the package maintainer.

Let's ssume that you have been hacking on :mod:`repoze.who`, and want to
publish your 'saml-2.0' feature branch in hopes of landing it in the next
release.  Let's also assume that you have an account on
`GitHub <http://github.com/>`_, and want to publish your branch there.
First, create the new empty repository on Github's `New Repository
page <http://github.com/repositories/new/>`_.  Give the repository the name
``repoze.who-saml_2.0``, add a description, and hit submit.

Then, from your terminal, push your branch to the new repository:

.. code-block:: sh

   $ git remote add github git@github.com:<userid>/repoze.who-saml_2.0.git
   $ git push github master

Replace ``<userid>`` with your Github account ID.


Pushing to other services
#########################

According to Wikipedia's `Git article
<http://en.wikipedia.org/wiki/Git_(software)>`_,
a number of other code-hosting services support Git branches.  You should
be able to publish your branch to any of them in a similar way.

Pushing to your own server
##########################

You should be able to pubish your branch on any public webserver where you
have space available, using the SSH protocol.  E.g., assume that you have
an account on ``example.com``, where the contents of your home directory's
``htdocs`` directory are published under your userid:

.. code-block:: sh

   $ git clone --bare /path/to/repoze.who-saml_2.0 repoze.who-saml_2.0.git
   $ cd repoze.who-saml_2.0.git
   $ touch git-daemon-export-ok
   $ git --bare update-server-info
   $ mv hooks/post-update.example hooks/post-update
   $ cd ..
   $ rsync -avz repoze.who-samle_2.0.git \
      example.com:/home/<youraccount>/htdocs/

You can then use http://example.com/~youraccount/repoze.who-saml_2.0.git
to make the branch available to others.

How-to: Request a Merge
-----------------------

After pushing your branch, you can include its URL in an e-mail you send
to the maintainer, requesting a merge of your branch, or in a comment or
description of an issue in the tracker.
