infinispan
==========

Install [Infinispan](https://infinispan.org/) or [Red Hat DataGrid](https://www.redhat.com/en/technologies/jboss-middleware/data-grid) server configurations.


Role Defaults
-------------

* Service configuration defaults

| Variable | Description | Default |
|:---------|:------------|:--------|
|`infinispan_port`| Alternate port for the service | `11222` |
|`infinispan_jgroups_port`| Alternate port for the jgroups cluster | `7800` |
|`infinispan_jgroups_relay_port`| Alternate port for the jgroups relaying cluster | `7801` |
|`infinispan_port_offset`| Optional port offset for colocated installations | `0` |
|`infinispan_nodename`| Instance name for service (ie. cluster node identifier) | `{{ inventory_hostname }}` |
|`infinispan_keycloak_persistence`| Enable persitence datasource for keycloak caches | `False` |
|`infinispan_service_user`| Posix account for the service installation | `ispn` |
|`infinispan_service_group`| Posix group for the service installation | `ispn` |
|`infinispan_logfile_format`| Main logfile format: FILE or JSON-FILE | `FILE` |
|`infinispan_logfile_root_level`| Root logging level: TRACE, DEBUG, INFO, WARN, ERROR | `INFO` |
|`infinispan_logfile_enable_audit`| Enable additional audit.log logfile | `True` |
|`infinispan_logfile_enable_hotrod_accesslog`| Enable additional hotrod-access.log | `False` |
|`infinispan_logfile_enable_rest_accesslog`| Enable additional rest-access.log | `False` |
|`infinispan_logfile_maxsize`| Max file size, triggers rotation | `100 MB` |
|`infinispan_default_realm_tls`| Enable TLS server certificate | `False` |
|`infinispan_keystore_path`| Path to keystore containing server identity certificate | `/etc/pki/java/cacerts` |
|`infinispan_keystore_password`| Keystore password | `changeit` |
|`infinispan_keystore_alias`| Alias for the certificate to load from keystore | `{{ inventory_hostname }}` |
|`infinispan_keystore_key_password`| Key passphrase for TLS server identity | `''`|
|`infinispan_keycloak_caches`| Creates remote caches for keycloak | `False` |
|`infinispan_jvm_package`| RHEL java package runtime | `java-11-openjdk-headless` |
|`infinispan_service_name`| Name of the systemd service unit, appended with `-{{infinispan_port_offset}}` when not 0 | `infinispan` |
|`infinispan_service_desc` | Description of the systemd service unit | `Infinispan` |
|`infinispan_service_restart_on_failure`| systemd restart-on-failure behavior activation | `True`` |
|`infinispan_service_startlimitintervalsec`| systemd StartLimitIntervalSec | `300` if `infinispan_service_restart_on_failure` else `` |
|`infinispan_service_startlimitburst`| systemd StartLimitBurst | `5` if `infinispan_service_restart_on_failure` else `` |
|`infinispan_service_restartsec`| systemd RestartSec | `10s` if `infinispan_service_restart_on_failure` else `` |
|`infinispan_resp_cache`| Name of the cache on which to enable the RESP protocol; if empty, disable RESP | `''` |


* Cluster configuration

| Variable | Description | Default |
|:---------|:------------|:--------|
|`infinispan_jgroups_relay`| Enable cross-DC relaying | `False` |
|`infinispan_jgroups_relay_sites`| List of site names for cross-DC relaying | `[]` |
|`infinispan_jgroups_relay_site`| Site the inventory host is in when cross-DC is enabled | `''` |
|`infinispan_jgroups_discovery`| Clustering discovery protocol, value from [`PING`,`TCPPING`,`JDBC_PING`] | `` |
|`infinispan_jgroups_iface` | The NIC name to be used for cluster IPv4 addresses (ie. 'eth0') | `default_ipv4` |
|`infinispan_jgroups_cluster_nodes`| List of node definitions for jgroups cluster, read below for the format | `[]` |

The `infinispan_jgroups_cluster_nodes` parameter, when empty, tell the collection to geenrate the list from the hosts variables in `ansible_play_hosts`;
otherwise, it can be passed-in using the following dictionary format:

```yaml
infinispan_jgroups_cluster_nodes:
  - address: 10.0.0.175
    inventory_host: '10.0.0.175[7800]'
    name: us-east-2-datagrid-1
    port: 7800
    site: us-east-2
    value: 'tcp://10.0.0.175:7800'
  - address: 10.0.0.179
    inventory_host: "10.0.0.179[7800]"
    name: us-east-2-datagrid-2
    port: 7800
    site: us-east-2
    value: 'tcp://10.0.0.179:7800'
```

where `address`, `port`, and `inventory_host` are connection details; `name` is the name of the host in the cluster, `site` is the name of the cluster in the xsite configuration,
and `value` is explicit connection string.


* Download and install defaults

| Variable | Description | Default |
|:---------|:------------|:--------|
|`infinispan_offline_install`| Perform an offline install |`False`|
|`infinispan_version`| Infinispan version to install | `14.0.13.Final` |
|`infinispan_bundle`| Archive name for Infinispan download | `infinispan-server-{{ infinispan_version }}.zip` |
|`infinispan_download_url`| Download URL for infinispan | `https://downloads.jboss.org/infinispan/{{ infinispan_version }}/{{ infinispan_bundle }}` |
|`infinispan_dest`| Directory where to extract installation archives | `/opt/infinispan` |
|`infinispan_installation_path`| Specific unxtracted installation path for infinispan | `/opt/infinispan/infinispan-server-{{ infinispan_version }}/` |
|`infinispan_app_download_dir`| Directory where to download archives | `/opt/infinispan` |
|`infinispan_healthcheck`| Check health of service at end of installation | `True` |
|`infinispan_bind_address`| Alternate bind address for the daemon | `localhost` |
|`infinispan_caches`| List of cache definitions to configure statically | `[]` |
|`infinispan_users`| List of users to create | `[]` |
|`infinispan_rest_cache_api_path`| Path of infinispan rest api | `/rest/v2/caches/` |
|`infinispan_configure_firewalld`| Ensure firewalld is running and configure infinispan ports | `False` |


Role Variables
--------------

The following are a set of required variables for the role:

| Variable | Description | Required |
|:---------|:------------|:---------|
|`infinispan_supervisor_password`| Password for the administration console user account | `yes` |
|`infinispan_users`| List of _user definitions_ to create | `no` |
|`infinispan_java_home`| JAVA_HOME of installed JRE, leave empty for using specified `infinispan_jvm_package` RPM path | `no` |

Sample _user definition_ format:

```yaml
infinispan_users:
  - { name: 'testuser1', password: 'test', roles: 'observer' }
  - { name: 'testuser2', password: 'test', roles: 'application' }
```

The following are _required_ when `infinispan_jgroups_discovery` is `JDBC_PING`:

| Variable | Description | Default |
|:---------|:------------|:--------|
|`infinispan_jdbc_engine` | backend database engine (values: `['mariadb','postgres','sqlserver']`) | `mariadb` |
|`infinispan_jdbc_driver_version`| driver version to download | `2.7.4` |
|`infinispan_jdbc_url`| URL for jdbc connection | `jdbc:mariadb://localhost:3306/keycloak` |
|`infinispan_jdbc_user`| username for jdbc connection | `keycloak-user` |
|`infinispan_jdbc_pass`| password for jdbc connection | `keycloak-pass` |

When setting up cross-DC relaying, also setup mariadb in active-active mode (ie. with galera cluster), and switch the JDBC to url to the `sequential` scheme; similar configuration for other database engines.


Dependencies
------------

The role depends on the following collections:

* [middleware_automation.common](https://github.com/ansible-middleware/common)
* [ansible.posix](https://github.com/ansible-collections/ansible.posix)

To install, from the collection root directory, run:

    ansible-galaxy collections install -r requirements.yml

Python _lxml_ and _jmespath_ libraries are needed on the host that executes this module. To install, from the collection root directory, run:

    pip install -r requirements.txt


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
            infinispan_supervisor_password: "changeme"
            infinispan_users: []
```


Offline installation
--------------------

Performing an offline installation is possible by:

* setting `infinispan_offline_install` to `True`
* making the file available to ansible controller, using as filename `infinispan_bundle`.


Keycloak integration
--------------------

Enabling `infinispan_keycloak_caches` will prepare the following caches in a dedicated cache container for remote keycloak access:

    - sessions
    - offlineSessions
    - clientSessions
    - offlineClientSessions
    - loginFailures
    - actionTokens
    - work

for more details, refer to the: [INSTALLATION AND CONFIGURATION GUIDE - 3.4.6. Infinispan caches](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.5/html-single/server_installation_and_configuration_guide/index#cache)


Deploying custom cache configurations
-------------------------------------

It is possible to deploy caches statically in the infinispan.xml server configuration, by populating the `infinispan_caches` list of dicts.
In case of clustered deployments, this configuration must be executed against all nodes in the cluster, as they are not propagated by the service.
To deploy cache configurations at runtime, refer to the `infinispan_cache` role instead.

For more details, refer to:
* [Configuring Infinispan Caches - 3.1 Declarative cache configuration](https://infinispan.org/docs/stable/titles/configuring/configuring.html#declarative-cache-configuration_cache-configuration)
* [Configuring Infinispan Caches - 3.3 Creating remote caches](https://infinispan.org/docs/stable/titles/configuring/configuring.html#creating-remote-caches)


How to configure caches
-----------------------

A cache configuration can be passed-in as an XML file or string, as it is generated by the infinispan server console; otherwise,
it is possible to define configuration dicts, used to populate the available templates.


To pass XML directly, as string or with a file:

```
infinispan_caches:
  - cache_xml: >
          <local-cache name="testcachexml" statistics="true">
            <encoding media-type="application/x-protostream"/>
          </local-cache>
  - cache_xml: "{{ lookup('file', user_data_file) }}"

```

To configure caches:

```
infinispan_caches:
  - cache_config:
      name: 'my-distributed-cache'
      template: 'distribute-cache'
      encoding: 'application/x-jboss-marshalling'
      persistence: False

```

It is possible to mix and match the two configurations in the `infinispan_caches` list.


License
-------

Apache License 2.0


Author Information
------------------

* [Guido Grazioli](https://github.com/guidograzioli)
* [Romain Pelisse](https://github.com/rpelisse)
* [Matthew Fernandez](https://github.com/l3acon)
