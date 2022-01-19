infinispan_cache
================

Configures [Infinispan](https://infinispan.org/) or [Red Hat DataGrid](https://www.redhat.com/en/technologies/jboss-middleware/data-grid) caches at runtime.

This role allows to deploy a cache configuration from a provided xml file, or using ansible configuration, via infinispan hotrod or rest api; the configuration
happens at runtime, and will be distributed to all nodes of the cluster, so it is executed with the `run_once` attribute. To deploy cache configuration statically
in the infinispan.xml server configuration, use the `infinispan` role instead.

For more details, refer to:
* [Configuring Infinispan Caches - 3.1 Declarative cache configuration](https://infinispan.org/docs/stable/titles/configuring/configuring.html#declarative-cache-configuration_cache-configuration)
* [Configuring Infinispan Caches - 3.3 Creating remote caches](https://infinispan.org/docs/stable/titles/configuring/configuring.html#creating-remote-caches)


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


where:

* `cache_xml` is an xml cache declaration validating against infinispan cache [xsd](https://infinispan.org/schemas/infinispan-config-12.1.xsd).
* `cache_config` is a yaml dict for templating the cache xml, refer to the [templates](templates/) directory for accepted variables.


Role Variables
--------------

The following are a set of required variables for the role:

| Variable | Description |
|:---------|:------------|
|`deployer_password`| Password for the user performing the API call |


Dependencies
------------

The role has currently no other dependency. Python _lxml_ and _jmespath_ libraries are needed on the host that executes this module.
To install, from the collection root directory, run:

    pip install -r requirements.txt


Example Playbook
----------------

The following are example playbooks that make use of the role to create Infinispan caches:

```yaml
- hosts: [...]
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

```yaml
- hosts: [...]
      collections:
        - middleware_automation.infinispan
      tasks:
       - name: Include Infinispan cache role
         include_role:
           name: infinispan_cache
         vars:
           deployer_password: changeme
           cache_xml: >
             <local-cache name="testcachexml" statistics="true">
               <encoding media-type="application/x-protostream"/>
             </local-cache>
```


```yaml
- hosts: [...]
      collections:
        - middleware_automation.infinispan
      tasks:
       - name: "infinispan cache role (yml)"
         include_role:
           name: ../../roles/infinispan_cache
         vars:
           deployer_user: "supervisor"
           deployer_password: "itsme"
           cache_config:
             name: configuredcache
             template: replicated
             mode: ASYNC
             unreliable_return_values: true
             transaction_mode: NONE
             transaction_locking: PESSIMISTIC
             memory_max_size: '100MB'
             memory_when_full: 'REMOVE'
             expiration_lifespan: 60000
             expiration_max_idle: 10000
             persistence: false
             indexing: false
```


License
-------

Apache License 2.0


Author Information
------------------

* [Guido Grazioli](https://github.com/guidograzioli)
