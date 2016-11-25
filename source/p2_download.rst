Obtaining the Source
====================

Before you can start making changes to the manual, you must:

- ``Fork`` the repository on GitHub;
- ``Pull`` the fork down to your computer;
- Configure git;
- Make your changes or additions;
- Commit the changes to your local repository;
- ``Push`` the changes to your forked repository;
- Create a ``pull`` request to me;

At this point, after I've merged your changes, you can either:

- Delete your fork; or;
- Keep it, and keep it in sync with mine.

.. Note:: The following assumes that you are fully up to date with installing all the required software detailed in the previous part of the book.


Forking the Repository
----------------------

Forking the main repository is simple. 

- Go to the `repository on GitHub <https://github.com/NormanDunbar/SuperBASIC-Manual>`__\ .
- Click on the ``Fork`` button at the top of the screen, on the right:

  ..  image:: images\Fork.png
      :align: center
      :alt: Image showing how to fork a repository in GitHub.

- If you are a member of an organisation as well as being an individual, you will be prompted to select a location. Choose whichever one applies.
- That's it. After a while, the repository will show up in your list of repositories.
        

Pull the Source
---------------


Configure Git
-------------


Edit the Source
---------------


Commit Your Changes Locally
---------------------------


Push Changes Back to GitHub
---------------------------


Create a Pull Request
---------------------


Delete Your Fork
----------------


Keeping Your Fork in Sync
-------------------------

If you think that you might do some more work on the manual at a later date, then why not keep a hold of your forked repository and update it as and when required to sync it with the main repository. It's not all that difficult at all.


Add an Upstream Remote
~~~~~~~~~~~~~~~~~~~~~~

The first and most important thing to do is add the main repository as a ``remote``. Don't worry about the term ``remote`` it's just a name as far as we need to be bothered!

Open up a command line session and execute the following commands::

    cd SuperBASIC-Manual
    git remote add upstream https://github.com/NormanDunbar/SuperBASIC-Manual.git
    
That's it! You can check that it worked as follows::

    git remote -v
    
The output should resemble the following::

    upstream https://github.com/NormanDunbar/SuperBASIC-Manual.git (fetch)
    upstream https://github.com/NormanDunbar/SuperBASIC-Manual.git (push)
    
    
Sync Your Fork
~~~~~~~~~~~~~~

Your fork may be behind the upstream repository, as the main one is now known in your development system, so before making any changes, bring it up to date. You need to be sure that all your changes are pushed to your repository first though.

The following commands will commit and push your latest work back to your fork. This will not be necessary if you have not done any work since the last push.

::

    git status
    git add ....
    git commit -m "Pushing my latest work before syncing from upstream."
    git push

Now that your fork is up to date will your local work, you should fetch the upstream/master branch. Doing this will also cause your development area to do a ``git checkout upstream/master`` command, so you will need to checkout your master branch afterwards::

    git fetch upstream
    git checkout master
    git merge upstream/master
    git push

That's the master branch taken care of. We don't however, do our work in that branch, we use working, so we also need to be sure that we have synced our working branch with upstream too::
    
    git fetch upstream/working
    git checkout working
    git merge upstream/working
    git push

Now we are up to date *locally* and our fork is at the same commit point as the upstream repository. We can go to work. You will:

- Make changes and test in the working branch;
- ``Commit`` those changes and ``push`` them to your fork;
- ``Check out`` your master branch
- ``Merge`` the changes from your working branch;
- ``Push`` those to your fork;
- Raise a ``pull`` request in the normal manner.

All of these steps are described in detail, above.
    
    
    