# git-deploy

`git-deploy` is a tool for managing scripts and schemas associated with deploying updates to an application.

## Usage

```shell
$ git deploy
Usage:
------
create  [-s|--switch-branch]  --pre|--post  filename
  Create the {filename} deployment script in the current namespace. Will create a new namespace if necessary.

build / reintegrate  [reintegration branch]
  Freeze a namespace and reintegrate the changes.

edit
  Switch to the current deployment branch

ls-files  [-t|--type <extension>]  --pre|--post
```