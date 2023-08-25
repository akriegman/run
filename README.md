# run
Every build system has a different approach to handling the tasks that you need to run often for your project. With `make` each task would become a different recipe. With `npm` you would use `npm run`. With `cargo` the most common tasks are a subcommand. But then say you have an uncommon thing you need to do a lot, or you need to pass an extra argument to `cargo run` every time, then `cargo` can't help you with that. So I often find myself creating a `makefile` for my Rust projects. But then if I want to be able to pass arguments to the recipes, `make` doesn't allow for that.

`run` is intended to be a more unified solution to the common scenario of "I have some tasks that I want to run often in this directory". The idea is that you write your tasks as regular bash functions in a file named `runfile` in the directory where you plan to run them. Then you use `run` to run tasks from your runfile. The tasks are ordinary bash, because `make` somehow has a language even worse than bash. Similar to `make`, if you execute `run` with no arguments then it runs the task called `all`. `run` also lets you pass arguments to your tasks.

`run` is a 9 line bash script. Installation is easy, you just copy and paste the script into a file on your path. Or just run this command:
```bash
curl https://raw.githubusercontent.com/akriegman/run/main/run >~/bin/run ; chmod +x ~/bin/run
```
Or, if you have a project with a runfile but you don't have `run` installed, you just run the tasks as  ordinary bash functions, for example:
```bash
$ . runfile
$ all
```
This has the disadvantage of poluting your bash session.

Many people prefer `Makefile` over `makefile` because it appears higher in most file explorers. As a terminal user, this doesn't help me as `ls` doesn't put all the capitalized files before the lowercase ones. Further, `Makefile` is harder to type and uglier than `makefile`. For these reasons I prefer lowercase, and I guess for simplicity `run` only acknowledges `runfile`s, not `Runfile`s.
