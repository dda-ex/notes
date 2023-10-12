# How to use git

## Git init repository

### A new repo from an existing project

Say you’ve got an existing project that you want to start tracking with git.

- Go into the directory containing the project.
- Type `git init`.
- Type `git add` to add all of the relevant files.
- You’ll probably want to create a `.gitignore` file right away, to indicate all of the files you don’t want to track. Use `git add .gitignore`, too.
- Type `git commit`.

### Connect it to github

You’ve now got a local git repository. You can use git locally, like that, if you want. But if you want the thing to have a home on github, do the following.

- Go to [github](https://github.com).
- Log in to your account.
- Click the [new repository](https://github.com/new) button in the top-right. You’ll have an option there to initialize the repository with a README file, but I don’t.
- Click the “Create repository” button.

Now, follow the second set of instructions, “Push an existing repository…”

```
$ git remote add origin git@github.com:username/new_repo
$ git push -u origin master
```

Actually, the first line of the instructions will say

```
$ git remote add origin https://github.com/username/new_repo
```