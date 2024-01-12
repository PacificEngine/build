![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins

## Purpose
The Purpose of this plugin is to make it easier to release to complicated repositories such as GCP and GitHub.

This plugin intentionally excludes the default assigned plugin artifact, so you can custom add custom names for the plugins.

If you'd like to include the default assigned plugin artifact, use [io.github.pacificengine.build.release](../../release/README.md) instead.

## Examples

* [io.github.pacificengine.build.docker](https://github.com/PacificEngine/build/tree/main/docker)
* [io.github.pacificengine.build.java](https://github.com/PacificEngine/build/tree/main/java)
* [io.github.pacificengine.build.plugin.groovy](https://github.com/PacificEngine/build/tree/main/plugin/groovy)
* [io.github.pacificengine.build.plugin.release](https://github.com/PacificEngine/build/tree/main/plugin/release)
* [io.github.pacificengine.build.release](https://github.com/PacificEngine/build/tree/main/release)
* [io.github.pacificengine.build.repository](https://github.com/PacificEngine/build/tree/main/repository)
* [io.github.pacificengine.build.zip](https://github.com/PacificEngine/build/tree/main/zip)

## Usage

Just include the plugin into any build you'd like to use it in and assign the appropriate properties.

__Gradle File__
```groovy
plugins {
    id 'io.github.pacificengine.build.plugin.groovy' version '0.1.0'
    id 'io.github.pacificengine.build.plugin.release' version '0.1.0'
    id 'com.gradle.plugin-publish' version "1.2.1"
}
```

## Properties
### Required Properties
* `project.group` The group the archive belongs to (Example: `io.github.PacificEngine`)
* `project.name` The name of the project (Should be automatically assigned by gradle) (Example: `zipper`)
* `project.version` The build version of the project (Example: `1.0.0`)

### Optional Properties
* `project.sign` To determine if the release should be signed (Defaults to only on non-SNAPSHOT builds, `true` will always sign, `false` will never sign)
* `plugin.artifact.group` The group to assign the plugin artifact in maven (Defaults to `project.group`)
* `plugin.artifact.id` The artifact id to assign the plugin artifact in maven (Defaults to `${rootProject.name}-${project.name}`)
* `plugin.artifact.version` The version id to assign the plugin artifact in maven (Defaults to `project.version`)
* `git.maven.repo.url` The maven repo for the git project you want to push the release to (Defaults to System Variable `GIT_MAVEN_URL`)
* `git.project.name` The project name of the git project you want to push the release into (Defaults to `project.name.short`)
* `git.maven.repo.user` The git username (Defaults to System Variable `GIT_USERNAME`)
* `git.maven.repo.key` The git key (Defaults to System Variable `GIT_TOKEN`)
* `gcp.maven.repo.url` The GCP artifactory repository to release to (Defaults to System Variable `GCP_MAVEN_URL`)
* `gcp.maven.repo.user` The GCP username (Defaults to System Variable `GCP_MAVEN_USER`)
* `gcp.maven.repo.key` The GCP key (Defaults to System Variable `GCP_MAVEN_KEY`)
