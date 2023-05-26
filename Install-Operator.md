# Installing MongoDB Kubernetes Operator

This guide outlines the steps to install the MongoDB Kubernetes Operator, which allows you to manage MongoDB deployments on Kubernetes.

## Prerequisites

Before proceeding with the installation, ensure that you have the following prerequisites:

- Kubernetes cluster up and running
- `kubectl` command-line tool installed and configured

## Steps

### Step 1: Add the MongoDB Helm Repository

Add the MongoDB Helm repository to your Helm configuration:

```
helm repo add mongodb https://charts.mongodb.com/stable
```
```
helm repo update

```
Step 2: Install the MongoDB Kubernetes Operator
Install the MongoDB Kubernetes Operator using Helm:

```
helm install my-mongodb-operator \
  --namespace my-mongodb \
  --set securityContext.enabled=false \
  --set serviceAccounts.agent.create=false \
  mongodb/mongodb-kubernetes-operator
```  
Adjust the values based on your requirements. In this example, we install the operator in the my-mongodb namespace. The securityContext.enabled=false flag is used for demonstration purposes and can be adjusted based on your security requirements.

Step 3: Verify the Installation
Check the status of the MongoDB Kubernetes Operator deployment:
```
kubectl get pods -n my-mongodb
```
Ensure that the MongoDB Kubernetes Operator pods are running and ready.

[MongoDB Kubernetes Operator Installation Documentation](https://www.mongodb.com/docs/kubernetes-operator/stable/tutorial/install-k8s-operator/#install-k8s)
