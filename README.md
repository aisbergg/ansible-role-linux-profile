# Ansible Role: `aisbergg.linux-profile`

The purpose of this Ansible role is to configure shell profiles like bashrc and such. The role doesn't come with any files or templates, you have to supply your own. As such the role acts simply as a helper to install your personal shell profiles on an Ansible controlled machine.

## Requirements

None.

## Role Variables

| Variable | Default | Comments |
|----------|---------|----------|
| `linux_profile_packages` | `[]` | List of extra packages to be installed. |
| `linux_profile` | `{}` | Dictionary of files (e.g. `/etc/profile`) to copy. |
| `linux_profile["/path/to/file"]` | `{}` | Destination path for a file. |
| `linux_profile["/path/to/file"].content` |  | Content to copy into `/path/to/file`. |
| `linux_profile["/path/to/file"].file` |  | File to copy to `/path/to/file`. |
| `linux_profile["/path/to/file"].template` |  | Template file to create `/path/to/file`. |
| `linux_profile["/path/to/file"].owner` |  | Owner of the file. |
| `linux_profile["/path/to/file"].group` |  | Group of the file. |
| `linux_profile["/path/to/file"].mode` |  | Mode of the file. |
| `linux_profile["/path/to/file"].state` | `present` | Whether the file/dir shall be `present` or `absent`. |
| `linux_profile_default_owner` |  | Default for file owner. |
| `linux_profile_default_group` |  | Default for file group. |
| `linux_profile_default_mode` |  | Default for file mode. |

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  vars:
    linux_profile_packages:
      - bc
      - zsh

    linux_profile:
      # create /etc/profile by rendering a template
      "/etc/profile":
        template: profile.j2
        vars:
          foo: bar
        owner: root
        group: root
        mode: "0644"

      # create /etc/bash.bashrc by copying a file
      "/etc/bash.bashrc":
        file: bash.bashrc

      # create /etc/zsh/zprofile by providing its content
      "/etc/zsh/zprofile":
        content: |
          emulate sh -c 'source /etc/profile'

      # delete a file
      "/etc/motd.d/cockpit":
        state: absent

  roles:
    - aisbergg.linux-profile
```

## License

MIT

## Author Information

Andre Lehmann (aisberg@posteo.de)
