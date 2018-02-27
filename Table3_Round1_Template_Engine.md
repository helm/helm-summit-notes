# Template Engine

- Factoring out the template engine

- Dynamically overriding charts that are not templated

### Overriding templates

The idea is to override arbitrary bits of YAML

Q: Does that introduce a security issue?

- No?

Idea: Overriding the templates like erb — allow a template override. E.g. specify a path to override.

- Merging problem when the template is not structured well

- Brian L: Using KSonnet instead.

- Generate a diff of one template against another

- Brian G: There’s always something to override, so templating is not as good of an assumption as forking Also using overlays. Merging is done after the rendering has been done.

- This requires additional tooling to detect errors as overlays change

- Applying patches and the diff outcome is the main important artifact

- Version of chart the patch applies to... and wheter it is overriding something new

Q: What about templatizing values files?

Some discussion about sealing values (making them unoverridable without some additional flag).

Q: Do people want to fork packages?

- “I don’t ever want to”

- “In Chef it was a massive rebase problem and maintenance problem”

- Parameterize over forking

- “We have to fork every chart to add things like node selectors... but we don’t want to”

- “Overlays might allow a fast path to upstream”

- “The comparison is incorrect”

- “If I as a user takes a standard config, and I override, I know I am taking responsibility”

- “In the CM world, wrapping a good enough version is the main practice”

- “Often we want to prune down what is configurable”

Proposal: Overlay with a JSON or YAML patch that is applied after the render.

- “It’s a version 0.5 of the idea, but needs cleaner tooling”

Proposal: Make it possible to do other template engines

**Back to template solutions:**

“Is there value in giving hte user choice between pre-render/post-render?”

A pre-render means you can plug in your own values

Proposal: Hooks in template lifecycle hooks pre-/post-template
