---
title: "AdGuard Home"
---

Homepage: [https://adguard.com/en/adguard-home/overview.html](https://adguard.com/en/adguard-home/overview.html)

Docker Container: [https://hub.docker.com/r/adguard/adguardhome](https://hub.docker.com/r/adguard/adguardhome)

AdGuard Home is a network-wide software for blocking ads & tracking. After you set it up, it'll cover ALL your home devices, and you don't need any client-side software for that.

## Usage

Set `adguard_home_enabled: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

If you want to access AdGuard Home externally, set `adguard_home_available_externally: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

The AdGuard Home web interface can be found at [http://ansible_nas_host_or_ip:3000](http://ansible_nas_host_or_ip:3000).

## Specific Configuration

The first time you access AdGuard Home, you will be guided through a setup wizard where you can:

1. Set admin username and password
2. Configure DNS settings
3. Enable protection features

To use AdGuard Home as your DNS server, configure your router to use your Ansible-NAS IP address as the primary DNS server or configure individual devices to use it.
