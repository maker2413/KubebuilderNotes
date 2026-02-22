# Groups, Versions, and Kinds
This document is based on this page of the kubebuilder guide: https://book.kubebuilder.io/cronjob-tutorial/gvks

## Groups and Versions
An API Group in Kubernetes is simply a collection of related functionality. Each group has one or more versions, which, as the name suggests, allow us to change how an API works over time.

## Kinds and Resources
Each API group-version contains one or more API types, which we call Kinds. While a Kind may change forms between versions, each form must be able to store all the data of the other forms, somehow (we can store the data in fields, or in annotations). This means that using an older API version won’t cause newer data to be lost or corrupted. See the [Kubernetes API guidelines](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md) for more information.

You’ll also hear mention of resources on occasion. A resource is simply a use of a Kind in the API. Often, there’s a one-to-one mapping between Kinds and resources. For instance, the `pods` resource corresponds to the `Pod` Kind. However, sometimes, the same Kind may be returned by multiple resources. For instance, the `Scale` Kind is returned by all scale subresources, like `deployments/scale` or `replicasets/scale`. This is what allows the Kubernetes HorizontalPodAutoscaler to interact with different resources. With CRDs, however, each Kind will correspond to a single resource.

Notice that resources are always lowercase, and by convention are the lowercase form of the Kind.

## So, how does that correspond to Go?
When we refer to a kind in a particular group version, we’ll call it a GroupVersionKind, or GVK for short. Same with resources and GVR. As we’ll see shortly, each GVK corresponds to a given root Go type in a package.

Now that we have our terminology straight, we can actually create our API!

## So, how can we create our API?
In the next section, [Adding a new API](https://book.kubebuilder.io/cronjob-tutorial/new-api), we will check how the tool helps us to create our own APIs with the command kubebuilder create api.

The goal of this command is to create a Custom Resource (CR) and Custom Resource Definition (CRD) for our Kind(s). To check it further see; [Extend the Kubernetes API with CustomResourceDefinitions](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/).

## But, why create APIs at all?
New APIs are how we teach Kubernetes about our custom objects. The Go structs are used to generate a CRD which includes the schema for our data as well as tracking data like what our new type is called. We can then create instances of our custom objects which will be managed by our [controllers](https://book.kubebuilder.io/cronjob-tutorial/controller-overview).

Our APIs and resources represent our solutions on the clusters. Basically, the CRDs are a definition of our customized Objects, and the CRs are an instance of it.
