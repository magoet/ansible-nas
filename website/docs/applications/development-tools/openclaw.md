---
title: "OpenClaw"
---

Homepage: [https://docs.openclaw.ai/](https://docs.openclaw.ai/)

OpenClaw is an AI gateway with a browser-based Control UI.

This role uses the official Docker deployment documented here: [https://docs.openclaw.ai/install/docker](https://docs.openclaw.ai/install/docker).

## Usage

Set `openclaw_enabled: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

The OpenClaw Control UI can be found at [http://ansible_nas_host_or_ip:18789](http://ansible_nas_host_or_ip:18789).

## Specific Configuration

Set `openclaw_gateway_token` in your inventory to a secure random value before exposing OpenClaw beyond your local network.

OpenClaw stores persistent data in:

- `{{ docker_home }}/openclaw/config` -> `/home/node/.openclaw`
- `{{ docker_home }}/openclaw/workspace` -> `/home/node/.openclaw/workspace`

Official docs treat Docker as optional overall, but this Ansible-NAS role intentionally uses the Docker option.