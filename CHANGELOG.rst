===============================================
middleware\_automation.infinispan Release Notes
===============================================

.. contents:: Topics

This changelog describes changes after version 0.1.9.

v1.3.3
======

Minor Changes
-------------

- Update to infinispan 15.2 / datagrid 8.5 `#49 <https://github.com/ansible-middleware/infinispan/pull/49>`_

v1.3.2
======

Minor Changes
-------------

- Update minimum ansible-core >= 2.15 `#46 <https://github.com/ansible-middleware/infinispan/pull/46>`_
- Update to 8.4.8 / 15.0.2 and remove deprecated configs `#44 <https://github.com/ansible-middleware/infinispan/pull/44>`_

v1.3.1
======

Minor Changes
-------------

- New parameter ``infinispan_jgroups_cluster_nodes`` to explicitly set initial nodes `#43 <https://github.com/ansible-middleware/infinispan/pull/43>`_

Bugfixes
--------

- Output cluster initial node list for TCPPING grouped by site when relay is enabled `#42 <https://github.com/ansible-middleware/infinispan/pull/42>`_

v1.3.0
======

Minor Changes
-------------

- Update infinispan to 14.0.21, data_grid to 8.4.6 `#39 <https://github.com/ansible-middleware/infinispan/pull/39>`_

Breaking Changes / Porting Guide
--------------------------------

- Update minimum ansible-core version to 2.14 `#37 <https://github.com/ansible-middleware/infinispan/pull/37>`_

v1.2.0
======

Major Changes
-------------

- Provide jgroups configuration `#31 <https://github.com/ansible-middleware/infinispan/pull/31>`_

Minor Changes
-------------

- Update to infinispan 14.0.13 `#32 <https://github.com/ansible-middleware/infinispan/pull/32>`_
- infinispan_cache: remove dependency on json_query `#34 <https://github.com/ansible-middleware/infinispan/pull/34>`_

Bugfixes
--------

- Force log directory symlink during update `#33 <https://github.com/ansible-middleware/infinispan/pull/33>`_

v1.1.4
======

Minor Changes
-------------

- Add sqlserver to infinispan jdbc configurations `#25 <https://github.com/ansible-middleware/infinispan/pull/25>`_
- Provide systemd unit restart behavior configuration `#26 <https://github.com/ansible-middleware/infinispan/pull/26>`_

v1.1.3
======

Minor Changes
-------------

- Switch redhat_csp_download with runtimes_common `#24 <https://github.com/ansible-middleware/infinispan/pull/24>`_

v1.1.2
======

Minor Changes
-------------

- Update defaults to infinispan 14.0.3 - data grid 8.4.0 `#23 <https://github.com/ansible-middleware/infinispan/pull/23>`_

v1.1.1
======

Bugfixes
--------

- Add requirements.yml dependencies to galaxy.yml `#21 <https://github.com/ansible-middleware/infinispan/pull/21>`_

v1.1.0
======

Breaking Changes / Porting Guide
--------------------------------

- Rename roles and variables to have ``infinispan_`` prefix `#17 <https://github.com/ansible-middleware/infinispan/pull/17>`_

v1.0.3
======

Release Summary
---------------

Patch release containing an important bugfix for downloaded archives filemodes.

v1.0.2
======

Major Changes
-------------

- Make playbook compatible with multiple installations on same host `#12 <https://github.com/ansible-middleware/infinispan/pull/12>`_

Minor Changes
-------------

- Make ``supervisor_password`` a default with assert (was: role variable) `#14 <https://github.com/ansible-middleware/infinispan/pull/14>`_
- New ``jdg_configure_firewalld`` bool parameter controls firewall config `#13 <https://github.com/ansible-middleware/infinispan/pull/13>`_

Bugfixes
--------

- JAVA_HOME should be set according to requested JVM package, or overridden via ``jdg_java_home`` `#15 <https://github.com/ansible-middleware/infinispan/pull/15>`_

v1.0.1
======

Release Summary
---------------

Patch release containing only cleanup and documentation changes.

v1.0.0
======

Release Summary
---------------

This is the first stable release of the ``middleware_automation.infinispan`` collection.
