Digital Ocean Bootstrap
=======================

Use the Digital Ocean API v2 to create and Droplets using Ansible 2.0:

### Table of contents
- [Overview](#Overview)
- [How to use this repo](#features)
- [Requirements](#requirements)
- [Installation](#Installation)

## How to use this repo?

There are currently two main playbooks to launch and destroy Digital Ocean droplets with Ansible. Once the project is installed, the playbooks can be run as follows.

### launch.yml
Launch and provision a new server on Digital Ocean.
```shell
ansible-playbook launch.yml -c local
```

### destroy.yml
Destroys a server on Digital Ocean.
```shell
ansible-playbook destroy.yml -c local
```

## Requirements

* Install Ansible

Linux, Mac, Windows, Fedora

## Installation

* Install dependencies with pip

```python
pip install requirements.txt
```

* Make sure your python path is configured correctly.

```shell
#for example when using OSX homebrew
export PYTHONPATH=/usr/local/lib/python2.7/site-packages
```

* Create the `vars.yml`

Copy the `vars.yml.dist` and rename the file to `vars.yml`. Please note there is a `.gitignore` directive to exclude the `vars.yml` file so be sure the naming convention is followed if there are any private variables.

## Authentication

There are two ways to authenticate with Digital Ocean

#### A) Set the DO_API_TOKEN

Set the `DO_API_TOKEN` and this will avoid having to set the authentication token in `vars.yml`.

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

#### Variables

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

The following variables are available:
- `do_api_token`
    * A string representing the image to use when creating a new droplet. It defaults to `ubuntu-14-04-x64`.
    List available images with the `digitalocean-list images $DIGITAL_OCEAN_TOKEN` command. Like when using the DigitalOcean API directly, [it can be an image ID or slug](https://developers.digitalocean.com/documentation/v2/#create-a-new-droplet).
- `do_ssh_name`
    * A boolean flag indicating whether to enable IPv6
- `do_region`
    * A string representing the region to create the new droplet in. It defaults to `nyc2`. List available regions with the `digitalocean-list regions $DIGITAL_OCEAN_TOKEN` command.
- `do_size`
    * A string representing the size to use when creating a new droplet (e.g. `1gb`). It defaults to `512mb`. List available sizes with the `digitalocean-list sizes $DIGITAL_OCEAN_TOKEN` command.

### Resources

#### Digital Ocean API

Create a new API key on the [API access page](https://cloud.digitalocean.com/api_access).
Only API v2 is supported currently by Ansible.
Add the client_id and api_key to `vars.yml`. @todo modify for v2
