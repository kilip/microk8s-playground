Olympus Cluster
====
Highly opinionated a single [k3s](https://k3s.io) cluster with [Ansible](https://www.ansible.com) and [Terraform](https://www.terraform.io) backed by [Flux](https://toolkit.fluxcd.io/) and [SOPS](https://toolkit.fluxcd.io/guides/mozilla-sops/).

# TL;DR

### Configuration
```sh
task init
task precommit:init
task precommit:update
cp .config.sample.env .config.env
cp .envrc.dist.env.envrc
```
Start configure ```.envrc``` and ```.config.env``` check configuration with:
```sh
task verify
```
And runs this command after succeeded:
```sh
task configure
```

### Install
#### prepare nodes step:
```sh
task an:init
task an:list
task an:ping

# start preparing your nodes
task an:prepare

# run this command if ansible not rebooting the nodes:
task an:force-reboot
```

#### k3s install step:
```sh
task an:list
task an:ping
task an:install
```

#### cluster install:
```sh
# push your changes to github first
git add . -A
git commit  -am "initial commit"
git push

# start installation
task cl:label olympus/role=node_role
task cl:verify
task cl:install

# verify install
task cl:pods -- -n flux-system
```
