# Spring Boot Conventions

![Test Workflow](https://github.com/kadras-io/package-for-spring-boot-conventions/actions/workflows/test.yml/badge.svg)
![Release Workflow](https://github.com/kadras-io/package-for-spring-boot-conventions/actions/workflows/release.yml/badge.svg)
[![The SLSA Level 3 badge](https://slsa.dev/images/gh-badge-level3.svg)](https://slsa.dev/spec/v1.0/levels)
[![The Apache 2.0 license badge](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Follow us on Twitter](https://img.shields.io/static/v1?label=Twitter&message=Follow&color=1DA1F2)](https://twitter.com/kadrasIO)

A Carvel package for the [Spring Boot Convention Server](https://github.com/kadras-io/spring-boot-conventions), a component that works with [Cartographer Conventions](https://github.com/vmware-tanzu/cartographer-conventions) to apply best-practices to workloads at runtime by understanding the developer's intent. It is a key component to build application-aware platforms rather than forcing applications to be platform-aware.

## 🚀&nbsp; Getting Started

### Prerequisites

* Kubernetes 1.26+
* Carvel [`kctrl`](https://carvel.dev/kapp-controller/docs/latest/install/#installing-kapp-controller-cli-kctrl) CLI.
* Carvel [kapp-controller](https://carvel.dev/kapp-controller) deployed in your Kubernetes cluster. You can install it with Carvel [`kapp`](https://carvel.dev/kapp/docs/latest/install) (recommended choice) or `kubectl`.

  ```shell
  kapp deploy -a kapp-controller -y \
    -f https://github.com/carvel-dev/kapp-controller/releases/latest/download/release.yml
  ```

### Dependencies

Spring Boot Conventions requires the [Cartographer](https://github.com/kadras-io/package-for-cartographer) and [cert-manager](https://github.com/kadras-io/package-for-cert-manager) packages. You can install them from the [Kadras package repository](https://github.com/kadras-io/kadras-packages).

### Installation

Add the Kadras [package repository](https://github.com/kadras-io/kadras-packages) to your Kubernetes cluster:

  ```shell
  kctrl package repository add -r kadras-packages \
    --url ghcr.io/kadras-io/kadras-packages \
    -n kadras-packages --create-namespace
  ```

<details><summary>Installation without package repository</summary>
The recommended way of installing the Spring Boot Conventions package is via the Kadras <a href="https://github.com/kadras-io/kadras-packages">package repository</a>. If you prefer not using the repository, you can add the package definition directly using <a href="https://carvel.dev/kapp/docs/latest/install"><code>kapp</code></a> or <code>kubectl</code>.

  ```shell
  kubectl create namespace kadras-packages
  kapp deploy -a spring-boot-conventions-package -n kadras-packages -y \
    -f https://github.com/kadras-io/package-for-spring-boot-conventions/releases/latest/download/metadata.yml \
    -f https://github.com/kadras-io/package-for-spring-boot-conventions/releases/latest/download/package.yml
  ```
</details>

Install the Spring Boot Conventions package:

  ```shell
  kctrl package install -i spring-boot-conventions \
    -p spring-boot-conventions.packages.kadras.io \
    -v ${VERSION} \
    -n kadras-packages
  ```

> **Note**
> You can find the `${VERSION}` value by retrieving the list of package versions available in the Kadras package repository installed on your cluster.
> 
>   ```shell
>   kctrl package available list -p spring-boot-conventions.packages.kadras.io -n kadras-packages
>   ```

Verify the installed packages and their status:

  ```shell
  kctrl package installed list -n kadras-packages
  ```

## 📙&nbsp; Documentation

Documentation, tutorials and examples for this package are available in the [docs](docs) folder.
For documentation specific to Cartographer Conventions, check out [github.com/vmware-tanzu/cartographer-conventions](https://github.com/vmware-tanzu/cartographer-conventions).

## 🎯&nbsp; Configuration

The Spring Boot Conventions package can be customized via a `values.yml` file.

  ```yaml
  namespace: spring-boot-conventions
  ```

Reference the `values.yml` file from the `kctrl` command when installing or upgrading the package.

  ```shell
  kctrl package install -i spring-boot-conventions \
    -p spring-boot-conventions.packages.kadras.io \
    -v ${VERSION} \
    -n kadras-packages \
    --values-file values.yml
  ```

### Values

The Spring Boot Conventions package has the following configurable properties.

<details><summary>Configurable properties</summary>

| Config | Default | Description |
|-------|-------------------|-------------|
| `namespace` | `spring-boot-conventions` | The namespace where to install Spring Boot Conventions. |
| `resources.limits.cpu` | `100m` | CPU limits for the Convention Server. |
| `resources.limits.memory` | `256Mi` | Memory limits for the Convention Server. |
| `resources.requests.cpu` | `100m` | CPU requests for the Convention Server. |
| `resources.requests.memory` | `20Mi` | Memory requests for the Convention Server. |

</details>

## 🛡️&nbsp; Security

The security process for reporting vulnerabilities is described in [SECURITY.md](SECURITY.md).

## 🖊️&nbsp; License

This project is licensed under the **Apache License 2.0**. See [LICENSE](LICENSE) for more information.
