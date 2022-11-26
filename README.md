# SCONE Operator Samples

# SCONE Custom Resources Quickstart

## Prerequisites

We assume that

- you have [installed the SCONE Operator](https://sconedocs.github.io/2_operator_installation/)
- you have an create a Kubernetes secret `sconefor pulling the container images from repo `registry.scontain.com/scone.cloud`
- you have created the image pull secret [`sconeapps`](https://sconedocs.github.io/registry/#create-an-access-token) for `registry.scontain.com/scone.cloud` in the namespace in which you deploy the instances.

### Create Base Custom Resources: SGXPlugin and LAS and CAS

You can install SGX Plugin, LAS, and a CAS instance with one command:

```bash
kubectl create -f https://raw.githubusercontent.com/scontain/operator-samples/main/base_and_cas.yaml
```

This deploys a production CAS and all necessary SCONE base services. The CAS database is persistent.

!!! note "No Fail-Over to other nodes"
    This CAS instance does support fail-over to another Kubernetes node. Such a fail-over requires the backup-controller to be enabled.

### Create Base Custom Resources: SGXPlugin and LAS

You can install SGX Plugin with `kubectl`:

```bash
kubectl create -f https://raw.githubusercontent.com/scontain/operator-samples/main/base_v1beta1_sgxplugin.yaml
```

LAS from the included sample manifests:

```bash
kubectl create -f https://raw.githubusercontent.com/scontain/operator-samples/main/base_v1beta1_las.yaml
```

These two manifests have reasonable defaults and should work without any modifications for most deployments. The default Kubernetes namespace for the SGX Plugin and LAS is the namespace of the SCONE Operator. The default Kubernetes namespace of the SCONE Operator is `scone`.

In case the defaults do not fit your requirements, you can customize the manifests as described in the [SCONE Custom Resource Definitions](3_resource_definitions.md).

### Create CAS resource

- Install SCONE CAS to your cluster in production mode as follows:

```bash
kubectl -f create https://raw.githubusercontent.com/scontain/operator-samples/main/services_v1beta1_cas.yaml
```

This CAS will use a persistent volume for its database but it does not support a fail-over to a different host.


## References

For more details, see https://sconedocs.github.io/3_resource_definitions/

