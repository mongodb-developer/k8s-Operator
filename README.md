# Deploying a MongoDB Replica Set with MongoDB Kubernetes Operator

This guide outlines the steps to deploy a MongoDB replica set using the MongoDB Kubernetes Operator. The MongoDB Kubernetes Operator simplifies the deployment and management of MongoDB clusters on Kubernetes.

## Prerequisites

Before proceeding with the deployment, ensure that you have the following prerequisites:

- Kubernetes cluster up and running
- `kubectl` command-line tool installed and configured
- MongoDB Kubernetes Operator installed in your cluster

## Steps

### Step 1: Create a Namespace

Create a Kubernetes namespace to isolate the MongoDB resources:
```
kubectl create namespace my-mongodb
```
### Step 2: Create a Secret

Create a Kubernetes secret to store the MongoDB admin credentials:
```
kubectl create secret generic my-mongodb-credentials
--namespace my-mongodb
--from-literal=mongodb-admin-username=<admin_username>
--from-literal=mongodb-admin-password=<admin_password>
```
Replace `<admin_username>` and `<admin_password>` with the desired MongoDB admin username and password.

### Step 3: Deploy the MongoDB Replica Set

Create a YAML file, for example `mongodb-replicaset.yaml`, with the following content:

```yaml
apiVersion: mongodb.com/v1
kind: MongoDB
metadata:
  name: my-mongodb
  namespace: my-mongodb
spec:
  members: 3
  type: ReplicaSet
  version: "6.3.1"
  security:
    authentication:
      modes: ["SCRAM"] 
```      
           
Adjust the configuration based on your requirements, such as the number of replica set members, MongoDB version, and authentication settings.

Deploy the MongoDB replica set:
```
kubectl apply -f mongodb-replicaset.yaml
```
Step 4: Verify the Deployment
Check the status of the MongoDB replica set deployment:
```
kubectl get mongodb -n my-mongodb
```
Ensure that the STATUS is Running and the READY count matches the number of replica set members.

Step 5: Connect to the Replica Set
To connect to the MongoDB replica set, retrieve the connection details:
```
kubectl get mongodb -n my-mongodb -o jsonpath='{.items[0].status.connectionString}'
```
Use the obtained connection string to connect to the replica set from your application or MongoDB client.

Conclusion
In this guide, you successfully deployed a MongoDB replica set using the MongoDB Kubernetes Operator. You can now leverage the power and scalability of MongoDB on Kubernetes for your applications.

[MongoDB Kubernetes Operator Documentation](https://www.mongodb.com/docs/kubernetes-operator/stable/)
