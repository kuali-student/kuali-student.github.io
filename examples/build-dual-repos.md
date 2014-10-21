---
layout: default
---

# Build the Code

Building the code in the dual repository configuration is pretty close to how it is described to be built in the [Kuali Student Developer Guide](https://wiki.kuali.org/display/STUDENTDOC/Kuali+Student+Developer+Guide)

Overview:

1. Clone the repositories
2. Tag the pom version's in both repositories and linked properties.
3. Run manual impex if required
4. Load latest impex data
5. Build the code
6. Deploy the war
7. Run the AFT's


This process is basically the same as we worked out for the [pull-request-processing](https://github.com/kuali-student/pull-request-processing/blob/master/pull-request-builder) repository which was being used in CI to run checks per pull request before allowing them to be merged.

## Clone the repositories

Clone the code repository:

``` git clone https://github.com/kuali-student/ks-development ```

Change to the master branch

``` git checkout master ```

Clone the impex repository:

``` git clone https://github.com/kuali-student/ks-development-impex ```

Change to the master branch

``` git checkout master ```

## Tag Build X

Not required for local development but it is for CI builds.

The master branch in both repositories has been setup with configuration for the fusion-maven-plugin's tag mojo that can be used to change the -SNAPSHOT part of the project versions into something hardened.

For CI running against commits made directly on a branch the build tagging support should be used:

```mvn validate -Dfusion-maven-plugin.tag-build.phase=validate -e -N```

This expects an environment variable BUILD_NUMBER to exist and hold the number of the build.  This would turn 2.1.1-FR2-M1-SNAPSHOT into 2.1.1-FR2-M1-build-${BUILD_NUMBER}.

For CI running against pull requests the pull request tagging support should be used:

```mvn validate -Dfusion-maven-plugin.tag-pull-request.phase=validate -Dfusion-maven-plugin.tag.pull-request-number-property=XYZ -e -N```

This expects an environment variable XYZ (as given) to exist and hold the number of the pull-request.  This would turn 2.1.1-FR2-M1-SNAPSHOT into 2.1.1-FR2-M1-pull-request-${XYZ}.


The pull-request number environment variable parameter is confiurable to give more flexibility incase the CI driving the pull request build needs a different parameter name.


### Both Tag methods are aware of the related version properties

When the tagging is applied it applies to the GAV's of the projects but also certain linked properties.  See the ```<linkedVersionPropertyNames>```

When run on both sides both the GAV's and the referenced projects will be in sync.

## Run unit tests

Follow the script here: [pull-request-builder/run-unit-tests.sh](https://github.com/kuali-student/pull-request-processing/blob/master/pull-request-builder/run-unit-tests.sh)



## Manual Impex Process


Follow the script here: [pull-request-builder/run-manual-impex.sh](https://github.com/kuali-student/pull-request-processing/blob/master/pull-request-builder/run-manual-impex-process.sh)


## Loading Impex Data

The load side assumes that the ks-impex artifacts exist which the .mpx data contained within them.

{% highlight bash %}

cd ks-development

cd ks-deployments/ks-dbs/ks-impex

{% endhighlight %}

### Load Bundled DB

``` mvn initialize -Pdb,oracle,ks-impex-bundled -Dproperties.decrypt=false -o ```

### Load Rice DB

``` mvn initialize -Pdb,oracle,ks-impex-rice -Dproperties.decrypt=false -o ```

### Load App DB

``` mvn initialize -Pdb,oracle,ks-impex-app -Dproperties.decrypt=false -o ```


## Build Code for Deployment

{% highlight bash %}

cd ks-development

mvn clean install -DskipTests -Pbundled-only-war -Dks.gwt.compile.phase=none

{% endhighlight %}


