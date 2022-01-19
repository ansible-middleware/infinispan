# Ansible Collection - infinispan

[![Build Status](https://github.com/ansible-middleware/infinispan/workflows/CI/badge.svg?branch=main)](https://github.com/ansible-middleware/infinispan/actions/workflows/ci.yml)


Collection to install [Infinispan](https://infinispan.org/) or [Red Hat DataGrid](https://www.redhat.com/en/technologies/jboss-middleware/data-grid) server configurations, with optional remote caches for [Keycloak](https://www.keycloak.org/) or [Red Hat Single Sign-On](https://access.redhat.com/products/red-hat-single-sign-on). 

<!--start requires_ansible-->
## Ansible version compatibility

This collection has been tested against following Ansible versions: **>=2.9.10**.

Plugins and modules within a collection may be tested with only specific Ansible versions. A collection may contain metadata that identifies these versions.
<!--end requires_ansible-->

## Installation and Usage

### Installing the Collection from Ansible Galaxy

Before using the collection, you need to install it with the Ansible Galaxy CLI:

    ansible-galaxy collection install middleware_automation.infinispan

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: middleware_automation.infinispan
```

The infinispan collection also depends on the following python packages to be present on the controller host:

* lxml
* jmespath

A requirement file is provided to install:

    pip install -r requirements.txt


### Included roles

* `infinispan`: performs an installation of Infinispan or DataGrid nodes or cluster, with configuration of static caches.
* `infinispan_cache`: creates Infinispan or DataGrid caches at runtime.


### Choosing between Red Hat products and upstream project

The roles supports installing Red Hat Datagrid from the Customer Portal, when the following variables are defined:

```
rhn_username: '<customer_portal_username>'
rhn_password: '<customer_portal_password>'
jdg_rhn_id: '<datagrid_product_id>'
```

where `datagrid_product_id` is the ID for the specific Data Grid version, ie. _98151_ will install version _8.2.0_)


## License

Apache License v2.0 or later

See [LICENCE](LICENSE) to view the full text.

