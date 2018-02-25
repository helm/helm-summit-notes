# helm-summit-notes
Helm Summit notes from February 2018
Table 3, Round 4.
Extensions of existing charts.

## Raised issues:

1. How to make changes into existing charts. Without forking and modifying charts repo.
⋅⋅* Add new ladles, annotations, values
..* Add/remove side car[s]

## Proposals:

@omkensey mentioned that this topic was discussed in one of the previous tables (improving experince with charts) and proposal was to start using overlay.
@technosophos said that Helm is supporting overlaying from the begging.

Discussion log:
```
modify charts without breaking it.
add, remove, delete and things.
customizing charts with overlay
proposal from another group: improving experince with charts.
flags, apis.
mostly when k8s changes it takes forever to populate those into repo.

from chart aka docker file

use ksonnet as backend.

add external deps example: once chart is installed helm performs actions from annotation.
post/get query URLs. something like webhooks
```
