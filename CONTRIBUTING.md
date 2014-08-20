# How to contribute?

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