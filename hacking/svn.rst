Working with Subversion
=======================

.. warning::

   These instructions are only valid for Repoze components which have
   not been migrated to Github.

.. _read-only-subversion-checkout:

How-to: Get a read-only Subversion checkout
-------------------------------------------

Anonymous, read-only Subversion checkouts can be made over HTTP:

.. code-block:: sh

   $ svn co http://svn.repoze.org/repoze.who/trunk who-trunk

You should then be able to work inside ``who-trunk``, fixing a bug or
adding a feature.  You can use Subversion commands as normal, e.g.:

.. code-block:: sh

   $ cd who-trunk/
   $ svn info
   Path: .
   URL: http://svn.repoze.org/repoze.who/trunk
   Repository Root: http://svn.repoze.org
   Repository UUID: 8f1d8bf8-68d2-4fbe-a113-2afb08c80ed9
   Revision: 8672
   Node Kind: directory
   Schedule: normal
   Last Changed Author: Tres Seaver <tseaver@palladion.com>
   Last Changed Rev: 8673
   Last Changed Date: 2010-03-26 16:21:39 -0400 (Fri, 26 Mar 2010)

Let's say you wanted ot add a bit of explanation to the :file:`README.txt`
file:

.. code-block:: sh

   $ vi README.txt
   ...

Subversion knows about the changes you made:

.. code-block:: sh

   $ svn stat
   M      README.txt
   $ svn diff
   Index: README.txt
   ===================================================================
   --- README.txt	(revision 8276)
   +++ README.txt	(working copy)
   @@ -8,6 +8,8 @@
    for arbitrary WSGI applications.  ``repoze.who`` can be configured
    either as WSGI middleware or as an API for use by an application.
 
   +Blah, blah
   +
    ``repoze.who`` is inspired by Zope 2's Pluggable Authentication
    Service (PAS) (but ``repoze.who`` is not dependent on Zope in any
    way; it is useful for any WSGI application).  It provides no facility

You can keep your checkout updated with ongoing changes, too:

.. code-block:: sh

   $ svn up
   U    docs/api.rst
   U    docs/conf.py
   Updated to revision 8673.

and you may have to deal with changes which conflict with those you
have made.

However, because you are working in an anonymous, read-only checkout, you
cannot commit your changes back to the repository.

.. code-block:: sh

   $ svn commit -m "R00l da world."
   svn: Commit failed (details follow):
   svn: Can't create directory '/home/repoze/svn/db/transactions/8675-1.txn': \
     Permission denied

Oops, is all your hard work in vain?


.. _submitting-patches-svn:

How-to: Submit a patch from your Subversion checkout
----------------------------------------------------

Once you have fixed the bug or added the feature in your checkout, double-
check that you have touched all the bases (see :ref:`coding-standards`
and :ref:`layout-conventions`).  All is well, the tests pass, you added
documentation for your cool new feature, so it is time to submit the patch.

First, **don't** try to cut and paste the output from ``svn diff`` into an
e-mail message or a web-browser textarea:  such operations usually end up
mangling the line endings or other bits of the diff, and make it impossible
to apply cleanly.  The maintainer who has to do reconstructive surgery on
such a victim may just give up and ignore the patch.

Avoiding the cut-and-paste train wreck is straightforward:  just create
the patch as a file:

.. code-block:: sh

   $ svn diff > /tmp/repoze.who-my_cool_feature.patch

And then send or upload that file as an attachment:  mailers and web-browsers
are nearly as good at leaving attachments alone as they are at destroying
sensitive inline text!

For ``repoze`` projects, the default place to submit patches is to the
`repoze tracker <http://bugs.repoze.org/>`_.  You will need to register for
an account, but you should then be able to create a new issue and upload
your patch file to it.  Good titles, descriptions, and tags on the issue
should help it get the attention of the right maintainer for the project:
if you don't hear back fairly quickly, try asking on the `repoze IRC
channel <irc://freenode.net/#repoze>`_, or follow up to the `repoze-dev
mailing list <mailto:repoze-dev@lists.repoze.org>`_.


.. _svn-write-access:

How-to: Get a writable Subversion checkout
------------------------------------------

The Repoze project grants write access to the Subversion repository to
developers who are active with the project.  To obtain write access to the
Repoze subversion repository, you must sign a contributor's agreement.
This agreement is available in two varieties:

- `Form for electronic signature <http://repoze.org/signable.txt>`_
  Instructions for signing and remitting are included in the agreement.

- `Form for physical signature <http://repoze.org/contributor.pdf>`_
  A physically signed agreement should be mailed to the address below or
  faxed to (United States) 540 479 1706

.. code-block:: text

    Agendaless Consulting, Inc
    20 Pawnee Drive
    Fredericksburg, VA 22401
    U.S.A.

Once you have submitted the form, a core developer will respond in e-mail
requesting your SSH public key.  Once that key is uploaded, you can make
a writable checkout from Subversion:

.. code-block:: sh

   $ svn co svn+ssh://repoze@svn.repoze.org/svn/repoze.who/trunk who-trunk

and then commit your changes back directly:

.. code-block:: sh

   $ svn commit -m "Add new feature."
