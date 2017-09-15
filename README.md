# Ansible scripts to provision and deploy Odoo

These are [Ansible](http://docs.ansible.com/ansible/) playbooks (scripts) for managing an [Odoo](https://github.com/odoo/odoo) server.

You can create a local container instance with LXC using the `lxc/lxc-create.sh` script.
Run:

`./lxc/lxc-create.sh -n odoo-dev -t ubuntu -r xenial -h local.ofn.org`

## Playbooks

### Provision
`provision.yml` - Install and configure all required software on the server.

- Install common packages
- Install PostgreSQL database and create a user
- Install NodeJS and LESS

### Deploy
`deploy.yml` - Deploy source code from Odoo Nightly and install Python requirements.

- Install and create VirtualEnv
- Ansistrano deploy:
  - Download the source code
  - Before link task: Build
  - Before link task: Install requirements.txt
- Add systemd service

## Requirements

You will need Ansible on your machine to run the playbooks.
These playbooks will install the PostgreSQL database and Python virtualenv to manage python packages. 

It has currently been tested on **Ubuntu 16.04 Xenial (64 bit)**.

If you like run the `lxc-create` script, you need install [LXC](https://linuxcontainers.org/).

## Development - Using LXC containers

You can need a local container to test your customizations.
`lxc/lxc-create.sh` script creates a container, gets IP address of the new container and creates a known host whit this IP address.

`./lxc/lxc-create.sh -n NAME -t TEMPLATE -r RELEASE -h HOST`

Arguments:

```
  -n --name: LXC container name. Ex.: my-cont"
  -t --template: LXC container template. Ex.: ubuntu"
  -r --release: LXC container release. Ex.: xenial"
  -h --host: LXC container host name. Ex.: local.lxc.org"
```

**Name and host are required.** Default template is Ubuntu and default release is Xenial (16.04 LTS)
