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
version="$(PRINT_VERSION=true gradle --quiet :printVersion)"
git tag "${version}" -m "v${version}"
git push origin "${version}"
curl --request POST --location --fail --header 'Accept: application/vnd.github+json' --header "Authorization: Bearer ${GIT_TOKEN}" "https://api.github.com/repos/PacificEngine/gradle-plugins/releases" --data "{\"tag_name\":\"${version}\",\"name\":\"v${version}\",\"draft\":false,\"prerelease\":false,\"generate_release_notes\":true}"
gradle publish
gradle publishPlugins
```