infinispan_cache
================

Configures [Infinispan](https://infinispan.org/) or [Red Hat DataGrid](https://www.redhat.com/en/technologies/jboss-middleware/data-grid) caches at runtime.

This role allow to deploy a cache configuration from a provided xml file, or using ansible configuration, via infinispan hotrod or rest api; the configuration
happens at runtime, and will be distributed to all nodes of the cluster, so it is executed with the `run_once` attribute.


Role Defaults
-------------

| Variable | Description | Default |
|:---------|:------------|:--------|
|`jdg_port`| Alternate port for the service | `11222` |
|`jdg_bind_addr`| Alternate bind address for the daemon | `localhost` |
|`jdg_tls`| Server REST API/hotrod have TLS enable | `False` |
|`deployer_user`| Username that performs the API call | `supervisor` |
|`cache_xml`| XML declaration for the cache to deploy as string | `None` |
|`cache_config`| dict object with configuration for the cache to deploy | `{}`, see below for specs |


Role Variables
--------------

The following are a set of required variables for the role:

| Variable | Description |
|:---------|:------------|
|`deployer_password`| Password for the user performing the API call |


Dependencies
------------

The role has currently no other dependency. _python-lxml_ is needed on the host that executes this module.


Example Playbook
----------------

The following is an example playbook that makes use of the role to install Infinispan

```yaml
---
- hosts: ...
      collections:
        - middleware_automation.infinispan
      tasks:
        - name: Include Infinispan cache role
          include_role:
            name: infinispan_cache
          vars:
            deployer_password: changeme
            cache_xml: "{{lookup('file', 'templates/my_cache.xml') }}"
```


License
-------

Apache License 2.0


Author Information
------------------

* [Guido Grazioli](https://github.com/guidograzioli)
