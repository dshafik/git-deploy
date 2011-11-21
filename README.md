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

## Example
```shell
$ git deploy create
[!!] You must use either --pre or --post.
Usage:
...

$ git deploy create --pre add-user-api-key.sql
Creating new deploy branch: deploy-davey-1
Creating new deploy file: pre/1-add-user-api-key.sql

$ git deploy create --post generate-api-keys.php
Using deploy branch: deploy-davey-1
Creating new deploy file: post/1-generate-api-keys.php

$ git deploy edit
Switched to branch 'deploy-davey-1'

$ git deploy build
[W] This branch looks like a deploy branch, please specify the branch to integrate into.
Usage:
...

$ git deploy build master
Reintegrating into: 'master'
Switched to branch 'master'
First, rewinding head to replay your work on top of it...
Fast-forwarded master to deploy-davey-1.

$ git deploy create --post clear-cache.php
Creating new deploy branch: deploy-davey-2
Creating new deploy file: post/1-clear-cache.php

$ git deploy create --post clear-templates.php
Using deploy branch: deploy-davey-2
Creating new deploy file: post/2-clear-templates.php

$ git deploy create --switch-branch --post update-templates.php # could also use -s
Using deploy branch: deploy-davey-2
Creating new deploy file: post/3-update-templates.php
Switched to branch 'deploy-davey-2'

$ git deploy ls-files --pre
[W] Currently on a deploy branch. File list will reflect changes that have not been reintegrated yet.
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/1/pre/1-add-user-api-key.sql

$ git deploy ls-files --post
[W] Currently on a deploy branch. File list will reflect changes that have not been reintegrated yet.
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/1/post/1-generate-api-keys.php
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/2/post/1-clear-cache.php
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/2/post/2-clear-templates.php
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/2/post/3-update-templates.php

$ git checkout master
Switched to branch 'master'

$ git deploy ls-files --pre
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/1/pre/1-add-user-api-key.sql

$ git deploy ls-files --post -t sql
[OK] Nothing to do!

$ git deploy ls-files --post -t php
/Library/WebServer/Documents/orchestra.io/orchestrate/deploy/1/post/1-generate-api-keys.php
```