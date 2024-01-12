![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins

## Purpose
The Purpose of this plugin is to bundle all requirements for a java library into a zip file.

This plugin will also copy anything from the `src/zip` folder into the zip archive.

The zip file will be built to `build/artifact/${rootProject.name}-${project.name}-${project.property('project.version')}.zip`

## Usage

Using the `toCopy` in your dependencies will automatically copy the dependencies to a zip archive

__Gradle File__
```groovy
plugins {
    id 'io.github.pacificengine.build.zip' version '0.1.3'
}

dependencies {
    toCopy project(':instance')
}
```

## Properties
### Required Properties
* `project.group` The group the archive belongs to (Example: `io.github.PacificEngine`)
* `project.name` The name of the project (Should be automatically assigned by gradle) (Example: `zipper`)
* `project.version` The build version of the project (Example: `1.0.0`)

### Optional Properties
* `project.archive.zip.group` The group to put the zip in the maven for (Defaults to `project.archive.group` then to `project.group`) (Example: `io.github.PacificEngine`)
* `project.archive.zip.name` The name of the zip file (Defaults to `project.archive.name` then to `${rootProject.name}-${project.name}` unless rootProject.name is identical then it defaults to `project.name`) (Example: `zipper`)
* `project.archive.zip.version` The version of the zip file (Defaults to `project.archive.version` then to `project.version`) (Example: `1.0.0`)
* `project.archive.zip.extension` The extension of the zip file (Defaults to `project.archive.extension` then to `zip`)
* `project.archive.zip.source` The directory of files to be placed in the zip file (Defaults to `src/zip`)
* `project.archive.zip.build` When building the zip file, the location to put all the files (Default to `build/zip`)
* `project.archive.zip.libs` The location to put the jar files inside the zip file (Default to empty) (Example: `/libs`)
* `project.archive.zip.include` The values to include in the zip file [`;` Delimited] (Defaults to null) (Example: `*.jar;*.txt`)
* `project.archive.zip.exclude` The values to exclude from the zip file [`;` Delimited] (Defaults to null) (Example: `*.zip;*.log`)
* `project.archive.zip.destination` The location to put the built zip file (Defaults to `build/artifact`)
