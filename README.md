<!--
SPDX-FileCopyrightText: 2023 Julian-Samuel Gebühr
SPDX-FileCopyrightText: 2023 Slavi Pantaleev
SPDX-FileCopyrightText: 2025 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# InfluxDB Ansible role

>[!WARNING]
> This role is configured to install [InfluxDB OSS v2](https://docs.influxdata.com/influxdb/v2/). Though [InfluxDB 3 Core](https://docs.influxdata.com/influxdb3/core/) is open source, it is **not** a replacement for OSS v2. [InfluxDB 3 Enterprise](https://docs.influxdata.com/influxdb3/enterprise/) can replace OSS v2, but it is proprietary and we will not support it.

This is an [Ansible](https://www.ansible.com/) role which installs [InfluxDB](https://www.influxdata.com/) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

This role *implicitly* depends on:

- [`com.devture.ansible.role.playbook_help`](https://github.com/devture/com.devture.ansible.role.playbook_help)
- [`com.devture.ansible.role.systemd_docker_base`](https://github.com/devture/com.devture.ansible.role.systemd_docker_base)

Check [defaults/main.yml](defaults/main.yml) for the full list of supported options.

💡 See this [document](docs/configuring-influxdb.md) for details about setting up the service with this role.

## Development

You can optionally install [pre-commit](https://pre-commit.com/) so that simple mistakes are checked and noticed before changes are pushed to a remote branch. See [`.pre-commit-config.yaml`](./.pre-commit-config.yaml) for which hooks are to be executed.

See [this section](https://pre-commit.com/#usage) on the official documentation for usage.
