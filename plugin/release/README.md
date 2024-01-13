![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/build?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/build?label=last%20release&style=flat-square)

# How To Utilize Plugins
## Purpose
The Purpose of this plugin is to make it easier to release to complicated repositories such as GCP and GitHub.

This plugin intentionally excludes the default assigned plugin artifact, so you can custom add custom names for the plugins.

If you'd like to include the default assigned plugin artifact, use [io.github.pacificengine.build.release](../../release/README.md) instead.

## Example Projects
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
* `plugin.artifact.group` The group to assign the plugin artifact in maven (Defaults to `plugin.id` otherwise `project.archive.group` otherwise `project.group`)
* `plugin.artifact.id` The artifact id to assign the plugin artifact in maven (Defaults to `${plugin.id}.gradle.plugin` otherwise `project.archive.name` otherwise `${rootProject.name}-${project.name}`)
* `plugin.artifact.version` The version id to assign the plugin artifact in maven (Defaults to `project.version`)

#### Git Maven
* `git.maven.repo.url` The maven repo for the git project you want to push the release to
* `git.maven.url` Utilized if `git.maven.repo.url` is not defined. It is the base url for git maven commits (Defaults to System Variable `GIT_MAVEN_URL`)
* `git.project.name` Utilized if `git.maven.repo.url` is not defined. The project name of the git project you want to push the release into (Defaults to `project.name.short`)``
* `git.maven.repo.user` The git username (Defaults to System Variable `GIT_USERNAME`)
* `git.maven.repo.key` The git key (Defaults to `git.repo.key` otherwise to System Variable `GIT_TOKEN`)

#### Git Tagging
* `git.tag.auto` Should a tag be pushed on every non-SNAPSHOT publish (Defaults to `false`)
* `git.tag.id` The identifier to use for the tag (Defaults to `<%VERSION%>`)
* `git.tag.message` The commit message to use for the tag (Defaults to `Release <%VERSION%>`)
* `git.executable.path` The executable to run git commands (Defaults to System Variable `GIT_EXECUTABLE` otherwise `git`)
* `git.tag.repo` A list of repositories to write the tag to [`;` Delimited] (Defaults to `origin`)

#### GitHub Release
* `git.release.auto` Should a release be pushed on every non-SNAPSHOT publish (Defaults to `false`)
* `git.api.repo.url` The maven repo for the git project you want to push the release to
* `git.api.url` Utilized if `git.api.repo.url` is not defined. It is the base url for git maven commits (Defaults to System Variable `GIT_API_URL`)
* `git.project.name` Utilized if `git.api.repo.url` is not defined. The project name of the git project you want to push the release into (Defaults to `project.name.short`)``
* `git.api.repo.key` The git key (Defaults to `git.repo.key` otherwise to System Variable `GIT_TOKEN`)
* `git.release.name` The name of the release (Defaults to `Release <%VERSION%>`)
* `git.release.body` The body of the release
* `git.release.draft` Should the release be marked as a draft (Defaults to `false`)
* `git.release.prerelease` Should the release be marked as a pre-release (Defaults to `false`)
* `git.release.notes` Should the release use automatically generated notes (Defaults to `true`)
* `git.release.category` The discussion categories of the release
* `git.release.latest` Should the release be marked as latest (GitHub defaults this to `true`)

#### GCP Maven
* `gcp.maven.repo.url` The GCP artifactory repository to release to (Defaults to System Variable `GCP_MAVEN_URL`)
* `gcp.maven.repo.user` The GCP username (Defaults to System Variable `GCP_MAVEN_USER`)
* `gcp.maven.repo.key` The GCP key (Defaults to System Variable `GCP_MAVEN_KEY`)