<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#org7610c81">1. Future of Tiller</a>
<ul>
<li><a href="#org95557da">1.1. Overall expectations of Users</a></li>
<li><a href="#org9628262">1.2. Tiller-less Helm</a></li>
<li><a href="#org1c04aff">1.3. Proposal to use CRDs for Helm 3</a></li>
<li><a href="#orgbdc81e4">1.4. Next Steps for CRDs</a></li>
<li><a href="#org9c5d133">1.5. Other Observations</a></li>
</ul>
</li>
</ul>
</div>
</div>

<a id="org7610c81"></a>

# Future of Tiller


<a id="org95557da"></a>

## Overall expectations of Users

-   What are the expectations from our users? Do folks usually have templates rendered, and not look at them after rendering? Or do they make / track changes after rendering?
-   What's the vision and final goal of the project? What are the use-cases we are trying to solve?
-   Helm Power Users say: Hey I need something like Mongo, or redis &#x2013; moves on to how do I orchestrate this deploy &#x2013; moves on to orchestrating lifecycles this way.
-   Using CRDs for Helm 3 and tillerless helm almost sound antithetical to each other.
-   Can we use composible building blocks (Bryan Grants's proposal from earlier in the day)?


<a id="org9628262"></a>

## Tiller-less Helm

-   Do we head towards a Chef Model &#x2013; do we move towards Chef Zero vs. Cookbooks? Why not both? This should be possible.
-   Can we use plugins for the client side pieces?
    -   Currently authoring Helm plugins is a bit painful. There is a separate discussion on how to make this better.
-   Today Tiller deals with serialization, locking, etc. for multiple operations.
    -   v1 to v2 was a move from tillerless to tillerful &#x2013; do we have learnings from this move?
-   Some type of client side rendering can definitely help from a testing perspective


<a id="org1c04aff"></a>

## Proposal to use CRDs for Helm 3

-   Taylor's proposal touches on Application Lifecycle Management (<https://github.com/thomastaylor312/helm-3-crd>) which was pitched earlier during the Summmit.
-   One use case to definitely address &#x2013; having a component that is running all of the time that reconciles the distributed application.
-   Even if and when we do build something like this, the controller should consume libraries that can be injected into the client.
-   There was a strong proposal to eliminate the Lifecycle resource &#x2013; and watching on this resource.
    -   The reason was that we need a more consistent story about LifeCycle Hooks &#x2013; at scale ordering of dependencies doesn't really work well.
-   We haven't really defined what it means to be healthy &#x2013; so how do we define dependencies.
-   Can we use the concept of liveness / readiness that works so well for Pods also for the CRD level.
    -   The right way to do this may be to put this in a Service &#x2013; the semantic of Service readiness is more compelling than of aggregating Pod readiness.


<a id="orgbdc81e4"></a>

## Next Steps for CRDs

-   Eliminate the Lifecycle resource for CRDs &#x2013; and watching on this resource.
-   In the release object, probably makes sense to include a "status" field
    -   Report back the status of the CRD in this field
-   Another idea/suggestion was to have something like an "upgrade in progress" state.
-   Ordering is one use case, determining if an application is healthy is another use case. This would address both to a certain extent.
    -   Taylor: Maybe we can copy the deployment model to use going forward
    -   Taylor: We should be able to change things, we can't remove things as this would not be backwards compatible
-   For current lifecycle hooks, we can possibly write an optional operator that would consume this "state" from the CRD and run currently supported hooks (eg. pre / post-install, etc.)


<a id="org9c5d133"></a>

## Other Observations

-   Helm doesn't currently go all they way there for dependency management for some folks.
-   A lot of feedback was around keeping the scope of Helm small(er).
-   Open Question: How do we define the templating engines in a way that's smart that doesn't lead to drift? Not completely sure how to address this without tiller. eg. we have go-templates registered, but you can change this out to use a different one, is this possible per namespace?
-   Ensure that CRDs address harder problems that need to model state machines. How do multiple controllers solve the serialization problem for something like a state machine? The "state" proposed above can help.
