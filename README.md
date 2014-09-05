course-info
===========

GitHub Repo for http://db.csail.mit.edu/6.830/



Course Setup
============

This will guide you through understanding how we will be using Git & GitHub for
this course.

## Contents

- [Learning Git](#learning-git)
- [Setting up GitHub](#setting-up-github)
- [Setting up Git](#setting-up-git)
- [Getting Newly Released Homework](#getting-newly-released-homework)
- [Submitting Your Homework](#submitting-your-homework)
- [Word of Caution](#word-of-caution)
- [Help!](#help)


## Learning Git

There are numerous guides on using Git that are available. They range from being
interactive ones to just text ones. Find one that works and experiment; making
mistakes and fixing them is a great way to learn. Here is a link to resources
that GitHub suggests:
[https://help.github.com/articles/what-are-other-good-resources-for-learning-git-and-github][resources]

If you have no experience with git a quick web-based try git tutorial will be helpful
[https://try.github.io/levels/1/challenges/1][trygit]

## Setting Up GitHub

Assuming you have a solid enough understanding of Git, it's time to get started
with GitHub.

0. Install git

1. If you don't already have an account, sign up for one here:
   [https://github.com/join][join].

2. Next you need to join the GitHub Organization that we've created for the
   course: [MIT-DB-Class]

   To join it, go to the [Registration](http://mitdbclass.heroku.com/)
   page and click the **Sign in with GitHub** button.

   This application uses OAuth and it will take you to GitHub where you will
   have to give your permission to join it.

3. Enter your NetID and you'll be automatically added to the organization and
   will have a repository created for you.

4. If for whatever reason you can't join the organization, contact a TA,
   and them him know.

5. You should now be apart of the [MIT-DB-Class] and should have access
   to a few different repositories.

   You should also now have a repository setup just for your homework solutions.
   This should be located in the MIT-DB-Class organization and be called
   `hw-answers-<NetID here>`.

   This is what you'll setup in the next section to allow you to write your
   homework answers and submit them.

If the above didn't work, contact one of the TAs to help you out.

### Installing git
The instructions are tested on bash/linux environments. Installing git should be a simple
apt-get / yum / etc install.  

Instructions for installing git on Linux, OSX, or Windows can be found at
[http://git-scm.com/book/en/Getting-Started-Installing-Git][installGit].

If you are using Eclipse, many versions come with git configured. The instructions will
be slightly different than the command line instructions listed but will work for any OS. 
Detailed instructions can
be found at [http://wiki.eclipse.org/EGit/User_Guide][egit] or [http://eclipsesource.com/blogs/tutorials/egit-tutorial/][egit tutorial]. 




## Setting Up Git

You should have Git installed and have joined the MIT-DB-Class organization from
the previous section.

1. The first thing we have to do is to clone the current homework repository by
   issuing the following commands onto the command line:

   ```bash
    $ git clone git@github.com:MIT-DB-Class/simple-db-hw.git
   ```

   This will make a complete replica of the homework repository locally. Now we
   are going to change it to point to your personal repository that was created
   for you in the previous section.

   If you get an error that looks like:

   ```bash
    Cloning into 'homework'...
    Permission denied (publickey).
    fatal: Could not read from remote repository.
    ```

    More likely the cause is that you just haven't finished setting up your
    GitHub account. You just need to [setup an SSH key][ssh-key] to allow
    pushing and pulling over SSH.

   Change your working path to your newly cloned repository:

   ```bash
    $ cd simple-db-hw/
   ```

2. By default the remote called `origin` is set to the location that you cloned
   the repository from. You should see the following:

   ```bash
    $ git remote -v
        origin git@github.com:MIT-DB-Class/simple-db-hw.git (fetch)
        origin git@github.com:MIT-DB-Class/simple-db-hw.git (push)
   ```

   We don't want that remote to be the origin, instead, we want to change it to
   point to your repository. To do that, issue the following command:

   ```bash
    $ git remote rename origin upstream
   ```

   And now you should see the following:

   ```bash
    $ git remote -v
        upstream git@github.com:MIT-DB-Class/simple-db-hw.git (fetch)
        upstream git@github.com:MIT-DB-Class/simple-db-hw.git (push)
   ```

3. Lastly we need to give your repository a new `origin` since it is lacking
   one. Issue the following but substituting your GitHub username in place:

   ```bash
    $ git remote add origin git@github.com:MIT-DB-Class/hw-answers-<NetID>.git
   ```

   But substitute in your own NetID of course.

   If you have an error that looks like the following:

   ```
  Could not rename config section 'remote.[old name]' to 'remote.[new name]'
   ```

   Or this error:
   
   ```
   fatal: remote origin already exists.
   ```
   
   This appears to happen to some depending on the version of Git they are using. To fix it,
   just issue the following command:
   
   ```bash
   $ git remote set-url origin git@github.com:MIT-DB-Class/hw-answers-<NetID>.git
   ```

   This solution was found from [StackOverflow](http://stackoverflow.com/a/2432799) thanks to
   [Cassidy Williams](https://github.com/cassidoo).

   For reference, your final `git remote -v` should look like following when its
   setup correctly:


   ```bash
    $ git remote -v
        upstream git@github.com:MIT-DB-Class/simple-db-hw.git (fetch)
        upstream git@github.com:MIT-DB-Class/simple-db-hw.git (push)
        origin git@github.com:MIT-DB-Class/hw-answers-<NetID>.git (fetch)
        origin git@github.com:MIT-DB-Class/hw-answers-<NetID>.git (push)
   ```

4. Let's test it out by doing a push of your master branch to GitHub by issuing
   the following:

   ```bash
    $ git push -u origin master
   ```

   You should see something like the following:

   ```
    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 294 bytes | 0 bytes/s, done.
    Total 3 (delta 2), reused 0 (delta 0)
    To git@github.com:MIT-DB-Class/hw-answers-joshuad.git   f726472..545a4f0  master -> master
   ```

5. That last command was a bit special and only needs to be ran the first time
   to setup the remote tracking branches. Now we should be able to just run `git
   push` without the arguments. Try it and you should get the following:

   ```bash
    $ git push
          Everything up-to-date
   ```

If you don't know Git that well, this probably seemed very arcane. Just keep
using Git and you'll keep understanding more and more.

## Getting Newly Released Homework

Pulling in homeworks that are released or previous homework solutions should be
easy just so long as you set up your repository based on the instructions from
the last section.

1. All new homework and previous homework solutions will be posted to the
   [homeworks](https://github.com/MIT-DB-Class/simple-db-hw) repository in the class
   organization.

   Check it periodically as well as BlackBoard's announcements for updates on
   when the new homeworks are released.

2. Once a homework is released, pulling in the changes should be fairly simple:

   ```bash
        $ git pull upstream master
   ```

   **OR** if you wish to be more explicit, you can `fetch` first and then
   `merge`:

   ```bash
        $ git fetch upstream
        $ git merge upstream/master
   ```

3. If you've followed the instructions in each homework, you should have no
   merge conflicts and everything should be peachy.

## Submitting Your Homework

The submission of your homework should be done by the date and time the homework
is due.

The criteria for your homework being submitted on time is that your code must be
**pushed** by the date and time. This means that if one of the TAs or the
instructor were to open up GitHub, they would be able to see your solutions on
the GitHub web page.

Just because your code has been commited on your local machine, that doens't
mean that it has been **submitted**; it needs to be on GitHub.

Here are a few guideline steps for a process of submitting your solutions:

1. Look at your current repository status.

   ```bash
   $ git status
   ```

2. Add your solutions (if they aren't already added and commited).

   ```bash
    $ git add my-solutions/
   ```

3. Commit your solutions.

   ```bash
   $ git commit
   ```

   Enter your commit message and then save and exit.

4. This is the most important part: **push** your solutions to GitHub.

   ```bash
   $ git push origin master
   ```

   Or, just `git push` for short.

5. The last thing that we strongly recommend you do is to go to the
   [MIT-DB-Class] organization page on GitHub to
   make sure that we can see your solutions.

   Just navigate to your repository and check that your latest commits are on
   GitHub.

6. The go and eat some cinnamon rolls; you've finished the homework
   assignment.

## Word of Caution

Git is a distributed version control system. This means everything operates
offline until a `git pull` or `git push`. This is a great feature.

The bad thing is that you may forget to `git push` your changes. This is why we
strongly, **strongly** suggest that you check GitHub to be sure that what you
want us to see matches up with what you expect.

## Help!

If at any point you need help with setting all this up. Feel free to reach out
to one of the TAs or instructor. Their contact information can be found in the
[syllabus][syllabus].

[join]: https://github.com/join
[resources]: https://help.github.com/articles/what-are-other-good-resources-for-learning-git-and-github
[ssh-key]: https://help.github.com/articles/generating-ssh-keys


This page and infrastructure for this page was taken from https://github.com/MIT-DB-Class/course-info/blob/master/guides/course-setup.md
and https://github.com/jdavis/github-plus-university
