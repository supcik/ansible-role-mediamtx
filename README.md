# MediaMtx Ansible role

This role installs MediaMTX, a high-performance media server for RTSP, WebRTC, and SRT streaming.

It downloads the MediaMTX binary, installs it in the configured directory, fetches the default configuration, and prepares a systemd service unit for supported systems.

More information about MediaMTX can be found on the [official GitHub repository](https://github.com/bluenviron/mediamtx) or the [official website](https://mediamtx.org/).

## Requirements

- Ansible 2.2 or newer
- A target system running Linux or macOS
- A supported CPU architecture:
   - x86_64
   - aarch64
   - armv7l
   - i386

## Role variables

The role exposes the following variables through defaults/main.yml:

- `mediamtx_version`: MediaMTX release version to install (default: `1.19.3`)
- `mediamtx_install_dir`: Directory where the MediaMTX binary is installed (default: `/usr/local/bin`)
- `mediamtx_config_dir`: Directory where the configuration file is stored (default: `/etc/mediamtx`)
- `mediamtx_config_url`: URL of the default MediaMTX configuration file
- `mediamtx_supported_systems`: Supported operating systems for the role

## Dependencies

This role has no external dependencies.

## Example playbook

```yaml
---
- hosts: servers
  become: true
  roles:
    - name: ansible-role-mediamtx
      src: https://github.com/supcik/ansible-role-mediamtx.git
      scm: git
```

You can override variables if needed:

```yaml
---
- hosts: servers
  become: true
  vars:
    mediamtx_version: "1.19.3"
    mediamtx_install_dir: "/usr/local/bin"
  roles:
    - name: ansible-role-mediamtx
      src: https://github.com/supcik/ansible-role-mediamtx.git
      scm: git
```

## Notes

- The role downloads the official MediaMTX binary from GitHub releases.
- A sample systemd unit file is provided in templates/mediamtx.service.j2.
- The default configuration file is fetched only if it does not already exist, so local customizations are preserved.

## License

MIT

## Author information

Jacques Supcik <mailto:jacques@supcik.net>
