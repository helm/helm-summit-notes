# helm-summit-notes
Helm Summit notes from February 2018
Table 3, Round 5.
Tiller storage backends.

## Raised issues:

1. Use external state storage backend for Tiller.
2. CRs size is limited by 1MB (etcd limitations applied to all k8s objects)


## Proposals:

1. Helm 2. There is already a couple of projects to use Postgres, CosmosDB, and Mysql

2. Split current Tiller state into multiple CRs: Values, Chart, Release etc
..* Optimization: Modify Tiller to change/create only new CRs and reuse unchanged.
3. Store refs to external resources in CRs.
..* Possible issues with managing access info for external backends.

!["Tiller design diagramm"]("Tiller design diagramm" "Tiller design diagramm")

Discussion log:
```
for 2.8 there is a way of storing in DB.
helm3 (aka crd controller) possible issues is crd size is 1MB max (k8s object limit )
proposal to store ref to external storage in crd.
issues with access.
helm scheduler (k8s-helm).
reddis or Memcache for tiller
multiple CRDs from tiller. different Kinds. instead of one big one.

reuse of crds like compare if chart changed.
v1 create all. update changes only new things and rec
```
