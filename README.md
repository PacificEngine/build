# How To Utilize Template

# Compile
```bash
gradle clean build
```

# Pre-Commit
```bash
rm -rf gradle/wrapper gradlew gradlew.bat
gradle wrapper --gradle-version=8.5 --distribution-type=all
git add gradle/wrapper/ gradlew gradlew.bat
git update-index --chmod=+x gradle/wrapper/gradle-wrapper.jar gradlew gradlew.bat
git add gradle/wrapper/ gradlew gradlew.bat
```

# Publish
Requires `GIT_USERNAME` and `GIT_TOKEN` environment variables to be set
```bash
git tag '0.1.1' -m 'v0.1.1'
git push origin '0.1.1'
gradle publishPlugins publish
```