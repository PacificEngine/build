![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/build?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/build?label=last%20release&style=flat-square)

# How To Utilize Plugins

## Plugin List
For usage go to the bundle specific readme file.
* [io.github.pacificengine.build.docker](docker/README.md)
* [io.github.pacificengine.build.java](java/README.md)
* [io.github.pacificengine.build.plugin.groovy](plugin/groovy/README.md)
* [io.github.pacificengine.build.plugin.release](plugin/release/README.md)
* [io.github.pacificengine.build.release](release/README.md)
* [io.github.pacificengine.build.repository](repository/README.md)
* [io.github.pacificengine.build.zip](zip/README.md)

## Example Projects
* [Docker Deployment Spring Template](https://github.com/PacificEngine/DockerDeployment)

# How To Modify And Deploy
* [Source link](https://github.com/PacificEngine/build)

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
Requires `GIT_USERNAME` and `GIT_TOKEN` environment variables to be set with a token generated at https://github.com/settings/tokens/new with `write:packages` permissions.

__Mac/Linux__
```bash
./gradlew publish
./gradlew publishPlugins
```

__Windows__
```PowerShell
./gradlew.bat publish
./gradlew.bat publishPlugins
```