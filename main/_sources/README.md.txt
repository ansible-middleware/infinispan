# Ansible Collection - middleware_automation.infinispan

<!--start build_status -->
[![Build Status](https://github.com/ansible-middleware/infinispan/workflows/CI/badge.svg?branch=main)](https://github.com/ansible-middleware/infinispan/actions/workflows/ci.yml)

> **_NOTE:_ If you are Red Hat customer, install `redhat.data_grid` from [Automation Hub](https://console.redhat.com/ansible/ansible-dashboard) as the certified version of this collection.**
<!--end build_status -->

<!--start upstream_downstream -->
This is an Ansible collection dedicated to [Infinispan](https://infinispan.org/).

Infinispan can be used as remote caches for other software, such as [Keycloak](https://www.keycloak.org/) or [Wildfly](https://https://www.wildfly.org/).
<!--end upstream_downstream -->


<!--start requires_ansible-->
## Ansible version compatibility

This collection has been tested against following Ansible versions: **>=2.14.0**.

Plugins and modules within a collection may be tested with only specific Ansible versions. A collection may contain metadata that identifies these versions.
<!--end requires_ansible-->


## Installation and Usage

<!--start galaxy_download -->
### Installing the Collection from Ansible Galaxy

Before using the collection, you need to install it with the Ansible Galaxy CLI:

    ansible-galaxy collection install middleware_automation.infinispan

<!--end galaxy_download -->

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: middleware_automation.infinispan
```


### Build and install locally

Clone the repository, checkout the tag you want to build, or pick the main branch for the development version; then:

    ansible-galaxy collection build .
    ansible-galaxy collection install middleware_automation-amq-*.tar.gz


### Dependencies

#### Ansible collections:

* [middleware_automation.common](https://github.com/ansible-middleware/common)
* [ansible.posix](https://docs.ansible.com/ansible/latest/collections/ansible/posix/index.html)

#### Python:

The infinispan collection also depends on the following python packages to be present on the controller host:

* lxml
* jmespath

A requirement file is provided to install:

    pip install -r requirements.txt

<!--start roles_paths -->
### Included roles

* [`infinispan`](https://github.com/ansible-middleware/infinispan/tree/main/roles/infinispan): performs an installation of Infinispan or DataGrid nodes or cluster, with configuration of static caches.
* [`infinispan_cache`](https://github.com/ansible-middleware/infinispan/tree/main/roles/infinispan_cache): creates Infinispan or DataGrid caches at runtime.
<!--end roles_paths -->

<!--start support -->
<!--end support -->


## License

Apache License v2.0 or later

See [LICENSE](LICENSE) to view the full text.
