<!--
SPDX-FileCopyrightText: 2020 - 2024 MDAD project contributors
SPDX-FileCopyrightText: 2020 - 2024 Slavi Pantaleev
SPDX-FileCopyrightText: 2020 Aaron Raimist
SPDX-FileCopyrightText: 2020 Chris van Dijk
SPDX-FileCopyrightText: 2020 Dominik Zajac
SPDX-FileCopyrightText: 2020 Mickaël Cornière
SPDX-FileCopyrightText: 2022 François Darveau
SPDX-FileCopyrightText: 2022 Julian Foad
SPDX-FileCopyrightText: 2022 Warren Bailey
SPDX-FileCopyrightText: 2023 Antonis Christofides
SPDX-FileCopyrightText: 2023 Felix Stupp
SPDX-FileCopyrightText: 2023 Julian-Samuel Gebühr
SPDX-FileCopyrightText: 2023 Pierre 'McFly' Marty
SPDX-FileCopyrightText: 2024 - 2025 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Setting up InfluxDB OSS v2

This is an [Ansible](https://www.ansible.com/) role which installs [InfluxDB OSS v2](https://docs.influxdata.com/influxdb/v2/) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

InfluxDB OSS v2 is a self-hosted time-series database.

See the project's [documentation](https://docs.influxdata.com/influxdb/v2/get-started/) to learn what InfluxDB OSS v2 does and why it might be useful to you.

## Adjusting the playbook configuration

To enable InfluxDB OSS v2 with this role, add the following configuration to your `vars.yml` file.

**Note**: the path should be something like `inventory/host_vars/mash.example.com/vars.yml` if you use the [MASH Ansible playbook](https://github.com/mother-of-all-self-hosting/mash-playbook).

```yaml
########################################################################
#                                                                      #
# influxdb                                                             #
#                                                                      #
########################################################################

influxdb_enabled: true

########################################################################
#                                                                      #
# /influxdb                                                            #
#                                                                      #
########################################################################
```

### Set the hostname

To enable InfluxDB OSS v2 you need to set the hostname as well. To do so, add the following configuration to your `vars.yml` file. Make sure to replace `example.com` with your own value.

```yaml
influxdb_hostname: "example.com"
```

After adjusting the hostname, make sure to adjust your DNS records to point the domain to your server.

### Configure the initial user (optional)

You can set up the initial user by adding the following configuration to your `vars.yml` file:

```yaml
influxdb_init: true
influxdb_init_username: YOUR_USERNAME_HERE
influxdb_init_password: YOUR_PASSWORD_HERE
influxdb_init_org: YOUR_EXAMPLE_ORG_HERE
influxdb_init_bucket: YOUR_BUCKET_HERE
```

>[!NOTE]
> The settings will only be used once upon initial installation of InfluxDB OSS v2. Changing these values after the first start will have no effect.

Not setting them allows you to create the user manually after installation by going to the hostname set to `influxdb_hostname`.

### Expose the port for external services (optional)

In order to let external services (like Proxmox or Grafana) access the InfluxDB OSS v2's HTTP API, the corresponding port needs to be exposed.

```yaml
influxdb_container_http_host_bind_port: PORT_NUMBER_HERE
```

### Extending the configuration

There are some additional things you may wish to configure about the component.

Take a look at:

- [`defaults/main.yml`](../defaults/main.yml) for some variables that you can customize via your `vars.yml` file. You can override settings (even those that don't have dedicated playbook variables) using the `influxdb_environment_variables_additional_variables` variable

See the [documentation](https://docs.influxdata.com/influxdb/v2/reference/config-options/) for a complete list of InfluxDB OSS v2's config options that you could put in `influxdb_environment_variables_additional_variables`.

## Installing

After configuring the playbook, run the installation command of your playbook as below:

```sh
ansible-playbook -i inventory/hosts setup.yml --tags=setup-all,start
```

If you use the MASH playbook, the shortcut commands with the [`just` program](https://github.com/mother-of-all-self-hosting/mash-playbook/blob/main/docs/just.md) are also available: `just install-all` or `just setup-all`

## Usage

After running the command for installation, the InfluxDB OSS v2 instance becomes available at the URL specified with `influxdb_hostname`. With the configuration above, the service is hosted at `https://influxdb.example.com`.

To get started, open the URL with a web browser, and log in to the service if `influxdb_init` is set to `true` (or configure the first user if it is not).

## Troubleshooting

### Check the service's logs

You can find the logs in [systemd-journald](https://www.freedesktop.org/software/systemd/man/systemd-journald.service.html) by logging in to the server with SSH and running `journalctl -fu influxdb` (or how you/your playbook named the service, e.g. `mash-influxdb`).
