Puppet Agent
=========

Installs and configures the puppet agent on nodes.

Requirements
------------

A working puppet master.

Role Variables
--------------

Puppet agent configuration settings can be defined by overriding the default variable `puppet_agent_configuration`:

```yml
puppet_agent_configuration:
- main:
    certname: puppet-agent.localdomain
    server: "{{puppet_ca_master['server']}}"
- agent:
    report: true
    environment: production
```

Dependencies
------------

The **the-paulus.puppet** role is required by this as it uses the `puppet_ca_master['server']` variable.


```
ansible-galaxy install the-paulus.puppet
```

Example Playbook
----------------

Inventory example:
```
[puppetmasters]
puppet

[webservers]
www[1-3]

[loadbalancers]
lb[1-2]

[puppets]
www[1-3]
lb[1-2]
```
Playbook examples:
```yml
- hosts: all:!puppetmasters
  roles:
     - the-paulus.puppet-agent

- hosts: puppets
  roles:
    - the-paulus.puppet-agent
```

License
-------

BSD
