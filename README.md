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

## Authentication

There are two ways to authenticate with Digital Ocean

#### A) Set the DO_API_TOKEN

Use the DO_API_TOKEN
```shell
export DO_API_TOKEN=XXXX
```

#### B) Set the do_api_token in

Copy vars.yml.dist to vars.yml and then edit the `do_api_token`. Please note there is a `.gitignore` directive to exclude the `vars.yml` file so be sure the naming convention is followed if there are any private variables.

Use the DO_API_TOKEN
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

### Digital Ocean configuration

Create a new API key on the [API access page](https://cloud.digitalocean.com/api_access).
Only API v2 is supported currently by Ansible.
Add the client_id and api_key to `vars.yml`. @todo modify for v2

## Playbooks

### launch.yml
Launch and provision a new server on Digital Ocean.

    ansible-playbook launch.yml

### destroy.yml
Destroys a server on Digital Ocean.

    ansible-playbook destroy.yml
