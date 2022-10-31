# Carvel Package template

A template to bootstrap a [Carvel package](https://carvel.dev/kapp-controller/docs/latest/packaging) project.

## Components

* <package_name>

## Prerequisites

* Install the [`kctrl`](https://carvel.dev/kapp-controller/docs/latest/install/#installing-kapp-controller-cli-kctrl) CLI to manage Carvel packages in a convenient way.
* Ensure [kapp-controller](https://carvel.dev/kapp-controller) is deployed in your Kubernetes cluster. You can do that with Carvel
[`kapp`](https://carvel.dev/kapp/docs/latest/install) (recommended choice) or `kubectl`.

```shell
kapp deploy -a kapp-controller -y \
  -f https://github.com/vmware-tanzu/carvel-kapp-controller/releases/latest/download/release.yml
```

## Dependencies

TBD

## Installation

You can install the <package_name_display> package directly or rely on the [Kadras package repository](https://github.com/arktonix/kadras-packages) (recommended choice).

Follow the [instructions](https://github.com/arktonix/kadras-packages) to add the Kadras package repository to your Kubernetes cluster.

If you don't want to use the Kadras package repository, you can create the necessary `PackageMetadata` and
`Package` resources for the <package_name_display> package directly.

```shell
kubectl create namespace carvel-packages
kapp deploy -a <package_name>-package -n carvel-packages -y \
    -f https://github.com/arktonix/<package_name>/releases/latest/download/metadata.yml \
    -f https://github.com/arktonix/<package_name>/releases/latest/download/package.yml
```

Either way, you can then install the <package_name_display> package using [`kctrl`](https://carvel.dev/kapp-controller/docs/latest/install/#installing-kapp-controller-cli-kctrl).

```shell
kctrl package install -i <package_name> \
    -p <package_name>.packages.kadras.io \
    -v <package_version> \
    -n carvel-packages
```

You can retrieve the list of available versions with the following command.

```shell
kctrl package available list -p <package_name>.packages.kadras.io
```

You can check the list of installed packages and their status as follows.

```shell
kctrl package installed list -n carvel-packages
```

## Configuration

The <package_name_display> package has the following configurable properties.

| Config | Default | Description |
|-------|-------------------|-------------|
| `` | `` | Description. |

You can define your configuration in a `values.yml` file.

```yaml
namespace: test
```

Then, reference it from the `kctrl` command when installing or upgrading the package.

```shell
kctrl package install -i <package_name> \
    -p <package_name>.packages.kadras.io \
    -v <package_version> \
    -n carvel-packages \
    --values-file values.yml
```

## Documentation

For documentation specific to <package_name_display>, check out [link](url).

## Supply Chain Security

This project is compliant with level 2 of the [SLSA Framework](https://slsa.dev).

<img src="https://slsa.dev/images/SLSA-Badge-full-level2.svg" alt="The SLSA Level 2 badge" width=200>
