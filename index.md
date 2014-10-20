---
layout: default
---

# The Kuali Student Project

Kuali Student Website
See: http://www.kuali.org/ks

The [kuali-student github organization](https://github.com/kuali-student) is an effort to maintain the commit history of Kuali Student after development from Kuali.org has stopped.  

At this time (October 2014) there are no plans to maintain the project from the Kuali Foundation, the KualiCo organization, or from any other parties.  

As there have been no decisions regarding timelines, scope, and intent with regards to supporting this codebase from KualiCo and the Kuali Foundation, we are creating this codebase as a means for other communities to support the codebase by making it publicly available.  

If a community forms that wishes to maintain this codebase administration of this github organization and repositories will be transferred to the new community.

## Repositories

See: [Repositories](repositories.html) for a detailed breakdown of the *kuali-student* organization repositories.

## Committing Code
At this time, pull requests will remain unpushed until a community forms to govern the review, acceptance, and release policies.

How does this repository relate to svn.kuali.org?

This project is a fork of the Kuali Student SVN repo as of the nightly build tag 917 which occurred on October 12th 2014.  

This tag was considered a milestone release (details below).

## State of Applications at the time of forking

This code base originated from https://svn.kuali.org/repos/student/enrollment/trunk.  

Application All commit history has been preserved of Curriculum Management 3.0 (ks-lum Milestone 1 of Founder’s Release 1) 
and Enrollment 1.0 (ks-enroll Milestone 2 of Founder’s Release 2).  

Academic Planning is in a stable but functionally incomplete state (see https:\\wiki.kuali.org for more details).

## Building and Running

Steps to build and run the code can be found here: https://wiki.kuali.org/display/STUDENTDOC/3.+Build+the+Database+and+Code

Due to limitations of GitHub file sizes we’ve moved the database files to https://github.com/kuali-student/ks-development-impex so for step 3.2 you’ll need to clone that repo for loading data.  


# Examples

1. [Extract a new Repository from archived-from-svn](examples/extract-new-repo.html)
1. [Configure and Run the fusion-maven-plugin on top level aggregate branches](examples/configure-fusion-maven-plugin.html)

### How to Contribute more Documentation

This site is stored [on github](https://github.com/kuali-student/kuali-student.github.io) using the jekyll ruby site generation framework.  Refer to [Adding new Kuali Student on Github Documentation](site/contribute.html)


