# duply

[![Source Code](https://img.shields.io/badge/github-source%20code-blue?logo=github&logoColor=white)](https://github.com/rolehippie/duply)
[![General Workflow](https://github.com/rolehippie/duply/actions/workflows/general.yml/badge.svg)](https://github.com/rolehippie/duply/actions/workflows/general.yml)
[![Readme Workflow](https://github.com/rolehippie/duply/actions/workflows/docs.yml/badge.svg)](https://github.com/rolehippie/duply/actions/workflows/docs.yml)
[![Galaxy Workflow](https://github.com/rolehippie/duply/actions/workflows/galaxy.yml/badge.svg)](https://github.com/rolehippie/duply/actions/workflows/galaxy.yml)
[![License: Apache-2.0](https://img.shields.io/github/license/rolehippie/duply)](https://github.com/rolehippie/duply/blob/master/LICENSE)
[![Ansible Role](https://img.shields.io/badge/role-rolehippie.duply-blue)](https://galaxy.ansible.com/rolehippie/duply)

Ansible role to install duply as a simple backup solution.

## Sponsor

Building and improving this Ansible role have been sponsored by my current and previous employers like **[Cloudpunks GmbH](https://cloudpunks.de)** and **[Proact Deutschland GmbH](https://www.proact.eu)**.

## Table of contents

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [duply_default_command](#duply_default_command)
  - [duply_default_day](#duply_default_day)
  - [duply_default_gpg_key](#duply_default_gpg_key)
  - [duply_default_gpg_opts](#duply_default_gpg_opts)
  - [duply_default_gpg_passwd](#duply_default_gpg_passwd)
  - [duply_default_hour](#duply_default_hour)
  - [duply_default_max_age](#duply_default_max_age)
  - [duply_default_max_full](#duply_default_max_full)
  - [duply_default_minute](#duply_default_minute)
  - [duply_default_month](#duply_default_month)
  - [duply_default_variables](#duply_default_variables)
  - [duply_default_verbosity](#duply_default_verbosity)
  - [duply_default_volsize](#duply_default_volsize)
  - [duply_default_weekday](#duply_default_weekday)
  - [duply_profiles](#duply_profiles)
  - [duply_target](#duply_target)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.10`

## Supported Platforms

| Platform | Versions | Install Method |
|----------|----------|----------------|
| Ubuntu | 18.04, 20.04, 22.04, 24.04 | `apt` (duply + duplicity as packages) |
| Amazon Linux | 2023 | `pip` (duplicity) + source (duply script) |
| RHEL/CentOS | 7, 8, 9 | `dnf` via EPEL (duply + duplicity) |

### Amazon Linux 2023 Notes

Neither `duply` nor `duplicity` are in the standard AL2023 repositories:
- **duplicity** is installed via `pip`
- **duply** is downloaded as a source tarball from SourceForge and installed to `/usr/local/bin/duply`
- **cronic** is cloned from GitHub and symlinked to `/usr/bin/cronic`

Set `duply_install_cronic: false` if cronic is already installed by another role or playbook task.

## Default Variables

### duply_default_command

Default backup command

#### Default value

```YAML
duply_default_command: full+purgeFull --force
```

### duply_default_day

Default day cron entry

#### Default value

```YAML
duply_default_day: '*'
```

### duply_default_gpg_key

Default GnuPG key

#### Default value

```YAML
duply_default_gpg_key: disabled
```

### duply_default_gpg_opts

Default GnuPG options

#### Default value

```YAML
duply_default_gpg_opts: --pinentry-mode loopback
```

### duply_default_gpg_passwd

Default GnuPG password

#### Default value

```YAML
duply_default_gpg_passwd:
```

### duply_default_hour

Default hour cron entry

#### Default value

```YAML
duply_default_hour: '5'
```

### duply_default_max_age

Default max age

#### Default value

```YAML
duply_default_max_age: 1M
```

### duply_default_max_full

Default max full

#### Default value

```YAML
duply_default_max_full: '1'
```

### duply_default_minute

Default minute cron entry

#### Default value

```YAML
duply_default_minute: '5'
```

### duply_default_month

Default month cron entry

#### Default value

```YAML
duply_default_month: '*'
```

### duply_default_variables

Default variables list

#### Default value

```YAML
duply_default_variables: []
```

#### Example usage

```YAML
duply_default_variables:
  - key: aws_access_key_id
    value: S62L74JZVLLKQ5E9077R
  - key: aws_secret_access_key
    value: xmGiLiTMBGzMMwRh+jAYBvn9C7roiuDqVHDF_+RI
```

### duply_pip_packages

Python packages to install via pip (for platforms without native packages).
Set automatically by OS vars files.

#### Default value

```YAML
duply_pip_packages: []
```

### duply_install_method

How to install duply — `package` (dnf/apt) or `source` (download tarball).
Set automatically by OS vars files.

#### Default value

```YAML
duply_install_method: package
```

### duply_source_url

URL to download duply source tarball (when `duply_install_method` is `source`).

#### Default value

```YAML
duply_source_url: "https://sourceforge.net/projects/ftplicity/files/duply%20%28simple%20duplicity%29/2.5.x/duply_2.5.1.tgz/download"
```

### duply_source_version

Version string for duply source install (used for idempotency check).

#### Default value

```YAML
duply_source_version: "2.5.1"
```

### duply_bin_path

Path where duply binary is installed. On Ubuntu this is `/usr/bin/duply` (from package).
On AL2023/RHEL with source install, this is `/usr/local/bin/duply`.

#### Default value

```YAML
duply_bin_path: /usr/local/bin/duply
```

### duply_install_cronic

Whether to install cronic (cron error reporting wrapper). Set to `false` if cronic
is already installed by another role or playbook task.

#### Default value

```YAML
duply_install_cronic: true
```

### duply_cronic_install_method

How to install cronic — `package` (apt on Ubuntu) or `source` (git clone on AL2023/RHEL).
Set automatically by OS vars files.

#### Default value

```YAML
duply_cronic_install_method: source
```

### duply_cronic_repo

Git repo URL for cronic source install.

#### Default value

```YAML
duply_cronic_repo: "https://github.com/justincase/cronic.git"
```

### duply_cronic_src_path

Local path to clone cronic source.

#### Default value

```YAML
duply_cronic_src_path: /opt/umac/src/cronic
```

### duply_log_dir

Directory for backup log files. Each profile gets its own log at `<dir>/<profile-name>.log`.
Set to empty string to disable file logging (falls back to cronic-only mode).

#### Default value

```YAML
duply_log_dir: /var/log/duply
```

### duply_use_cronic

Wrap backup command with cronic (emails MAILTO on failure only).
Only used when `duply_log_dir` is empty. When logging is enabled, cron's native
MAILTO handles failure alerts via the exit code.

#### Default value

```YAML
duply_use_cronic: true
```

### duply_default_max_fullbkp_age

Maximum age of the last full backup before an incremental run is automatically
promoted to a full backup. Set to `1W` for weekly full backups with daily incrementals.

#### Default value

```YAML
duply_default_max_fullbkp_age: 1W
```

### duply_default_verbosity

Default verbosity level

#### Default value

```YAML
duply_default_verbosity: '1'
```

### duply_default_volsize

Default volume size

#### Default value

```YAML
duply_default_volsize: '1024'
```

### duply_default_weekday

Default weekday cron entry

#### Default value

```YAML
duply_default_weekday: '*'
```

### duply_profiles

List of profile definitions

#### Default value

```YAML
duply_profiles: []
```

#### Example usage

```YAML
duply_profiles:
  - name: owncloud
    includes:
      - /var/lib/owncloud
  - name: external
    target: ftp://username:p455w0rd@ftp.example.com
    ansible.builtin.command: full+verify+purge --force
    gpg_key: 52DCE5AE1FC80340A33894F5D583668622CDE10E
    gpg_passwd: p455w0rd
    max_age: 1W
    max_full: '7'
    verbosity: '1'
    minute: '0'
    hour: '5'
    day: '*'
    month: '*'
    weekday: '*'
    includes:
      - /var/lib/foo
      - /var/lib/bar
```

### duply_target

Target for backups

#### Default value

```YAML
duply_target:
```

#### Example usage

```YAML
s3://backup.example.com
```

## Discovered Tags

**_duply_**

**_ipsec_**

## Dependencies

- None

## License

Apache-2.0

## Author

[Thomas Boerger](https://github.com/tboerger)
