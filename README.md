# Kubebuilder Practice
This repository exists to just allow me to write notes and build example projects while learning kubebuilder. I would not consider the information in this repository to be accurate, but I like to study in the public so if you find anything interesting here feel free to take it for your own studies.

# Kubebuilder commands
The `kubebuilder` cli is used to generate most of the boilerplate for operator code as well as build out general repository structure like github actions, a Makefile, a Dockerfile, and much more.

Some the important commands to know are the following:
- `kubebuilder init --domain=<domain> --repo=<repo>`: init is what is used to build out the initial scaffolding of a repository.
- `kubebuilder create api --group batch --version v1 --kind CronJob`: The create api command is used to add an api to your operator. In this example we would be creating a new kind called `CronJob` of the group `batch`. More information on creating APIs can be found: [here](https://book.kubebuilder.io/cronjob-tutorial/new-api).

# What is a Kubernetes Operator
An operator is a method of packaging, deploying, and managing a Kubernetes application by extending the Kubernetes API with custom resources and controllers.

A kubernetes controller can be described as code that runs on a loop forever observing the state of the resources your operators are written for. If at any point the state is updated the controller compares the current state to the desired state. Because the controller has to loop forever the code should be idempotent. If it finds that their is a drift between desired state and current state the controller will update it to match desired state.

The loop can be thought of like this:
```
for {
  1. observe()
  2. compare()
  3. update()
}
```

This is called the reconciliation process.

## Reconcile loop

The reconcile loop is loop we described above. We will now go over what a "happy path" for a reconcile loop looks like:
```go
reconcile App {

  // Check if a Deployment for the app exists, if not, create one
  // If there's an error, then restart from the beginning of the reconcile
  if err != nil {
    return reconcile.Result{}, err
  }

  // Check if a Service for the app exists, if not, create one
  // If there's an error, then restart from the beginning of the reconcile
  if err != nil {
    return reconcile.Result{}, err
  }

  // Look for Database CR/CRD
  // Check the Database Deployment's replicas size
  // If deployment.replicas size doesn't match cr.size, then update it
  // Then, restart from the beginning of the reconcile. For example, by returning `reconcile.Result{Requeue: true}, nil`.
  if err != nil {
    return reconcile.Result{Requeue: true}, nil
  }
  ...

  // If at the end of the loop:
  // Everything was executed successfully, and the reconcile can stop
  return reconcile.Result{}, nil

}
```
