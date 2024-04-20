# Pi-hole

[![CI](https://github.com/DudeCalledBro/pihole/actions/workflows/ci.yml/badge.svg)](https://github.com/DudeCalledBro/pihole/actions/workflows/ci.yml)

This repository contains my ansible deployment for Pi-hole. I am using Pi-hole on a Raspberry Pi 4 with Docker and it's been running rock-solid. The ansible deployment is designed to run on any platform with supported docker.

## Prerequisites

- Ensure you have Ansible installed (e.g. `pip3 install ansible`)
- Ensure Docker is installed on the Pi-hole server (you may want to checkout my [ansible-docker-role](https://github.com/DudeCalledBro/ansible-role-docker))

## Installation

1. Copy the `example.inventory.yml` file to `inventory.yml` and setup as you need. Ensure you also check the role's defaults.

2. Run the Ansible playbook to deploy Pi-hole

    ```bash
    ansible-playbook play-pihole.yml
    ```

    > Notice: Checkout the possible environment variables for Pi-hole (e.g. `TZ` or `WEBPASSWORD`). Check it out [here](https://github.com/pi-hole/docker-pi-hole?tab=readme-ov-file#environment-variables).

3. (**Optional**) Run the Ansible resolvconf playbook to update the Pi-hole server's resolvconf to use the local service

    ```bash
    ansible-playbook play-resolvconf.yml
    ```

## Backup and Restore

1. Login into the Pi-hole admin web gui

2. Change to `Settings` > `Teleporter`

3. There you either want to backup your data or restore it from an existing TAR file

> **Notice!** The Pi-hole ansible role creates an cronjob that backups all required data. You may want to mount the backup directory `{{ pihole_docker_path }}/backups` on to a NAS or dedicated hard drive.

## Further

- The Pi-hole web gui is reachable at `http://pihole.local/admin/login.php`

## License

Copyright © 2024 Niclas Spreng

Licensed under the [MIT license](LICENSE).
