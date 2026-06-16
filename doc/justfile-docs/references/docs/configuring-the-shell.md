### Configuring the Shell

There are a number of ways to configure the shell for shell recipes, which are
the default when a recipe does not start with a `#!` shebang. Their precedence,
from highest to lowest, is:

1. The `--shell` and `--shell-arg` command line options. Passing either of
   these will cause `just` to ignore any settings in the current justfile.
1. `set windows-shell := [...]`
1. `set windows-powershell` (deprecated)
1. `set shell := [...]`

Since `set windows-shell` has higher precedence than `set shell`, you can use
`set windows-shell` to pick a shell on Windows, and `set shell` to pick a shell
for all other platforms.