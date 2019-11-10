# Connect from k8s to cloud sql using cloud sql proxy

Here are the steps.

## Prerequisites

- A running k8s cluster.
- A second generation Cloud SQL MySQL instance and a connection user.
- A service account key file. This service account has one of Cloud SQL Client, Cloud SQL Editor or Cloud SQL Admin role.
- The Cloud SQL Admin API is enabled.

## Creating Secrets

```
kubectl create secret generic cloudsql-db-credentials --from-literal=username=USERNAME --from-literal=password=PASSWORD
kubectl create secret generic cloudsql-instance-credentials --from-file=./credentials.json
```

## Creating Deployment and Service

Remember to change <INSTANCE_CONNECTION_NAME> with yours.

```
kubectl apply -f wordpress-cloud-sql-deployment.yaml
kubectl apply -f wordpress-cloud-sql-service.yaml
```

## Test

```
kubectl get svc
```

Get the Load Balancer IP address and visit the site. Additionally you should see a wordpress database is created on your MySQL instance.

## References

https://cloud.google.com/sql/docs/mysql/connect-kubernetes-engine

https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/blob/master/cloudsql/mysql_wordpress_deployment.yaml
