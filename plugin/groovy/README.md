![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins
## Purpose
The Purpose of this plugin is to make it easier to create groovy plugins with custom names.

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

### Optional Properties
* `plugin.id` The id of the plugin. Without this assigned, it will default to apply the settings to all plugins. (Example: `io.github.pacificengine.build.plugin.groovy`)
* `plugin.displayName` The display name for the plugin. This is required if you want to release the plugin. (Defaults to `project.name`) (Example: `Gradle Plugin Groovy Plugin`)
* `plugin.description` The description for the plugin. (Example: `A plugin that help you write gradle plugins using groovy`)
* `plugin.implementationClass` The implementation class to use for the plugin (Example: `IOGithubPacificengineBuildPluginGroovyPlugin`)
* `plugin.tags` The tags to use for the plugin [`;` delimited] (Example: `gradle;groovy;build;artifact`)
* `plugin.website.url` The website to use for the plugin. (Defaults to `plugin.url` otherwise `git.repo.url`)
* `plugin.vcs.url` The vcs url to use for the plugin. (Defaults to `plugin.url` otherwise `git.repo.url`)