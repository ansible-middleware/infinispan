infinispan
==========

Install [Infinispan](https://infinispan.org/) or [Red Hat DataGrid](https://www.redhat.com/en/technologies/jboss-middleware/data-grid) server configurations.


Role Defaults
-------------

| Variable | Description | Default |
|:---------|:------------|:---------|
|`infinispan_keycloak_caches`| Creates remote caches for keycloak | `False` |
|`override_jdg_port`| Alternate port for the service | `11222` |
|`override_jdg_jgroups_port`| Alternate port for the jgroups cluster | `7800` |
|`override_jdg_bind_addr`| Alternate bind address for the daemon | `localhost` |


Role Variables
--------------

The following are a set of required variables for the role:

| Variable | Description |
|:---------|:------------|
|`supervisor_password`| Password for the administration console user account |
|`infinispan_users`| List of _user definitions_ to create |

Sample _user definition_ format:

```yaml
infinispan_users:
  - { name: 'testuser1', password: 'test', roles: 'observer' }
  - { name: 'testuser2', password: 'test', roles: 'application' }
```


Dependencies
------------

The roles depends on the redhat_csp_download roles of [middleware_automation.redhat_csp_download](https://github.com/ansible-middleware/redhat-csp-download) collection.


Example Playbook
----------------

The following is an example playbook that makes use of the role to install Infinispan

```yaml
---
- hosts: ...
      collections:
        - middleware_automation.infinispan
      tasks:
        - name: Include Infinispan role
          include_role:
            name: infinispan
          vars:
            supervisor_password: "changeme"
            infinispan_users: []
```

License
-------

Apache License 2.0

Author Information
------------------

* [Guido Grazioli](https://github.com/guidograzioli)
* [Romain Pelisse](https://github.com/rpelisse)
* [Matthew Fernandez](https://github.com/l3acon)