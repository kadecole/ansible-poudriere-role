# ansible-poudriere-role

[![CircleCI](https://img.shields.io/circleci/project/uchida/ansible-poudriere-role.svg)](https://circleci.com/gh/uchida/ansible-poudriere-role)
[![License](https://img.shields.io/github/license/uchida/ansible-poudriere-role.svg)](http://creativecommons.org/publicdomain/zero/1.0/deed)

role to install poudriere, clean room package builder for FreeBSD.
In addition, this role creates default ports tree and builder jail.

## Role Variables

Available variables are listed below, along with default values:

```yaml
  poudriere_zpool: zroot
  poudriere_jail: "FreeBSD:9:amd64"
  poudriere_jailversion: 9.3-RELEASE
  poudriere_portsmethod: portsnap
```

Use zfs pool named `{{ poudriere_zpool }}`, when available.
Creates builder jail with `{{ poudriere_jail }}` and
specify its version with `{{ poudriere_jailversion }}`.
`{{ poudriere_portsmethod }}` could be one of the following values

- `portsnap`
- `svn`
- `svn+http`
- `svn+https`
- `svn+ssh`
- `git`

## Example Playbook

install poudriere with `tank` zpool.

```yaml
  - hosts: servers
    roles:
    - { role: uchida.poudriere, poudriere_zpool: tank }
```

creates `9.3-RELEASE` and `10.2-RELEASE` builder.

```yaml
  - hosts: servers
    roles:
    - role: uchida.poudriere
      poudriere_jail: "FreeBSD:9:amd64"
      poudriere_jailversion: 9.3-RELEASE
    - role: uchida.poudriere
      poudriere_jail: "FreeBSD:10:amd64"
      poudriere_jailversion: 10.2-RELEASE
```

creates `10.2-RELEASE` builder and git ports tree.

```yaml
  - hosts: servers
    roles:

    - role: uchida.poudriere
      poudriere_jail: "FreeBSD:10:amd64"
      poudriere_jailversion: 10.2-RELEASE
      poudriere_portsmethod: git
```

## License

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed)

dedicated to public domain by [contributors](https://github.com/uchida/packer-poudriere/graphs/contributors).

