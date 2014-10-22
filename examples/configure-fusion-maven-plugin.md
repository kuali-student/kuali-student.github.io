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

The fuse mojo takes the branch and puts that tree into a directory of the same name of the __module__ in
the aggregate branch.

In order to be able to fuse and split the mappings need to be setup in the pom.xml file.

If you only intend to fuse but never split you can just fuse using the fusion-maven-plugin.dat file contents.

Although that file is only guaranteed accurate for build tags.  For trunks and feature branches it can be out of date (it is only updated when there is a commit on the aggregate branch, so doesn't capture changes made only to a module branch).


{% highlight xml %}
    <plugins>
	<plugin>
            <groupId>org.kuali.maven.plugins</groupId>
            <artifactId>fusion-maven-plugin</artifactId>
	    <version>${fusion-maven-plugin.version}</version>
            <configuration>
                <mappings>
		    <!-- Add a mapping for each directory and source branch -->
                    <mapping>
                        <module>ks-api</module>
			<branchName>
				contrib_CM_ks-api_branches_org-service  <!-- change this to the actual name of the source branch. -->
			</branchName>
                        <versionProperty>
				ks.api.version
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

