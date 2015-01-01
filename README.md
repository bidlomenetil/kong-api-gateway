# Kong API Gateway

API gateway implemented in Lua for OpenResty, with plugins, declarative configuration, and an administrative API.

This repository is a separately imported source snapshot of [kong](https://github.com/Kong/kong). Upstream contributors created the imported application; local work is recorded in the commits after the source import. See [Upstream source](UPSTREAM_SOURCE.md) for attribution.

## Read the history accurately

The local history starts with a source import on November 3, 2026. The parent year directory and the “Original project year” field do not establish a historical contribution date or a release tag. The imported upstream commit and release are not recorded in the available provenance file.

## Navigate the source

| Path | Responsibility |
| --- | --- |
| [kong/](kong/) | Gateway runtime and plugins |
| [spec/](spec/) | Busted specifications and fixtures |
| [kong.conf.default](kong.conf.default) | Annotated runtime settings |
| [kong-admin-api.yml](kong-admin-api.yml) | Administrative API definition |
| [Makefile](Makefile) | Development, lint, and test targets |

## Prepare development

Read `kong-latest.rockspec`, `.bazelversion`, and `.requirements` before preparing the Lua/OpenResty and Bazel toolchains. The Makefile includes targets that download build tools; inspect the target before executing it.

The commands below are existing project entry points, to run after their toolchain, dependency, and service prerequisites are ready:

```sh
make lint
make test
```

## Validation scope

The documentation change was checked for local link targets, manifest command references, and whitespace errors. Application builds, dependency installation, and service-backed test suites were not run for this documentation change. These instructions do not establish deployment readiness.

## Preserve upstream licensing

Missing upstream license notices were restored from the official repository. [License restoration](LICENSE_RESTORATION.md) records the retrieval revision, exact source URLs, and SHA-256 hashes. That revision does not identify the imported application snapshot. Read per-file and subtree notices as well as the root license before redistribution. This documentation does not change the license of imported code.

## Install and run locally

After preparing the toolchains declared in the rockspec and Bazel configuration, bootstrap the development environment:

```sh
make dev
cp kong.conf.default kong.conf
```

Edit `kong.conf` for your database connection and listener settings. For a fresh configured database, initialize the schema and start the gateway:

```sh
bin/kong migrations bootstrap -c kong.conf
bin/kong start -c kong.conf
```

For an existing database, use the version-appropriate migration procedure in `UPGRADE.md` instead of bootstrap. Stop the local instance with `bin/kong stop -c kong.conf`.

## Plan a deployment

Review `kong.conf.default`, `kong-admin-api.yml`, and `UPGRADE.md` for listener exposure, database credentials, administration access, and upgrade sequencing. The source build depends on its declared toolchain; a successful documentation check is not a built gateway image.
