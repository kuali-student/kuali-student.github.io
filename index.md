---
layout: default
---

# Repositories

## [archived-from-svn](https://github.com/kuali-student/archived-from-svn)

The kuali-student subversion repository contained 77740 revisions between April 2008 and October 2014.

The [git-repository-tools](https://github.com/kuali-student/git-repository-tools) project was used to perform the conversion of the entire repository into a single git repository.  

Most of the other repositories contain a portion of the commit graph contained here.

### Key Alterations

1. To reduce the repository size all .MPX files were modified to remove their content.
2. Two large files were removed to reduce the repository size and pass the github requirement of no files being > 100 MB in size.
3. Commits changed in steps 1 and 2 were rewritted with updated *fusion-maven-plugin.dat* values to allow the fusion-maven-plugin to continue to work.


# Examples

1. [Extract a new Repository from archived-from-svn](examples/extract-new-repo.html)
1. [Configure and Run the fusion-maven-plugin on top level aggregate branches](examples/configure-fusion-maven-plugin.html)

### How to Contribute more Documentation

This site is stored [on github](https://github.com/kuali-student/kuali-student.github.io) using the jekyll ruby site generation framework.  Refer to [Adding new Kuali Student on Github Documentation](site/contribute.html)


