Ansible Role Template
======================

A template role, adding Vagrant-testing support to the default Ansible-role
skeleton.

Ansible is a great tool, and trying things out with a virtual-machine is a
great way to learn, try things out, and test changes. But if you're trying
to learn Ansible and Vagrant/Virtualbox all at once, configuring a test-setup
just right can be a steep learning curve. This template demonstrates how
to set-up Vagrant to test your new Ansible role.


Notes
------
*Vagrantfile* sets up a testing virtual-machine, named `roletestingvm`.
This should be renamed to something sensible for your role so you can
recognise it if you have multiple VM's up and running, e.g. when running::

    vagrant global-status

... to remind yourself where all your RAM went.

The *ansible.cfg* file is not strictly necessary, but allows you to specify
a central location for storing roles, and also makes it possible to run
Ansible manually against your VM via the command line, rather than indirectly
by re-running Vagrant commands - this can speed up testing.
Note you will need to edit the `ssh_args` entry in *ansible.cfg*
so that the path matches the name of your VM.

For the testing playbook (*tests/test-roletemplate.yml*) to work correctly,
the relative import path has to match the folder-name you've checked out this
repository under. So e.g. for the unmodified template to run correctly, you
should clone it using:

    git clone git@github.com:timstaley/ansible-role-template.git roletemplate

Requirements
------------

[Vagrant-cachier](http://fgrehm.viewdocs.io/vagrant-cachier/) is recommended,
but optional.

This template includes an ansible-galaxy requirements file that pulls in
the [timstaley.base](https://github.com/timstaley/ansible-base) role, used
for configuring basic utilities on a fresh virtual-machine.
However, this is not a hard dependency, since users of a role may have their
own preferences as to e.g. exactly how `pip` gets installed.
To retrieve a copy of the roles listed in a requirements file, run::

    ansible-galaxy install -r requirements.txt

or

    ansible-galaxy install --force -r requirements.txt

to forcibly update old copies.

Note that *ansible.cfg* is configured such that roles will be installed under
*~/.ansible_roles*.

Role Variables
--------------

A description of the settable variables for this role should go here, including
any variables that are in defaults/main.yml, vars/main.yml, and any variables
that can/should be set via parameters to the role. Any variables that are read
from other roles and/or the global scope (ie. hostvars, group vars, etc.) should
be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in
regards to parameters that may need to be set for other roles, or variables that
are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers roles: - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a
website (HTML is not allowed).
