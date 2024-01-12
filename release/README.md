![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins

## Purpose
The Purpose of this plugin is to make it easier to use release to complicated repositories such as GCP and GitHub.

## Usage

Just include the plugin into any build you'd like to use it in and assign the appropriate properties.

This plug-in should automatically pick up artifacts marked for publishing. 

__Gradle File__
```groovy
plugins {
    id 'io.github.pacificengine.build.release' version '0.1.0'
}
```

## Properties
### Required Properties
* `project.version` The build version of the project (Example: `1.0.0`)

### Optional Properties
* `project.sign` To determine if the release should be signed (Defaults to only on non-SNAPSHOT builds, `true` will always sign, `false` will never sign)
* `git.maven.repo.url` The maven repo for the git project you want to push the release to (Defaults to System Variable `GIT_MAVEN_URL`)
* `git.project.name` The project name of the git project you want to push the release into (Defaults to `project.name.short`)
* `git.maven.repo.user` The git username (Defaults to System Variable `GIT_USERNAME`)
* `git.maven.repo.key` The git key (Defaults to System Variable `GIT_TOKEN`)
* `gcp.maven.repo.url` The GCP artifactory repository to release to (Defaults to System Variable `GCP_MAVEN_URL`)
* `gcp.maven.repo.user` The GCP username (Defaults to System Variable `GCP_MAVEN_USER`)
* `gcp.maven.repo.key` The GCP key (Defaults to System Variable `GCP_MAVEN_KEY`)