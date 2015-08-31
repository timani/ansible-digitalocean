Digital Ocean Bootstrap
=======================

Bootstrap Digital Ocean droplets using Ansible to:

* Configure SSH key
* Launch a droplet
* Configure DNS domain
* Destroy droplet

Inspired by [hostmaster/ansible-digitalocean-bootstrap](https://github.com/hostmaster/ansible-digitalocean-bootstrap).

## Installation

* Install Ansible

Linux, Mac, Windows, Fedora

* Install dependencies with pip

```python
pip install requirements.txt
```

* Make sure your python path is configured correctly.

```shell
#for example when using OSX homebrew
export PYTHONPATH=/usr/local/lib/python2.7/site-packages
```

* Copy `vars.yml.dist` to `vars.yml`

Please note there is a `.gitignore` directive to exclude the `vars.yml` file so be sure the naming convention is followed if there are any private variables.

## Authentication

There are two ways to authenticate with Digital Ocean

#### A) Set the DO_API_TOKEN

Set the DO_API_TOKEN and this will avoid having to set the authentication token in `vars.yml`.

Two environment variables can be used, either the `DO_API_KEY` and `DO_API_TOKEN`. They both refer to the v2 token.

```shell
export DO_API_TOKEN=XXXX
```

#### B) Set the do_api_token in vars.yml

Uncomment and set the `do_api_token` in `vars.yml`

```ruby
# DO API settings
do_api_token: XXXX
```

## Configuration

Change the variables to your need. @todo list of variables

* Create the default hosts file (optional):

@todo this should local to the project

```shell
sudo echo "localhost ansible_connection=local" > /etc/ansible/hosts
```

## Variables

```ruby
# DO API settings
do_api_token: XXXX

# DO SSH key settings
do_ssh_name: ansible
do_ssh_pub_key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"

# DO droplet settings
do_region: 5 # AMS
do_size: 62 # 2 GB / 2 CPU
do_image: 9801950 # Ubuntu 14.04 x64

# Swap settings
swap_file_path: /mnt/1GB.swap
swap_file_size_kb: 1048576

# System user to create
ssh_user: "{{ lookup('env', 'USERNAME') }}"
ssh_groups: "sudo"
ssh_pub_key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
```

## Playbooks

### launch.yml
Launch and provision a new server on Digital Ocean.
```shell
ansible-playbook launch.yml
```

### destroy.yml
Destroys a server on Digital Ocean.
```shell
ansible-playbook destroy.yml
```

### Resources

#### Digital Ocean API

Create a new API key on the [API access page](https://cloud.digitalocean.com/api_access).
Only API v2 is supported currently by Ansible.
Add the client_id and api_key to `vars.yml`. @todo modify for v2
