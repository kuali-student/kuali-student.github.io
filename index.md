---
layout: default
---

# The Kuali Student Project

Kuali Student Website
See: [http://www.kuali.org/ks](http://www.kuali.org/ks)

The [kuali-student github organization](https://github.com/kuali-student) is an effort to maintain the commit history of Kuali Student after development from Kuali.org has stopped.  

At this time (October 2014) there are no plans to maintain the project from the Kuali Foundation, the KualiCo organization, or from any other parties.  

As there have been no decisions regarding timelines, scope, and intent with regards to supporting this codebase from KualiCo and the Kuali Foundation, we are creating this codebase as a means for other communities to support the codebase by making it publicly available.  

If a community forms that wishes to maintain this codebase administration of this github organization and repositories will be transferred to the new community.

## Repositories

See: [Repositories](repositories.html) for a detailed breakdown of the *kuali-student* organization repositories.

The repositories are typically additive where fetching references from more than one will just add in extra leaf branches with a common base.

## Committing Code

At this time, pull requests will remain unpushed until a community forms to govern the review, acceptance, and release policies.

How does this repository relate to svn.kuali.org?

This project is a fork of the Kuali Student SVN repository at revision 77740.

[enrollment_aggregate_tags_builds_2.1_2.1.1-FR2-M1_build-917](https://github.com/kuali-student/archived-from-svn/tree/enrollment_aggregate_tags_builds_student-2.1_2.1.1-FR2-M1_build-917)
 which occurred on October 12th 2014 is considered the milestone for:

1. Curriculium Management 3.0 (ks-lum 3.0 Milestone 1 of Founder's Release 1)
2. Enrolmment 1.0 (ks-enroll Milestone 2 or Founder's Release 2)

It also contains a stable but functionally incomplete Academic Planning Module.  See [https://wiki.kuali.org](https://wiki.kuali.org) for more details.

A fused version of build-917 with the manual impex process reapplied is available from the [ks-final-milestone](https://github.com/kuali-student/ks-final-milestone) repository.  

  
## Building and Running

Steps to build and run the code can be found here: [https://wiki.kuali.org/display/STUDENTDOC/3.+Build+the+Database+and+Code](https://wiki.kuali.org/display/STUDENTDOC/3.+Build+the+Database+and+Code)


Due to limitations of GitHub file sizes we’ve moved the database files to the [ks-development-impex](https://github.com/kuali-student/ks-development-impex) repository so for step 3.2 you’ll need to clone that repo for loading data.  

Continued development of kuali student in Git should use the **ks-development-impex** repository to store the impex files.   For internal use you could fork before impex is split out just don't commit .mpx files back into the repository.  Store them somewhere else like in maven repository or a docker image.

# Examples

1. [Extract a new Repository from archived-from-svn](examples/extract-new-repo.html)
2. [Extract and fuse a single build tag from archived-from-svn](examples/extract-and-fuse-a-build-tag.html)
3. [Configure and Run the fusion-maven-plugin on top level aggregate branches](examples/configure-fusion-maven-plugin.html)
4. [Run the Manual Impex Process](examples/impex.html)

### How to Contribute more Documentation

This site is stored [on github](https://github.com/kuali-student/kuali-student.github.io) using the jekyll ruby site generation framework.  Refer to [Adding new Kuali Student on Github Documentation](site/contribute.html)


