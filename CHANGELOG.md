# Changelog

## [3.3.0](https://github.com/morgenn/ansible-role-duply/compare/v3.2.0...v3.3.0) (2026-05-31)


### Features

* add `duply_nice_prefix` for CPU/IO priority limiting (nice -n 19 + ionice -c3)
* move cron job command to configurable `duply_cron_job_template` variable
* add `TEMP_DIR` to duply config template via `duply_default_temp_dir`
* create temp directory task (skips /tmp and /var/tmp, uses 1777 permissions)

### Fixes

* fix stray "exit" text in log output (use `(exit $RC)` subshell instead of `exit $RC`)
* add `pexpect` to AL2023 pip packages (runtime dependency of duplicity)
* remove `gnupg2` from AL2023 packages (conflicts with pre-installed gnupg2-minimal)
* fix pip install to support `extra_args` dict format for `--no-deps`


### Features

* add configurable backup logging to file (duply_log_dir)
* add MAX_FULLBKP_AGE for automatic weekly full backups
* change default strategy to daily incremental with weekly full cycle
* deploy README-recovery.md to /etc/duply/ with restore examples
* cron job logs all output (success + failure) with [FAILED] marker on error
* three cron modes: log-to-file (default), cronic-only, or bare command
* fix pip install --no-deps for AL2023 duplicity (avoids dependency hell)


## [3.1.0](https://github.com/morgenn/ansible-role-duply/compare/v3.0.0...v3.1.0) (2026-05-31)


### Features

* add WordPress DB dump pre/post templates
* support pre_template/post_template for Jinja2 template rendering
* configurable dump name via db_dump_name profile variable
* compressed dumps in docroot/secure/ (Shibboleth-protected)


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
