utils-java [![Build Status](https://img.shields.io/travis/googlegenomics/utils-java.svg?style=flat)](https://travis-ci.org/googlegenomics/utils-java) [![Coverage Status](https://img.shields.io/coveralls/googlegenomics/utils-java.svg?style=flat)](https://coveralls.io/r/googlegenomics/utils-java)
==========

This project's goal is to reduce duplicate code across different Google Genomics Java integrations. 

If you have duplicate code appearing in your projects, or see useful functions in the other [googlegenomics Java repositories](https://github.com/googlegenomics?query=-java) that you want to depend on, please [contribute](CONTRIBUTING.rst)!

##Depending on this project

Note: you can find the latest available version of this project in [Maven's central repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22google-genomics-utils%22).

### Maven
Add the following to your `pom.xml` file:
```
<project>
  <dependencies>
    <dependency>
      <groupId>com.google.cloud.genomics</groupId>
      <artifactId>google-genomics-utils</artifactId>
      <version>v1beta2-0.1</version>
    </dependency>
  </dependencies>
</project>
```

### Gradle
Add the following to your `build.gradle` file:
```
repositories {
    mavenCentral()
}

dependencies {
    compile 'com.google.cloud.genomics:google-genomics-utils:v1beta2-0.1'
}
```

##The code

* [GenomicsFactory.java](src/main/java/com/google/cloud/genomics/utils/GenomicsFactory.java) makes it easier to construct an authenticated Genomics service
* [Paginator.java](src/main/java/com/google/cloud/genomics/utils/Paginator.java) lazily paginates through readsets, reads, variants and callsets

##Releasing new versions

This section contains details on getting a new release into Maven central and can be safely ignored by most people. If you need a new release of this code, go ahead and just [file an issue](https://github.com/googlegenomics/utils-java/issues/new).

###Prereqs
* [File a ticket](http://central.sonatype.org/pages/ossrh-guide.html#initial-setup) to get access to the Sonatype com.google.cloud.genomics group 
* [Setup gpg](http://central.sonatype.org/pages/working-with-pgp-signatures.html) (Don't forget to publish a public key)
* [Setup GitHub SSH keys](https://help.github.com/articles/generating-ssh-keys) (make sure `ssh -T git@github.com` works)
* Create a `~/.m2/settings.xml` file which has the following:
```
<settings>
  <servers>
    <server>
      <id>ossrh</id>
      <username>sonatype-username</username>
      <password>sonatype-password</password>
    </server>
  </servers>
</settings> 
```

###Making a new release
1. Use Maven to tag the code, up the pom version and release into the Sonatype staging area.
```
mvn release:prepare
mvn release:perform
```
2. Find the repository at https://oss.sonatype.org/#stagingRepositories and close it.
3. If closing succeeds, then release it. See the [detailed instructions](http://central.sonatype.org/pages/releasing-the-deployment.html#close-and-drop-or-release-your-staging-repository) for more info.
4. As long as there aren't any errors - that's it! The new version will be synced to Maven central.
