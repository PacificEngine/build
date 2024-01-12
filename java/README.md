![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins

## Purpose
The Purpose of this plugin is to significantly clean up standard java builds so that the build file is just a list of dependencies.

The plugin will handle creating artifacts in a standard way for most java builds.

## Usage

Just include the plugin into any build you'd like to use it in and assign the appropriate properties.

__Gradle File__
```groovy
plugins {
    id 'io.github.pacificengine.build.java' version '0.1.3'
}

dependencies {
    implementation libs.bundles.springboot
    implementation project(":library")

    compileOnly group: 'org.projectlombok', name: 'lombok', version: '1.18.+'
    annotationProcessor group: 'org.projectlombok', name: 'lombok', version: '1.18.+'
    testImplementation group: 'org.junit.jupiter', name: 'junit-jupiter-api', version: '5.9.+'
    testRuntimeOnly group: 'org.junit.jupiter', name: 'junit-jupiter-engine'
}
```

## Properties
### Required Properties
* `project.group` The group the archive belongs to (Example: `io.github.PacificEngine`)
* `project.name` The name of the project (Should be automatically assigned by gradle) (Example: `zipper`)
* `project.version` The build version of the project (Example: `1.0.0`)
* `java.source` The java source for the build (Example: `21`)
* `java.target` The java target for the build (Example: `21`)

### Optional Properties
* `project.archive.java.group` The group to put the java in the maven for (Defaults to `project.archive.group` then to `project.group`) (Example: `io.github.PacificEngine`)
* `project.archive.java.name` The name of the java build (Defaults to `project.archive.name` then to `${rootProject.name}-${project.name}` unless rootProject.name is identical then it defaults to `project.name`) (Example: `zipper`)
* `project.archive.java.version` The version of the java build (Defaults to `project.archive.version` then to `project.version`) (Example: `1.0.0`)
* `project.archive.java.include` The values to include in the zip file [`;` Delimited] (Defaults to null) (Example: `*.class;*.txt`)
* `project.archive.java.exclude` The values to exclude from the zip file [`;` Delimited] (Defaults to null) (Example: `*.xml;*.log`)

### Optional Manifest Specific Properties

#### Module Name
* `project.archive.java.module.include` If you want to include `Automatic-Module-Name` in the manifest file (Defaults to `true`)
* `project.archive.java.module.name` The value of `Automatic-Module-Name` (Defaults to `${javaArchiveGroupName}.${javaArchiveBaseName}`)

#### Bundle Info
* `project.archive.java.bundle.include` If you want to include `Bundle-Vendor`, `Bundle-SymbolicName`, `Bundle-Version`, `Bundle-Description`, and `Bundle-DocURL` in the manifest file (Defaults to `true`) 
* `project.archive.java.bundle.vendor.name` The value of `Bundle-Vendor` (Defaults to `project.vendor.name` otherwise ``)
* `project.archive.java.bundle.name` The value of `Bundle-SymbolicName` (Defaults to `${javaArchiveGroupName}.${javaArchiveBaseName}`)
* `project.archive.java.bundle.version` The value of `Bundle-Version` (Defaults to `javaArchiveVersion`)
* `project.archive.java.bundle.description` The value of `Bundle-Description` (Defaults to `project.description`)
* `project.archive.java.bundle.url` The value of `Bundle-DocURL` (Defaults to `project.url` otherwise `git.repo.url` otherwise ``)

#### Implementation Info
* `project.archive.java.implementation.include` If you want to include `Implementation-Vendor`, `Implementation-Vendor-Id`, `Implementation-Title`, `Implementation-Build-Date`, `Implementation-Version`, and `Implementation-URL` in the manifest file (Defaults to `true`)
* `project.archive.java.implementation.vendor.name` The value of `Implementation-Vendor` (Defaults to `project.vendor.name` otherwise ``)
* `project.archive.java.implementation.vendor.id` The value of `Implementation-Vendor-Id` (Defaults to `javaArchiveGroupName`)
* `project.archive.java.implementation.title` The value of `Implementation-Title` (Defaults to `javaArchiveBaseName`)
* `Implementation-Build-Date` is automatically assigned in the format `yyyy-MM-dd'T'HH:mm:ss.SSSZ`
* `project.archive.java.implementation.version` The value of `Implementation-Version` (Defaults to `javaArchiveVersion`)
* `project.archive.java.implementation.url` The value of `Implementation-URL` (Defaults to `project.url` otherwise `git.repo.url` otherwise ``)

#### Build Info
* `project.archive.java.buildInfo.include` If you want to include `Built-By`, `Build-Timestamp`, `Build-Jdk`, `Build-OS`, `Created-By`, `X-Compile-Target-JDK`, and `X-Compile-Source-JDK`  in the manifest file (Defaults to `true`)
* `Built-By` is automatically assigned to the system variable `user.name`
* `Build-Timestamp` is automatically assigned in the format `yyyy-MM-dd'T'HH:mm:ss.SSSZ`
* `Build-Jdk` is automatically assigned to the system variables `java.version (java.vendor) java.vm.version`
* `Build-OS` is automatically assigned to the system variables `os.name os.arch os.version`
* `Created-By` is automatically assigned to the value `Gradle ${gradle.gradleVersion}`
* `X-Compile-Target-JDK` is automatically assigned to the value `java.target`
* `X-Compile-Source-JDK` is automatically assigned to the value `java.source`