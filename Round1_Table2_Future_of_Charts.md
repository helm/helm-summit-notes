<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgb6c0abe">1. Future of Helm Charts</a>
<ul>
<li><a href="#orgc154935">1.1. Topic 1: Should repositories like ChartMuseum signal quality?</a>
<ul>
<li><a href="#orgdd2505e">1.1.1. Ratings</a></li>
<li><a href="#org3501125">1.1.2. Number of Downloads</a></li>
</ul>
</li>
<li><a href="#org00e9147">1.2. Topic 2: Changing the format of the chart index to be more performant .</a></li>
<li><a href="#org33a904c">1.3. Topic 3: Upload of charts directly from the helm CLI</a></li>
</ul>
</li>
</ul>
</div>
</div>

<a id="orgb6c0abe"></a>

# Future of Helm Charts


<a id="orgc154935"></a>

## Topic 1: Should repositories like ChartMuseum signal quality?

For users, it was agreed that it is useful to have some sort of signalling mechanism for quality. There were various proposals made to signal quality of charts &#x2013; each had its benefits and drawbacks.


<a id="orgdd2505e"></a>

### Ratings

-   There are certain problems that arise with using ratings as a quality signalling mechanism
    -   The system can be gamed, folks can ask friends / colleagues to rate things, often means nothing about the actual quality.
    -   Ratings don't work well over a period of time. For eg. if there is a chart with bad ratings, that gets fixed, the bad ratings still persist. Idea - rate every version seperately.
-   Maybe something along the style of Amazon reviews is better than ratings? But then again, this can be gamed &#x2013; see fake Amazon reviews.


<a id="org3501125"></a>

### Number of Downloads

-   How do you know that downloads have been by an actual user vs. something like a CI system?
-   kubeapps hub pulls all of the charts &#x2013; how do you distinguish that from a real person?
-   Any information can be gamed &#x2013; however if you have a million downloads / docker pulls, there is definitely a message there &#x2013; people are finding the chart / image useful!
-   Recently Helm added user agent flags &#x2013; maybe we can use something like this to differentiate from CI? This is worth a follow up.

However, with either of these two options, where is the correct place to store any such info about downloads? Does this belong in the chart repository?

-   Big orgs prefer to use on-premise tools. They need some way of sharing knowledge. Would they need something like this? Might be overkill for them though.


<a id="org00e9147"></a>

## Topic 2: Changing the format of the chart index to be more performant .

-   Upstream issue filed for this &#x2013; Issue 3557: <https://github.com/kubernetes/helm/issues/3557>
-   The original repository file format was based on Debian
    -   It was anticipated that someday we'll reach a scale where we will run into performance issues.
-   If someone wants to propose and move to a v2 repository file format this would be a good contribution
    -   There was a talk from Ankur Chadha (JFrog) that kicked off discussion here.
-   Will moving to a new v2 repository format be a breaking change for search?
    -   Helm search should still work even with this move
-   A problem this would solve for the chart repo - have a distributed index / chart delegation (viglesias).
    -   This would make charts a sort of meta-repo, so kubernetes/charts can have something that it can delegate to instead of growing unsustainably.


<a id="org33a904c"></a>

## Topic 3: Upload of charts directly from the helm CLI

-   It might make sense for the chart upload mechanism to be based on Helm plugins
    -   The plugin interface is confusing today, can we make this better / easier?
    -   Also discovery and downloading the plugins can be problematic (today at least).
    -   Moreover, kubectl has its own plugins and plugin mechanisms
    -   (Completely different side topic &#x2013; Should helm be/have a kubectl plugin interface?)
-   It was mentioned that the plugin conversation is not simple &#x2013; need to follow up with what conversations happend at the plugin table during the Summit (which was a later session).
-   Should "helm push" be added to the base API and not be a plugin? This is a bigger conversation. At the very least this deserves an issue in the Helm issue queue, where folks can weigh in on the idea.
