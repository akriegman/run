# run
Every build system has a different approach to handling repetitive tasks. With `make` each task would become a different recipe. With `npm` you would use `npm run`. With `cargo` the most common tasks are a subcommand. But then say you have an uncommon thing you need to do a lot, or you need to pass an extra argument to `cargo run` every time, then `cargo` can't help you with that. So I often find myself creating a `makefile` for my Rust projects. But then if I want to be able to pass arguments to the recipes, `make` doesn't allow for that. The whole thing is a big mess.

`run` is intended to be a more unified solution to the common scenario of "I have some tasks that I want to run often in this directory". The idea is that you write your tasks as regular bash functions in a file named `runfile` in the directory where you plan to run them. Then you use `run` to run tasks from your runfile. If you execute `run` with no arguments then it runs the task called `run`, like `make` does with the first recipe. `run` also lets you pass arguments to your tasks.

## Installation

`run` is a 12 line bash script. Installation is easy, you can just copy and paste the script into a file on your path. This command will do it for you:
```bash
curl https://raw.githubusercontent.com/akriegman/run/main/run >~/bin/run ; chmod +x ~/bin/run
```
Or, if you have a project with a runfile but you don't have `run` installed, you just run the tasks as  ordinary bash functions, for example:
```bash
$ . runfile
$ run
```
This has the disadvantage of polluting your bash session.

## Example
Here's an example `runfile` from a project of mine: https://github.com/akriegman/electro/blob/main/runfile

## Notes

Including a hashbang `#!/bin/bash` on the first line of your `runfile` may help your editor recognize your `runfile` as bash for syntax highlighting and formatting. This hashbang will not be used with either invocation method, however.

Many people prefer `Makefile` over `makefile` because it appears higher in most file explorers. As a terminal user, this doesn't help me as `ls` mixes capital and lowercase files. Further, `Makefile` is harder to type and I find `makefile` more aesthetic. For these reasons I prefer lowercase, and I guess for simplicity `run` only acknowledges `runfile`s, not `Runfile`s.

https://github.com/TekWizely/run and https://github.com/simpzan/run had the same idea as me with the same name. My version is the most minimal of the three, but if you want more features then check them out.
