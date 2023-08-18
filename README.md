# action-deploy2ssh
> An action for deploy to ssh.

## usage
1. set secret `gh secret set -f ~/.aliyun/.env.kubebio`
2. use below workflow
```yml
name: deploy2cos workflow
on:
  push:
    branches: master

jobs:
  Release:
    name: Release
    runs-on: ubuntu-latest
    env:
      COS_YML: ${{ secrets.COS_YML }}


    if: contains(github.event.head_commit.message, '__@production__')
    steps:
      - name: All in one
        uses: afeiship/action-deploy2ssh@master
        with:
          build_dist: "build"
          oss_bucket: cos://your-cos/test/

      - name: Debug
        run: |
          printenv
```

## for multiple envs

```yml
name: moban-admin workflow for AliyunOSS
on: [push]
jobs:
  beta:
    runs-on: ubuntu-latest
    env:
      COS_YML: ${{ secrets.COS_YML }}

    if: contains(github.event.head_commit.message, '__@beta__')
    steps:
      - name: All in one for beta
        uses: afeiship/action-deploy2ssh@master
        with:
          build_dist: "dist"
          oss_bucket: cos://your-cos/beta/

  production:
    runs-on: ubuntu-latest
    env:
      COS_YML: ${{ secrets.COS_YML }}

    if: contains(github.event.head_commit.message, '__@production__')
    steps:
      - name: All in one for production
        uses: afeiship/action-deploy2ssh@master
        with:
          build_dist: "dist"
          oss_bucket: cos://your-cos/production/
```