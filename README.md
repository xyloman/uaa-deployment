# credhub-deployment

> A toolchain for deploying UAA with [BOSH](https://bosh.io).

This repository is a community-maintained set of [manifests](http://bosh.io/docs/manifest-v2.html) and [opsfiles](http://bosh.io/docs/cli-ops-files.html) useful for deploying UAA in various configurations to various IaaSes.

* Leverages [uaa-release](https://github.com/cloudfoundry/uaa-release)

## Example Usage

### Bosh Deploy

```bash
bosh deploy ./uaa.yml \
  --vars-store ./uaa-creds.yml \
  --vars-file ./uaa-vars.yml \
  -o ./operations/target-group.yml \
  -o ./operations/scale.yml
```

### Example uaa-vars.yml

```yaml
# uaa release
uaa_version: '53.3'
uaa_sha1: 'ce435cbb190611db2685f135edc49f9eab6bab89'
uaa_vm_type: 'm4.large'
uaa_host: "uaa.example.com"
network_name: "default"

# target-group.yml for external load balancer
uaa_target_group_name: 'uaa-target-group'

# scale.yml
uaa_instances: 2
uaa_azs: [z1, z2, z3]

# external database
uaa_database_host: "hostname"
uaa_database_port: "5432"
uaa_database_username: "uaa"
uaa_database_password: "password"
```

## Operator Files

### scale.yml

uaa_azs - Update a UAA deployment to scale accross multiple AZs.
uaa_instances - Update a UAA deployment to change the number of instances of the service that is ran (e.g. VM Instances).

### target-group.yml

uaa_target_group_name - Update a UAA deployment to associate the uaa instance group with a vm_extension target_group used in AWS to associate an external load balancer or target group configured in cloud config.