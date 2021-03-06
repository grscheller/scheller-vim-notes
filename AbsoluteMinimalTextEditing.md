# Absolute Minimum One Needs to Know

Let's say you've ssh'ed to some server which only has
vi or vim installed.  No emacs, no nano.  You only have
one quick edit to do, so it is not worth installing your
favorite editor.  Here is some critical info you need to
know in order to sub-marginally accomplish your task.

## How to exit vi/vim/nvim

You invoked vi via

```
    $ vi /etc/hosts
```

You can move around with the arrow keys but when you try typing
stuff weird things happen.  You try to exit, but nothing works.
Damn it, CTRL-C does not even work!

To get out,

```
    <Esc>:q!<CR>
```

The ESC key brought you back (or left you in) "command mode".
In vim/nvim this mode is known as *normal mode*.  The `:` key
put you into "command-line mode", known as *command mode*
in vim/nvim.  You are now entering text on the last line of
the terminal which begins with a `:` prompt.  The `q!`
"command-line mode" vi command quits the editor without
saving any changes.  The `<CR>` key, also known as `<Return>`,
`<Enter>` or `<EOL>` key, submits the command ending your session.

From now on, we'll refer to these modes by their vim/nvim names.

## The 3 main modes

* *normal mode*: Used to navigate file and issue "visual interface" (vi) commands
* *insert mode*: Used to type text into the file
* *command mode*: Used to issue "line editor" (ex) commands

If in either *insert mode* or *command mode*, `<Esc>` will take
you to *normal mode*.

## Minimal command set common to vi, vim, and nvim

Here are a minimal common subset of commands for vi, vim, and nvim.

### Cursor movement in *Normal Mode*

*Normal mode* is the default mode you are put in when the editor
is started.  Hitting `<Esc>` while in *insert mode* or *command mode*
will put you into *normal mode*.

| Command  | Description                                 |
|:--------:|:------------------------------------------- |
| `h`      | move cursor one character to left           |
| `l`      | move cursor one character to right          |
| `j`      | move cursor one line directly down          |
| `k`      | move cursor one line directly up            |
| `w`      | move forward to beginning next word         |
| `b`      | move back to beginning of word cursor is on |
| `e`      | move forward to end of of word cursor is on |
| `$`      | move cursor to end of line                  |
| `0`      | move cursor to start of line                |

In vi/vim/nvim, depending on terminal type, arrow keys will
also work to navigate the file in the editing buffer.

### Commands to insert or manipulate text

These *normal mode* commands take vim to *insert mode*.
To return to *normal mode*, type `<Esc>`.

| Command | Description                                                |
|:-------:|:---------------------------------------------------------- |
| `i`     | insert text before character cursor is on                  |
| `a`     | insert text after character cursor is on                   |
| `A`     | insert text at end of line                                 |
| `o`     | open new line after current line in insert text            |
| `O`     | open new line before current line in insert text           |
| `3cw`   | change next three words                                    |
| `2c3w`  | change next six words                                      |

### Changing text and/or interacting with "the buffer" in *Normal Mode*

Buffer is older vi jargon for what is now
called the default register in vim/nvim.

| Command   | Description                                            |
|:---------:|:------------------------------------------------------ |
| `dd`      | delete line and put in default register (cut)          |
| `5dd`     | delete 5 lines and put in default register             |
| `d$`      | delete to end of line, put in default register         |
| `d0`      | delete to beginning of line, put in default register   |
| `yy`      | yank line to default register (copy)                   |
| `x`       | delete character under cursor, put in default register |
| `r<char>` | change current character cursor highlights to `<char>` |
| `p`       | paste default register contents "after"                |
| `P`       | paste default register contents "before"               |
| `J`       | join curent & next line, insert spaces as needed       |

What "before" or "after" mean depends on what is in the default register.

### *Insert Mode*

The whole vi paradigm is that you do all navigation in *normal mode*
and type text into the file buffer in *insert mode*.  You return
to *normal mode* by pressing the `<Esc>` key.

With vim/nvim, in *insert mode*, you can navigate through the file with
the arrow keys.  You cannot navigate this way with vi.

### *Command Mode*

Use the `:` command to enter *command mode*.  The
cursor jumps down to the bottom of the terminal window
and prompts you with `:`.

| Command             | Description                                            |
|:------------------- |:------------------------------------------------------ |
| `:w`                | write to disk file being edited                        |
| `:w file`           | write to file, still editing original file             |
| `:q`                | quit editing, will warn about unsaved changes          |
| `:wq`               | write to disk, then quit                               |
| `:q!`               | quit without saving unsaved changes                    |
| `:n`                | edit next buffer typically next file on command line   |
| `:prev`             | edit previous buffer                                   |
| `:42`               | move cursor to beginning of line 42                    |
| `:#`                | give line number of current line cursor is on          |
| `:s/foo/bar/`       | substitute first instance of foo with bar              |
| `:s/foo/bar/g`      | substitute all instances of foo with bar               |
| `:17,42s/foo/bar/g` | substitute all foo with bar, lines 17 to 42            |
| `:/dog/`            | jump next line with `dog` in it (first non-whitespace) |
| `/dog`              | jump to next instance of `dog` in file                 |

Entering `<CR>` will cause the above commands to be executed and return you
to *normal mode*.  Hitting `<Esc>` instead will punt on running the command
and return you to *normal mode*.

### Repeating commands in *Normal Mode*

| Command | Description                                |
|:-------:|:------------------------------------------ |
| `.`     | repeat the last command which changed text |

This repeats the last *normal mode* command used which changed text.
It does not repeat *command mode* commands.

## POSIX shell command line editing mode

The non-multiline *normal mode* commands above
also apply to POSIX shell when in vi cmdline
editing mode.  By default, Bash uses emacs editing
mode.  Put `set -o vi` in your `~/.bashrc` file to
enable vi editing mode.

* When the prompt is printed you are in *insert mode*
* Pressing `<Esc>` puts you in *normal mode* with a one line view
* Pressing `k` takes you back through your command line history
* Pressing `j` takes you forward through your command line history
* Pressing `h` and `l` moves you forward and back on the command line
* The `f`, `t`, `F`, `T`, `;`, `,` commands, covered later, are useful

---

| [Home][1] | next: [Basic Text Editing][2] |

[1]: README.md
[2]: BasicTextEditing.md
