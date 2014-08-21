# How to contribute?

## Goals

- clean, easy to read/understand, linear history
- work in feature-branches
- use of Pull Request to get code review (if possible)
- intermediary branch (`develop`) to let `master` clean in production
- don't be dependant of an external tool like github or similar


## Git workflow

### Available branches

- `master`: the one in production
- `develop`: the one used to create feature-branches
- `<dev shortname>-<ticket number>-<very short description>`: feature branches, where all magic happens

### Workflow

First you need to create a local `develop` branch tracking the remote `develop` one:

```bash
git checkout -b develop origin/develop
```

Now you need to work on ticket #123.

```bash
# Create feature branch from up-to-date develop branch
git checkout develop
git pull
git checkout -b loicm-123-explain_gitworkflow
```

Work in this branch. Code, commit, code, commit as many time as needed.

When your work is ready, you want to prepare your branch for a Pull Request:

```bash
# Be sure you're still up-to-date with remote develop branch
git pull --rebase origin develop

# Reset your work so it's uncommited and staged
git reset --soft develop

# You can now commit your work in one commit with a beautiful commit message (see below)
git ci -m "ref #123: Add explanation of the git workflow"

# Push your branch to remote so other developers can see it
git push origin loicm-123-explain_gitworkflow
```

Then ask for a review via a PR (whatever tool you use: github, gitlab, bitbucket…)

When review is OK, it's time to merge your work on `develop` branch.

```bash
# Switch to develop branch and be sure it's up-to-date with remote and with master
git checkout develop
git pull
git pull --rebase origin master

# Then merge your feature-branch or let the reviewer doing it (let the default merge commit message)
git merge --no-ff loicm-123-explain_gitworkflow

# And push to remote
git push origin develop
```

Get your work in production (ie: on `master` branch)

```bash
git checkout master
git pull
git pull --rebase origin develop
git push origin master
```


## Commit messages

Everything has to be written in english.

Format should be:

```
<keyword> #<ticket number>: <Short message>

<Long message with multiple lines if needed>
```

`<keyword>` are:

- `fix`: when ticket is a bug and the commit fix it
- `ref`: for every other ticket

`<Short message>` is:

-  the ticket title or;
-  a simple phrase as simple and explicit as possible

We can add some context, for example:

```
Improve UI - lorem ipsum…
Add feature - lorem ipsum…
```

Your commit may not be related to a ticket: still keep good habits for your `<Short message>` and `<Long message>`.   
It should be easy for the others to understand what your commit brings to the project.


### Example

```
ref #123: Add feature - "forget password"

New 'password' controller dealing with the password recovery process

- 1 action to send a recovery email
- 1 action to allow input of new password (after clicking on link in the email just above)

Email content is configurable from BackOffice under "Config > Emails".
Email is send in HTML format.
```

## Useful links

(Mostly in French)

- [Configuration git](http://www.git-attitude.fr/2013/04/03/configuration-git/) (in French)
- [Configuration du prompt](http://www.git-attitude.fr/2013/05/22/prompt-git-qui-dechire/) (in French)
- [Git flow](http://danielkummer.github.io/git-flow-cheatsheet/)
- [Bien utiliser git merge et rebase](http://www.git-attitude.fr/2014/05/04/bien-utiliser-git-merge-et-rebase/) (in French)
- [Rebase](http://git-scm.com/book/fr/Les-branches-avec-Git-Rebaser)

