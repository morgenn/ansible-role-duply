# Changelog

## [3.0.0](https://github.com/morgenn/ansible-role-duply/compare/v2.1.0...v3.0.0) (2026-05-31)


### Features

* add Amazon Linux 2023 and RHEL/CentOS support ([al2023-updates](https://github.com/morgenn/ansible-role-duply/tree/al2023-updates))
* install duplicity via pip on platforms without native packages (AL2023)
* install duply from source tarball when not available as system package
* add cronic install task (package on Ubuntu, git clone on AL2023/RHEL)
* add configurable `duply_bin_path` for cron job command
* add `duply_install_cronic` toggle to disable cronic install if handled elsewhere
* add `.gitattributes` for LF line ending enforcement

### Platform Support

* Amazon Linux 2023 (pip duplicity + source duply + source cronic)
* RHEL/CentOS/Rocky/Alma 7/8/9 (EPEL duplicity + source cronic)
* Ubuntu 18.04, 20.04, 22.04, 24.04 (unchanged, package-based)

### Breaking Changes

* `cronic` removed from Ubuntu `duploy_packages` list (now installed by dedicated task)
* Cron job uses `duply_bin_path` variable instead of bare `duply` command

## [2.1.0](https://github.com/rolehippie/duply/compare/v2.0.0...v2.1.0) (2025-09-29)


### Features

* apply new repo structure and update linting and integrate noble ([cd75a83](https://github.com/rolehippie/duply/commit/cd75a83d141e0baf753aef00f8450aa1664ffaf3))

## [2.0.0](https://github.com/rolehippie/duply/compare/v1.0.0...v2.0.0) (2024-02-12)


### Features

* drop support for ubuntu 18.04 ([e1c947c](https://github.com/rolehippie/duply/commit/e1c947cba61bed299235843ec24b153eea947d62))
* used full qualified collection names ([f6a2d6d](https://github.com/rolehippie/duply/commit/f6a2d6dc66c92084c4b93178e71ae960176d7800))

## 1.0.0 (2023-01-04)


### Features

* restructure workflows and enable automated releases ([3df6a45](https://github.com/rolehippie/duply/commit/3df6a45def6248374c0e07b2f8fe2230d75ef278))
