# Testing

## Continuous integration

The collection is tested with a [molecule](https://github.com/ansible-community/molecule) setup covering the included roles and verifying correct installation, configuration, and idempotency.
The test scenarios are available on the source code repository each on his own subdirectory under [molecule/](https://github.com/ansible-middleware/infinispan/molecule).


## Test playbooks

Sample playbooks are provided in the `playbooks/` directory; to run the playbooks locally (requires a rhel system with python 3.9+, ansible, and systemd) the steps are as follows:

```
# setup environment
pip install ansible-core
# clone the repository
git clone https://github.com/ansible-middleware/infinispan
cd infinispan
# install collection dependencies
ansible-galaxy collection install -r requirements.yml
# install collection python deps
pip install -r requirements.txt
# create inventory for localhost
cat << EOF > inventory
[infinispan]
localhost ansible_connection=local
EOF
# run the playbook
ansible-playbook -i inventory playbooks/infinispan.yml
```

