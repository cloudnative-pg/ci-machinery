[![CloudNativePG](./logo/cloudnativepg.png)](https://cloudnative-pg.io/)

# CI Machinery for CloudNativePG

A unified set of CI tasks shared across the projects of the CloudNativePG
ecosystem, such as the
[CloudNativePG operator](https://github.com/cloudnative-pg/cloudnative-pg),
the [Barman Cloud Plugin](https://github.com/cloudnative-pg/plugin-barman-cloud)
and [Klio](https://github.com/cloudnative-pg/klio).

As the CloudNativePG ecosystem grows, it is no longer affordable for each
project to define its own way of running CI. Maintaining separate, slightly
different implementations of the same tasks costs time, makes pipelines less
stable, and leads to conflicts and drift between projects at both development
and release time.

CI Machinery centralizes those tasks in a single place, so they are written,
fixed and improved once and benefit every project in the ecosystem.

Ideally, this repository will also provide a generic and reusable way to set
up test environments. Today, that logic is duplicated in every project, such
as CloudNativePG itself, the Barman Cloud Plugin, Klio, the Helm charts and the
CNPG Playground.

## Usage

CI Machinery is meant to be used as a library: each project integrates it by
referencing the shared [Taskfile](https://taskfile.dev/) definitions remotely,
instead of copying them into its own repository.

```yaml
# renovate: datasource=github-tags depName=go-task/task versioning=semver
version: 3.54.0

includes:
  olm: https://github.com/cloudnative-pg/ci-machinery.git//taskfiles/taskfile.olm.yaml?ref=main
  infra: https://github.com/cloudnative-pg/ci-machinery.git//taskfiles/taskfile.infra.yaml?ref=main
  renovate: https://github.com/cloudnative-pg/ci-machinery.git//taskfiles/taskfile.renovate.yaml?ref=main
```

The included tasks are then available under their namespace, e.g.
`task renovate:validate`. Run `task --list` to see them all.

## Contributing

Please read the [contributing guidelines](./CONTRIBUTING.md), the
[governance model](./GOVERNANCE.md) and the
[code of conduct](./CODE_OF_CONDUCT.md) before contributing.

## License

This code is released under the [Apache License 2.0](./LICENSE).
