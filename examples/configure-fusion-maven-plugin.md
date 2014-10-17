---
layout: default
---

# The fusion-maven-plugin 

## Background

In may git workflows the different logical modules that share the same subversion repository are split into seperate git repositories.

When split into seperate modules the git *submodule* feature can be used to connect the child projects as subdirectories under the aggregate branch.

In the kuali student git conversion we left open the option to not split out the different modules.

## fusion-maven-plugin 

In the current kuali-student conversion the *fusion-maven-plugin* can be used for the same effect.  It uses either the fusion-maven-plugin.dat file created during the export or allows the different branches to be used as sub directories to be specified in the projects pom.xml file.

The code for the fusion-maven-plugin is hosted in the kuali foundation repository (not yet converted to git) [here](http://svn.kuali.org/repos/foundation/trunk/fusion-maven-plugin/).

We wanted to support development on a fused branch (so that the developer perspective would remain the same) with all of the different modules materialized and editable.

The idea was that developers would create feature branches from this *fused* branch and then file github pull-requests atainst the fused branch.

Then in the process of applying the changes the SplitMojo would be used to create commits for each changed module and then those merged down into the individual module branches.

We intended for the modules to be tagged and then refused back into a  merged branch that would become the new stable commit on the fused branch.

<!-- TODO: add in some documentation here -->

### FuseMojo

The fuse mojo uses JGit combined with the git-repository-tools-common artifact to create the fused merge commit.

The *<mappings>* section in the pom.xml is used to specify the name of the directory to materialize within the aggregate and also the source branch to use.

The fusion-maven-plugin.dat file if it exists tries to provide the exact git commit id's to use (i.e. what those branches specified in the svn:externals pointed at the last time there was a commit into the aggregate).


