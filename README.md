# action-deploy2ssh
> An action for deploy to ssh.

## usage
<!-- ~/.dotfiles/.servers/.env.dicfree-server -->
1. set secret `gh secret set -f ~/.dotfiles/.servers/.env.dicfree-server`
2. use below workflow
```yml
name: deploy2ssh workflow
on:
  push:
    branches: main

jobs:
  Release:
    name: Release
    runs-on: ubuntu-latest
    env:
      SSH_HOST: ${{ secrets.SSH_HOST }}
      SSH_USERNAME: ${{ secrets.SSH_USERNAME }}
      SSH_PASSWORD: ${{ secrets.SSH_PASSWORD }}

    if: contains(github.event.head_commit.message, '__@production__')
    steps:
      - uses: actions/checkout@v3
      - name: copy file via ssh password
        uses: afeiship/action-deploy2ssh@main
        with:
          build_dist: app
          oss_bucket: /mnt/vdb/wms.dicfree.cn/frontend/beta/
```

## for multiple envs
> tobe done.
```yml
```