---
title: "Immich"
---

Homepage: [https://immich.app](https://immich.app)

GitHub: [https://github.com/immich-app/immich](https://github.com/immich-app/immich)

Immich is a high-performance, self-hosted photo and video backup solution. It provides the ease and convenience of commercial cloud photo services while respecting your privacy and data ownership. Immich offers a modern, responsive web interface and native mobile apps for Android and iOS.

## Usage

Set `immich_enabled: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

If you want to access Immich externally, set `immich_available_externally: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

The Immich web interface can be found at [http://ansible_nas_host_or_ip:2283](http://ansible_nas_host_or_ip:2283).

## Specific Configuration

For security, it's recommended to change these default settings in your `inventories/<your_inventory>/group_vars/nas.yml` file:

```yaml
immich_db_password: "your_secure_password_here"
```

You can also configure the photo upload directory by changing:

```yaml
immich_upload_directory: "/path/to/your/photos"
```

### Immich Power Tools

Immich Power Tools provides additional utilities for managing your Immich library. To enable it, set:

```yaml
immich_install_power_tools: true
```

The Immich Power Tools web interface can be accessed at [http://ansible_nas_host_or_ip:3035](http://ansible_nas_host_or_ip:3035).

### Hardware Considerations

For optimal performance, especially with the machine learning features like facial recognition:

- At least 4GB RAM is recommended
- Higher memory allocations may be needed for large libraries
- Consider increasing `immich_machinelearning_memory` from the default 4GB for large libraries

### Mobile Apps

Immich provides mobile apps for both iOS and Android that can be used to automatically back up photos and videos from your devices:

- [Android app](https://play.google.com/store/apps/details?id=app.alextran.immich)
- [iOS app](https://apps.apple.com/us/app/immich/id1613945652)
