<h1 align=center><code>just</code></h1>
<div align=center>
  <a href=https://crates.io/crates/just>
    <img src=https://img.shields.io/crates/v/just.svg alt="crates.io version">
  </a>
  <a href=https://github.com/casey/just/actions/workflows/ci.yaml>
    <img src=https://github.com/casey/just/actions/workflows/ci.yaml/badge.svg alt="build status">
  </a>
  <a href=https://github.com/casey/just/releases>
    <img src=https://img.shields.io/github/downloads/casey/just/total.svg alt=downloads>
  </a>
  <a href=https://discord.gg/ezYScXR>
    <img src=https://img.shields.io/discord/695580069837406228?logo=discord alt="chat on discord">
  </a>
  <a href=mailto:casey@rodarmor.com?subject=Thanks%20for%20Just!>
    <img src=https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg alt="say thanks">
  </a>
</div>
<br>

`just` is a handy way to save and run project-specific commands.

This readme is also available as a [book](https://just.systems/man/en/). The
book reflects the latest release, whereas the
[readme on GitHub](https://github.com/casey/just/blob/master/README.md)
reflects latest master.

(中文文档在 [这里](https://github.com/casey/just/blob/master/README.中文.md),
快看过来!)

Commands, called recipes, are stored in a file called `justfile` with syntax
inspired by `make`:

![screenshot](https://raw.githubusercontent.com/casey/just/master/etc/screenshot.png)

You can then run them with `just RECIPE`:

````console
$ just test-all
cc *.c -o main
./test --all
Yay, all your tests passed!
````

`just` has a ton of useful features, and many improvements over `make`:

* `just` is a command runner, not a build system, so it avoids much of
  [`make`’s complexity and idiosyncrasies](what-are-the-idiosyncrasies-of-make-that-just-avoids.html).
  No need for `.PHONY` recipes!

* Linux, macOS, Windows, and other reasonable unixes are supported with no
  additional dependencies. (Although if your system doesn’t have an `sh`,
  you’ll need to [choose a different shell](settings.html#shell).)

* Errors are specific and informative, and syntax errors are reported along
  with their source context.

* Recipes can accept [command line arguments](recipe-parameters.html).

* Wherever possible, errors are resolved statically. Unknown recipes and
  circular dependencies are reported before anything runs.

* `just` [loads `.env` files](settings.html#dotenv-settings), making it easy to populate
  environment variables.

* Recipes can be [listed from the command line](listing-available-recipes.html).

* Command line completion scripts are
  [available for most popular shells](shell-completion-scripts.html).

* Recipes can be written in
  [arbitrary languages](shebang-recipes.html), like Python or Node.js.

* `just` can be invoked from any subdirectory, not just the directory that
  contains the `justfile`.

* And [much more](https://just.systems/man/en/)!

If you need help with `just`, please feel free to open an issue or ping me on
[Discord](https://discord.gg/ezYScXR). Feature requests and bug reports are
always welcome!