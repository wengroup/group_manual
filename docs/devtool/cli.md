(command:line:tool)=

# Command Line Tool

## Syntax

```
command [--option 1] [--option 2] <subcommand 1>
```

## Manual of a command

```
$ man <command>
# e.g.
$ man ls
```

## Help of a command

```
$ <command> --help
# e.g.
$ git --help
```

Some commands may have subcommands, you can get help for a subcommand as well.

```
$ <command> <subcommand> --help
# e.g.
$ git add --help
```

## Some useful commands

### `which`

Locate a program file in the user's path. For example,

```
$ which git
```

shows that the `git` command is from `/usr/bin/git`.

### `tldr`

`tldr` simplify the beloved man pages with practical examples. For example,

```
$ tldr ls
```

gives

```
ls

List directory contents.
More information: <https://www.gnu.org/software/coreutils/ls>.

- List files one per line:
    ls -1

- List all files, including hidden files:
    ls -a
...

- Only list directories:
    ls -d */
```

```{note}
`tldr` needs to be installed before using. On macOS, do `$ brew install tldr`.
```

## More information
