==============================================
middleware_automation.infinispan Release Notes
==============================================

.. contents:: Topics

This changelog describes changes after version 0.1.9.

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

