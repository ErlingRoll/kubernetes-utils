# Kubernetes utils

Skaffold deployment of
- Metrics server
- Dashboard

## Usage

```
skaffold run
```

## Admin account

The release creates a cluster-admin service account with name `.Values.cluster.admin.name` from values.yaml.
This account is used to access the dashboard.


Create cluster proxy to local machine:
```
kubectl proxy
```

Get login token from admin account:
```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep health-admin | awk '{print $1}')
```

Access dashboard at: http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:https/proxy/#/login

Paste token from admin account to login.

Alternatively use your `kubectl` config file usually located at `~/.kube/config`.

If the error: `Internal Error (500): square/go-jose: error in cryptographic primitive` occurs
it usually means the browser cookie is stale.

Source: https://github.com/kubernetes/dashboard/issues/2970#issuecomment-416023429