---
layout: default
---

# Pull Request Workflow

Instead of commiting directly to the __master__ branch in the kuali-student hosted repository you should create a feature branch in your _fork_ of the kuali-student host repository.

You're fork's branch can be linked through Github back to the original repository by filing a pull request against the original repository.

## Code Review

By filing a pull request you can allow for code review of your changes before they are merged.  

Developers with Write access to a repository have the power to merge contributed pull-requests.

# Automated Pull Request CI

The original intent of the Kuali Student migration to github was to use CI on feature branches to vet changes before
they were committed to trunk and could break things for simple to check reasons.

We were evaluating running these checks:

1. Does the code compile?
2. Do the unit tests work?
2.1 Detect which modules changed and run the per module unit tests aswell.
3. Are there sql changes?
3.1 Does the manual impex process work
3.2 Can a previous pull-request build's impex data be resused?
4. Can the application be built
5. Can the application be deployed in Tomcat
6. Do the smoke test automated functional tests pass

Scripts were developed that invoked the <b>git-workflow-maven-plugin</b> and the <b>fusion-maven-plugin</b> for this process against the fused enrollment_aggregate_trunk.

Acting upon the results of these checks was never implemented but in most cases if there is sign-off then the change should be automatically merged into the __master__ branch.  In a post successful build action.




