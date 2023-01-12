# Creating a Kubernetes cluster

Please choose a Kubernetes cluster compatible with the Calico Cloud [system requirements](https://docs.calicocloud.io/get-started/requirements/system-requirements).

## Install Calico Open Source

Please refer to the Calico Open Source documentation for instructions on how to [install Calico with Helm](https://projectcalico.docs.tigera.io/getting-started/kubernetes/helm).

### Managed Kubernetes Shortcuts

```
helm repo add projectcalico https://projectcalico.docs.tigera.io/charts
kubectl create namespace tigera-operator
```

Amazon Elastic Kubernetes Service (EKS)

```
helm install calico projectcalico/tigera-operator --version v3.23.5 -f misc/values-eks-aws-cni.yaml --namespace tigera-operator
```

Microsoft Azure Kubernetes Service (AKS)

```
helm install calico projectcalico/tigera-operator --version v3.23.5 -f misc/values-aks-azure-cni.yaml --namespace tigera-operator
```

Confirm all the pods are ready

```
watch kubectl get pods -n calico-system
```

Confirm all the nodes are ready

```
kubectl get nodes
```

[Next -> Module 2](calicocloud.md)
