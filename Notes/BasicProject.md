# What’s in a basic project?

When scaffolding out a new project, Kubebuilder provides us with a few basic pieces of boilerplate.

## Build Infrastructure

First up, basic infrastructure for building your project:
- go.mod: A new Go module matching our project, with basic dependencies
- Makefile: Make targets for building and deploying your controller
- PROJECT: Kubebuilder metadata for scaffolding new components

## Launch Configuration

We also get launch configurations under the `config/` directory. Right now, it just contains Kustomize YAML definitions required to launch our controller on a cluster, but once we get started writing our controller, it’ll also hold our CustomResourceDefinitions, RBAC configuration, and WebhookConfigurations.

`config/default` contains a Kustomize base for launching the controller in a standard configuration.

Each other directory contains a different piece of configuration, refactored out into its own base:
- `config/manager`: launch your controllers as pods in the cluster
- `config/rbac`: permissions required to run your controllers under their own service account

## The Entrypoint

Last, but certainly not least, Kubebuilder scaffolds out the basic entrypoint of our project: main.go.
