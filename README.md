# Dev Containers

Pre-build [Development Containers](https://containers.dev/)

<!-- toc -->

* [Purpose](#purpose)
* [Images](#images)
  * [Base](#base)
  * [Full](#full)
* [Usage](#usage)
  * [Adding new features](#adding-new-features)
  * [Lifecycle scripts](#lifecycle-scripts)
  * [It's just Docker](#its-just-docker)
* [Contributing](#contributing)
  * [Open in a container](#open-in-a-container)

<!-- Regenerate with "pre-commit run -a markdown-toc" -->

<!-- tocstop -->

## Purpose

This is a series of pre-built Dev Container images to enable local development.
This allows us to ship the development environment as part of our source code,
meaning that we can onboard new developers quickly and open-source contributors
can get working really quickly.

## Images

There are a number of images that exist and each have slightly different purposes.
These images are rebuilt weekly to ensure that they have all the latest-and-greatest
bugfixes and improvements.

### Base

> `ghcr.io/kubefirst/devcontainers/base`

This provides a base image to use for all your development environment need.
This is an Ubuntu image with sensible defaults, including
[the best-looking Git diffs](https://github.com/so-fancy/diff-so-fancy),
Docker support, tab-completion and useful Git aliases.

### Full

> `ghcr.io/kubefirst/devcontainers/full`

An image with the main Kubefirst tooling installed.

* [Go](https://github.com/devcontainers/features/tree/main/src/go) ✅
* [Homebrew](https://github.com/meaningful-ooo/devcontainer-features/tree/main/src/homebrew)
  ✅
* [Kubernetes and Helm](https://github.com/devcontainers/features/tree/main/src/kubectl-helm-minikube)
  ✅
* [Kubectx](https://github.com/devcontainers-contrib/features/tree/main/src/kubectx-kubens)
  ✅
* [K9s](https://github.com/rio/features/tree/main/src/k9s) ✅
* [mkcert](https://github.com/devcontainers-contrib/features/tree/main/src/mkcert)
  ✅
* [Node.js](https://github.com/devcontainers/features/tree/main/src/node) ✅
* [Pre-Commit](https://github.com/devcontainers-contrib/features/tree/main/src/pre-commit)
  ✅
* [Python](https://github.com/devcontainers/features/tree/main/src/python) ✅
* [Terraform](https://github.com/devcontainers/features/tree/main/src/terraform)
  ✅

The advantage of using this image is that the features are pre-built which shifts
the build effort into GitHub Actions rather than on your local machine.

This can be easily extended with additional features by adding them to your
`.devcontainer/devcontainer.json` file.

## Usage

These images can be used in any way that Dev Containers supports. Typically,
this would be by specifying the `image` in your `devcontainer.json` file:

```json
{
  "name": "devcontainer",
  "image": "ghcr.io/kubefirst/devcontainers/full",
  "features": {}
}
```

As this image is pre-built, it will vastly speed up your workflow. The recommended
workflow is to pull the image separately (eg, `docker pull ghcr.io/kubefirst/devcontainers/full`),
but it is not a requirement.

### Adding new features

Sometimes, this will be used in a project and a feature is required just for
that. You can easily add additional languages or tooling to your Dev Container
by adding to your `features` object. For example, if you wanted to add Rust to
your container, all you have to do is add:

```json
{
  "features": {
    "ghcr.io/devcontainers/features/rust:1": {}
  }
}
```

Additional features can be found on the [Dev Container Features](https://containers.dev/features)
page.

### Lifecycle scripts

You can also use the [lifecycle scripts](https://containers.dev/implementors/json_reference/#lifecycle-scripts)
to run arbitrary commands when your container is run:

```json
{
  "postAttachCommand": {
    "mkcertInstall": "mkcert -install"
  }
}
```

You are advised to use the object notation for the lifecycle scripts so that additional
scripts may be added in future.

### It's just Docker

Ultimately, Dev Containers are just Docker containers run in a way that your IDE
is able to manage. If you wish to connect to the container via your terminal,
simply running `docker exec -it -n <container-id>` will get you in there.

## Contributing

### Open in a container

* [Open in a container](https://code.visualstudio.com/docs/devcontainers/containers)
