# helm-summit-notes
Helm Summit notes from February 2018
Table 1, Round 3.
RBAC friendly Tiller

## Raised issues:

1. Tiller requires admin permission (GOD MODE) for operations.
2. With access to Tiller, user can user Tiller's permissions, not user's own set permissions
3. There is no clear way of access/object creation auditing.

## Proposals:

1. Start using Impersonation API in Tiller. https://kubernetes.io/docs/admin/authentication/#user-impersonation
Discussion log:
```
SA creation and assigning permissions
tiller uses provided SA for app deployment
I'm user X and go use that SA account.
Impersonation API. whats missing and can it be used by tiller. there is no way of checking who was who and see what was created.
Impersonation api is not stable enough.
```

2. Pass rendered YAMLs back to the client and use kubctl to create actual objects.
Discussion log:
```
passing back from tiller and run kubectl
helm has to have credentials.
pass credentials to use and check if allowed to use
```

3. Tiller as CRD controller. No direct iteration with Tiller.
If a user can create CRDs this automatically will allow object creation in that namespace.
Discussion log:
```
tiller is controller watch CRDs and then do it.
policies in tiller, check what about t create.
not allowed to specify SA which elevates permissions.
2 type charts: local and global.
helm release and cluster-helm-release
controller opting-in its permissions.
can secure only 1 namespaces
```

4. Tiller as API server
Discussion log:
```
admission controller checking names who created and who trying to do.
tiller as admission controller.
CR with the field of impersonation a user.
API server (custom) aggregating API you need to use your own etcd.
code is there for crd controller and api server. in bitnami github
```

P.S. @anguslees has working version of Tiller CRD controller and almost ready for API server
