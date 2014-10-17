---
layout: default
---

# How to extract a subgraph from the original converted repository

The full repository contains build tags along all of the different product streams and branches that were deleted, etc.

While useful in a historical context having so many branches slows git down and makes it complicated to review the project history.

In Git it is the graph that is important.

For the most part you can just take a few key branches and any history that they are connected to (essentially the root of the graph) instead of the build tags and other streams of work (the leaf's of the tree).

This page describes the mechanics of extracting a subset of the archived-from-svn repository.

# Example: Extract CM Contribution Branches from archived-from-svn

The CM Contribution branches were a special aggregate created on top of one of the CM releases.

To support community contributions we should extract all of the CM contribution branches aswell as the CM 2.0.0 release branches.

Then we can convert some of the branches into tags (for things like the build tags and release tags).

## Checkout the full repository locally as a bare repository.

{% highlight shell %}
$ cd git
$ git clone --bare https://github.com/kuali-student/archived-from-svn.git
{% endhighlight %}

## Create the cm-contribution repository locally

```
$ git init --bare cm-contribution
```

## Register the remote in the archived-from-svn repository


{% highlight shell %}
$ cd archived-from-svn
$ git remote add cmc ../cm-contribution
{% endhighlight %}

## Now select the contrib_CM_* prefixed branches and send them to the myplan repo

In the archived-from-svn repository clone run:

```
$ git branch | grep " contrib_CM" | grep -v "@" | xargs git push cmc
```


The conversion process tracked when branches were deleted and suffixed the revision where the delete took place to the name of the branch.  The **grep -v "@"** part excludes any branches that represent deletes as they are not needed.

#### Example of push output
![](images/push-contrib-cm.png)


## Create CM 2.x release tags and push to the cm-contribution repository

### Push the student-2.x release branches to the cm-contribution repository

{% highlight shell %}
$ cd archived-from-svn
$ git branch | grep " enrollment_aggregate_tags_student-2.0." | xargs git push cmc
{% endhighlight %}

### Create tags from the branch and delete the branches

{% highlight shell %}
$ cd cm-contribution
$ git branch | grep " enrollment_aggregate_tags_student-2.0." | less

$ git tag student-2.0.0-cm enrollment_aggregate_tags_student-2.0.0-cm
$ git tag student-2.0.1-cm enrollment_aggregate_tags_student-2.0.1-cm
$ git tag student-2.0.2-cm enrollment_aggregate_tags_student-2.0.2-cm
$ git tag student-2.0.3-cm enrollment_aggregate_tags_student-2.0.3-cm

$ git branch | grep " enrollment_aggregate_tags_student-2.0." | xargs git branch -D

{% endhighlight %}

## Convert build tag branches to git tags

Inside the git-repository-tools/git-importer artifact there is a program called ConvertBuildTagBranchesToGit and it will parse the long structure and create a tag without the leading enrollment_aggregate_tags_builds part.




