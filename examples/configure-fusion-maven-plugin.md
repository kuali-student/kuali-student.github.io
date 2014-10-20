---
layout: default
---

# The fusion-maven-plugin 

## Background

In many git workflows the different logical modules that share the same subversion repository are split into seperate git repositories.

When split into seperate modules the git *submodule* feature can be used to connect the child projects as subdirectories under the aggregate branch.

In the kuali student git conversion we left open the option to not split out the different modules by creating a JGit multiple subtree merge function (implemented in the *fusion-maven-plugin*'s fuse mojo).

The git-repositry-tools:git-exporter artifact notices which directories have **svn:externals** properties set and will create a **fusion-maven-plugin.dat** file in the equivilent git branch.  

The fusion can be made against the latest commit on a certain named branch (typically what you want went fusing trunk branches) but can also be locked onto a specific commit object id (this is useful for build tags for example).

The code for the fusion-maven-plugin is hosted in the kuali foundation repository (not yet converted to git) [here](http://svn.kuali.org/repos/foundation/trunk/fusion-maven-plugin/).

We wanted to support development on a fused branch (so that the developer perspective would remain the same) with all of the different modules materialized and editable.

The idea was that developers would create feature branches from this *fused* branch and then file github pull-requests atainst the fused branch.

Then in the process of applying the changes the SplitMojo would be used to create commits for each changed module and then those merged down into the individual module branches.

We intended for the modules to be tagged and then refused back into a  merged branch that would become the new stable commit on the fused branch.

<!-- TODO: add in some documentation here -->

# Using the fusion-maven-plugin

Several Mojo's exist but most were experimental.

1. Fuse Mojo will create a commit containing reaslized subdirectories for each named module.
2. Split Mojo will create a commit for each module from a fused base.  This is needed so that the per module part can be merged back into the per module branches.
3. Tag Mojo will rewrite the project pom versions (allowing for different modules to have different versions) and support the impex version aswell.

## Mappings

### Setup properties 

{% highlight pom %}
<fusion-maven-plugin.version>0.0.4</fusion-maven-plugin.version>
<fusion-maven-plugin.fuse.phase>none</fusion-maven-plugin.fuse.phase>
{% endhighlight %}

### Remove externals-maven-plugin configuration from ```<pluginManagement>``` section


### Add fusion-maven-plugin definition to the ```<plugins>``` section


{% highlight xml %}
    <plugins>
	<plugin>
            <groupId>org.kuali.maven.plugins</groupId>
            <artifactId>fusion-maven-plugin</artifactId>
	    <version>${fusion-maven-plugin.version}</version>
            <configuration>
                <mappings>
                    <mapping>
                        <module>ks-api</module>
			<branchName>
				contrib_CM_ks-api_branches_org-service
			</branchName>
                        <versionProperty>
				ks.api.version
			</versionProperty>
                    </mapping>
                    <mapping>
                        <module>ks-core</module>
			<branchName>
				contrib_CM_ks-core_branches_org-service
			</branchName>
                        <versionProperty>
				ks.core.version
			</versionProperty>
                    </mapping>
                    <mapping>
                        <module>ks-lum</module>
			<branchName>
				contrib_CM_ks-lum_branches_org-service
			</branchName>
                        <versionProperty>
				ks.lum.version
			</versionProperty>
                    </mapping>
                    <mapping>
                        <module>ks-deployments</module>
			<branchName>
				contrib_CM_ks-deployments_branches_org-service
			</branchName>
                        <versionProperty>
				ks.deployments.version
			</versionProperty>
                    </mapping>
                </mappings>
            </configuration>

	    <executions>
            	<execution>
                	<id>fuse</id>
                        <goals>
	                    <goal>fuse</goal>
        	        </goals>
                	<phase>${fusion-maven-plugin.fuse.phase}</phase>
			<!-- run this on the command line:  mvn validate -->
			<!-- -Dfusion-maven-plugin.fuse.phase=validate -e -N -->
			<configuration>
				<!-- instead of using the branch mappings use
				<!-- the fusion data file -->
				<preferFusionDataFile>
					true
				</preferFusionDataFile>
			</configuration>
		</execution>
	    </executions>

        </plugin>

    </plugins>
{% endhighlight %}

## FuseMojo

The fuse mojo uses JGit combined with the git-repository-tools-common artifact to create the fused merge commit.

The *<mappings>* section in the pom.xml is used to specify the name of the directory to materialize within the aggregate and also the source branch to use.

The fusion-maven-plugin.dat file if it exists tries to provide the exact git commit id's to use (i.e. what those branches specified in the svn:externals pointed at the last time there was a commit into the aggregate).

## Split Mojo

## Tag Mojo
