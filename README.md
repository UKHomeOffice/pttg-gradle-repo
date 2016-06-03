Maven repository for gradle artifacts.

Consume artifacts from this repository into your gradle build using the following repository configuration:

maven { url "https://github.com/UKHomeOffice/pttg-gradle-repo/raw/master/releases" }


Publish artifacts to this repository using the following configuration, and use the publishToGitHub task:

buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'com.layer:gradle-git-repo-plugin:2.0.2'
    }
}

...

apply plugin: 'git-repo'

...

gitPublishConfig {
    org = "UKHomeOffice"
    repo = "pttg-gradle-repo"
    gitUrl = "https://github.com/UKHomeOffice/pttg-gradle-repo.git"
}

publishing {
    repositories {
        maven {
            url "file://${gitPublishConfig.home}/${gitPublishConfig.org}/${gitPublishConfig.repo}/releases"
        }
    }
    publications {
        mavenJava(MavenPublication) {
            from components.java
        }
    }
}
