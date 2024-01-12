![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins

For usage go to the local readme file.
* [io.github.pacificengine.build.docker](docker/README.md)
* [io.github.pacificengine.build.java](java/README.md)
* [io.github.pacificengine.build.release](release/README.md)
* [io.github.pacificengine.build.repository](repository/README.md)
* [io.github.pacificengine.build.zip](zip/README.md)

### Purpose
The Purpose of this plugin is to bundle all requirements for a java library into a zip file.

This plugin will also copy anything from the `src/zip` folder into the zip archive.

The zip file will be built to `build/artifact/${rootProject.name}-${project.name}-${project.property('project.version')}.zip`

### Properties
#### Required Properties
* `project.group` The group the archive belongs to (Example: `io.github.PacificEngine`)
* `project.name` The name of the project (Should be automatically assigned by gradle) (Example: `zipper`)
* `project.version` The build version of the project (Example: `1.0.0`)

#### Optional Properties
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

### Usage

Using the `toCopy` in your dependencies will automatically copy the dependencies to a zip archive

__Gradle File__
```groovy
plugins {
    id 'io.github.pacificengine.build.zip' version "0.1.3"
}

dependencies {
    toCopy project(':instance')
}
```

# How To Modify And Deploy

## Compile
__Mac/Linux__
```bash
./gradlew clean build
```

__Windows__
```cmd
./gradlew.bat clean build
```

## Update Gradle
```bash
rm -rf gradle/wrapper gradlew gradlew.bat
gradle wrapper --gradle-version=8.5 --distribution-type=all
git add gradle/wrapper/ gradlew gradlew.bat
git update-index --chmod=+x gradle/wrapper/gradle-wrapper.jar gradlew gradlew.bat
git add gradle/wrapper/ gradlew gradlew.bat
```

## Publish
Requires `GIT_USERNAME` and `GIT_TOKEN` environment variables to be set

__Mac/Linux__
```bash
version="$(PRINT_VERSION=true ./gradlew --quiet :printVersion)"
git tag "${version}" -m "v${version}"
git push origin "${version}"
url="https://api.github.com/repos/PacificEngine/gradle-plugins/releases"
body="{\"tag_name\":\"${version}\",\"name\":\"v${version}\",\"draft\":false,\"prerelease\":false,\"generate_release_notes\":true}"
curl --request POST --location --fail --header 'Accept: application/vnd.github+json' --header "Authorization: Bearer ${GIT_TOKEN}" $url --data $body
./gradlew publish
./gradlew publishPlugins
```

__Windows__
```PowerShell
set PRINT_VERSION=true
$version="$(./gradlew.bat --quiet :printVersion)"
set PRINT_VERSION=
git tag "${version}" -m "v${version}"
git push origin "${version}"
$url = "https://api.github.com/repos/PacificEngine/gradle-plugins/releases"
$Headers = @{
	'Accept' = 'application/vnd.github+json'
	'Authorization' = "Bearer ${GIT_TOKEN}"
}
$Body = "{`"tag_name`":`"${version}`",`"name`":`"v${version}`",`"draft`":false,`"prerelease`":false,`"generate_release_notes`":true}"
Invoke-WebRequest -Uri $url -Method POST -MaximumRedirection 5 -Headers $Headers -Body $Body
./gradlew.bat publish
./gradlew.bat publishPlugins
```