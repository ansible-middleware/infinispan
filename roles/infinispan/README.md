infinispan
==========

Install [Infinispan](https://infinispan.org/) or [Red Hat DataGrid](https://www.redhat.com/en/technologies/jboss-middleware/data-grid) server configurations.


Role Defaults
-------------

| Variable | Description | Default |
|:---------|:------------|:--------|
|`infinispan_keycloak_caches`| Creates remote caches for keycloak | `False` |
|`jdg_port`| Alternate port for the service | `11222` |
|`jdg_jgroups_port`| Alternate port for the jgroups cluster | `7800` |
|`jdg_jgroups_relay_port`| Alternate port for the jgroups relaying cluster | `7801` |
|`jdg_bind_addr`| Alternate bind address for the daemon | `localhost` |
|`jdg_jgroups_relay`| Enable cross-DC relaying | `False` |
|`jdg_jgroups_relay_sites`| List of site names for cross-DC relaying | `[]` |
|`jdg_jgroups_relay_site`| Site the inventory host is in when cross-DC is enabled | `''` |
|`jdg_jgroups_jdbcping`| Enable clustering using JDBC PING discovery | `False` |
|`jdg_keycloak_persistence`| Enable persitence datasource for keycloak caches | `False` |
|`jdg_service_user`| posix account for the service installation | `jdg` |
|`jdg_service_group`| posix group for the service installation | `jdg` |
|`jdg_logfile_format` | main logfile format: FILE or JSON-FILE | `FILE` |
|`jdg_logfile_root_level`| Root logging level: TRACE, DEBUG, INFO, WARN, ERROR | `INFO` |
|`jdg_logfile_enable_audit` | Enable additional audit.log logfile | `True` |
|`jdg_logfile_enable_hotrod_accesslog` | Enable additional hotrod-access.log | `False` |
|`jdg_logfile_enable_rest_accesslog` | Enable additional rest-access.log | `False` |
|`jdg_logfile_maxsize` | Max file size, triggers rotation | `100 MB` |
|`jdg_default_realm_tls`| Enable TLS server certificate | `False` |
|`jdg_keystore_path`| Path to keystore containing server identity certificate | `/etc/pki/java/cacerts` |
|`jdg_keystore_password`| Keystore password | `changeit` |
|`jdg_keystore_key_password` | Key passphrase for TLS server identity | `''`|
|`jvm_package`| RHEL java package runtime | `java-1.8.0-openjdk-devel` |


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

The following are required when `jdg_jgroups_jdbcping` is enabled:

| Variable | Description | Default |
|:---------|:------------|:--------|
|`jdg_jdbc_engine`| backend database engine (values: `['mariadb','postgres']`) | `mariadb` |
|`jdg_jdbc_driver_version`| driver version to download | `2.7.4` |
|`jdg_jdbc_url`| URL for jdbc connection | `jdbc:mariadb://localhost:3306/keycloak` |
|`jdg_jdbc_user`| username for jdbc connection | `keycloak-user` |
|`jdg_jdbc_pass`|password for jdbc connection | `keycloak-pass` |

When setting up cross-DC relaying, also setup mariadb in active-active mode (ie. with galera cluster), and switch the JDBC to url to the `sequential` scheme; similar configuration for other database engines.


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

Choosing what to install
------------------------

The role will install Red Hat DataGrid when the following variables are defined in the playbook execution:

```
jdg_rhn_id: '98151'
rhn_username: '<customer portal account username>'
rhn_password: '<customer portal account password>'
```

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

License
-------

Apache License 2.0

Author Information
------------------

* [Guido Grazioli](https://github.com/guidograzioli)
* [Romain Pelisse](https://github.com/rpelisse)
* [Matthew Fernandez](https://github.com/l3acon)