Ansible Role Template
=====================

A template for an Ansible-role, adding Vagrant-testing support to the 
default Ansible-role skeleton.

Ansible is a great tool, and trying things out with a virtual-machine is a
great way to learn, try things out, and test changes. But if you're trying
to learn Ansible and Vagrant/Virtualbox all at once, configuring a test-setup
just right can be a steep learning curve. This template demonstrates how
to set-up Vagrant to test your new Ansible role.


tl;dr:
------
**To get this template running:**

    git clone git@github.com:timstaley/ansible-role-template.git roletemplate
    
NB the local folder-name is important - that's how we refer back to the
role from the test-script, and so the folder-name should match the 
role-name.

    cd roletemplate/vagrant
    vagrant up

**To use this template for your own stand-alone role:**

    git clone git@github.com:timstaley/ansible-role-template.git myrolename
Now edit myrolename/tests/test-roletemplate.yml to change the role name 
to your own, accordingly. Then get started making changes to write your
own role.

Notes
------
*Vagrantfile* sets up a testing virtual-machine, 
by default named `roletestingvm` (see [Vagrantfile](vagrant/Vagrantfile)).
This should be renamed to something sensible for your role so you can
recognise it if you have multiple VM's up and running, e.g. when running::

    vagrant global-status

... to remind yourself where all your RAM went.

The *ansible.cfg* file tells ansible how to find the Vagrant SSH login 
details, which makes it easy to run Ansible manually against your 
VM via the command line, rather than indirectly
by re-running Vagrant commands - this can speed up testing.

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

    ansible-galaxy install -r requirements.yml

or

    ansible-galaxy install --force -r requirements.yml

to forcibly update old copies.

Note that *[ansible.cfg](vagrant/ansible.cfg)* is configured such that 
roles installed via Ansible Galaxy will be installed under 
*vagrant/galaxy_roles*.

When documenting a role, you should either specify expected 
pre-requisites (e.g. git) in the README, or if your dependencies 
are provided by a specific role then you should record it in the 
role metadata ([see docs](https://galaxy.ansible.com/intro#dependencies)).

License
-------

BSD