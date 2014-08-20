# How to contribute?

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

# Then merge your feature-branch
git merge loicm-123-explain_gitworkflow

# And push to remote
git push
```

Get your work in production (ie: on `master` branch)

```bash
git checkout master
git pull
git pull --rebase origin develop
git push
```

## Commit messages

Everything has to be written in english.

Format must be:

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

### Example

```
ref #123: Add feature - "forget password"

New 'password' controller dealing with the password recovery process

- 1 action to send a recovery email
- 1 action to allow input of new password (after clicking on link in the email just above)

Email content is configurable from BackOffice under "Config > Emails".
Email is send in HTML format.
```