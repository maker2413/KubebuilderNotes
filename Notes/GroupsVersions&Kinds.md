# Groups, Versions, and Kinds

This document is based on this page of the kubebuilder guide: https://book.kubebuilder.io/cronjob-tutorial/gvks

## Groups and Versions
An API Group in Kubernetes is simply a collection of related functionality. Each group has one or more versions, which, as the name suggests, allow us to change how an API works over time.

## Kinds and Resources
Each API group-version contains one or more API types, which we call Kinds. While a Kind may change forms between versions, each form must be able to store all the data of the other forms, somehow (we can store the data in fields, or in annotations). This means that using an older API version won’t cause newer data to be lost or corrupted. See the [Kubernetes API guidelines](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md) for more information.

You’ll also hear mention of resources on occasion. A resource is simply a use of a Kind in the API. Often, there’s a one-to-one mapping between Kinds and resources. For instance, the pods resource corresponds to the Pod Kind. However, sometimes, the same Kind may be returned by multiple resources. For instance, the Scale Kind is returned by all scale subresources, like deployments/scale or replicasets/scale. This is what allows the Kubernetes HorizontalPodAutoscaler to interact with different resources. With CRDs, however, each Kind will correspond to a single resource.

Notice that resources are always lowercase, and by convention are the lowercase form of the Kind.
