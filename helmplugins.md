# Helm Plugins working group


Level set:
---

Plugins should not be opinionated
Plugins should be generic as possible

Creating new flow (for Adam):
- Copy old plugin, changing values, profit

plugin.yaml contains:
- metadata
- hooks
- definition

Plugins are essentially aliases to longer commands
Plugin hooks to directories

`helm install` will fetch remote, run any hooks, link everything in cache directly to $HELM_HOME

`helm plugin install` for local development pointing at directories

When plugin is executed, sets up all environment variables needed

Tiller-side plugins are also possible:
- [rudder](https://github.com/helm/rudder-appcontroller)


## Curating Helm Plugins

Currently, community asks you to
    - add the tag `helm-plugin` to your project in Github
    - submit a PR to [related section](https://github.com/kubernetes/helm/blob/master/docs/related.md#helm-plugins)


Proposed items:
    - helm create for base template of plugins
    - hub.kubeapps.com but for helm plugins
