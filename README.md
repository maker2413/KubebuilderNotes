# Kubebuilder Practice

This repository exists to just allow me to write notes and build example projects while learning kubebuilder.

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

## Reconcile loop

The reconcile loop is loop we described above. We will now go over what a "happy path" for a reconcile loop looks like:
