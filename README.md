# Influxdb Ansible Role

[influxdb](https://www.influxdata.com/) is a self-hosted time-series database. This role helps you to set up influxdb:

- with everything run in [Docker](https://www.docker.com/) containers
- powered by [the official influxdb container image](https://hub.docker.com/r/superseriousbusiness/influxdb/)


## Installing

To configure and install influxdb on your own server(s), you should use a playbook like [Mother of all self-hosting](https://github.com/mother-of-all-self-hosting/mash-playbook) or write your own.

# Configuring this role for your playbook

```
influxdb_enabled: true
influxdb_hostname: 'example.org'
```

## Advanced configuration

To bootstrap an initial user, bucket and organization you can use

```yaml
# Configure the inital user, organization and bucket
# This setting will only be used once upon initial installation of influxdb. Changing this values after the first
# start of influxdb will have no effect.
# Not setting this will allow you to manually set these by visiting the domain you set in influxdb_hostname after installation.
influxdb_init: true
influxdb_init_username: "USERNAME"
influxdb_init_password: "SUPERSECRETPASSWORD"
influxdb_init_org: "EXAMPLE_ORG"
influxdb_init_bucket: "SOMEBUCKET"
```

## Support

- Github issues: [mother-of-all-self-hosting/ansible-role-influxdb/issues](https://github.com/mother-of-all-self-hosting/ansible-role-influxdb.git/issues)
