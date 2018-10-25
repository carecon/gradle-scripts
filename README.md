# gradle-scripts

Gradle scripts used inside of carecon.

## jcenter.gradle
Used for publishing to nexus@carecon and jcenter.

### Usage
At the end of your build.gradle add

```
apply from: 'https://raw.githubusercontent.com/carecon/gradle-scripts/master/jcenter.gradle'
```

### Required Environment variables:

For publishing to maven

- `NEXUS_RELEASES_URL`: The nexus releases repository url like: `http://repo.your-company.com/nexus/content/repositories/releases/`
- `NEXUS_SNAPSHOTS_URL`: The nexus snapshots repository url like: `http://repo.your-company.com/nexus/content/repositories/snapshots/`
- `NEXUS_USERNAME`
- `NEXUS_PASSWORD`

For publishing to jcenter

- `BINTRAY_USER`: the username
- `BINTRAY_KEY`: from profile page -> edit
- `BINTRAY_ORG`: (optional): If publishing to a org
- `BINTRAY_GPG_PASSWORD`: (optional) The passphrase for GPG signing'

### Tasks

Command to publish to maven:

```
./gradlew publish
```

Command to publish to jcenter (only release versions)
```
./gradlew bintrayUpload
```

#### Possible shell script for releasing is:
```
VERSION=$(./gradlew -q printVersion | tail -1)
if [[ $VERSION =~ .*-SNAPSHOT$ ]]; then
  ./gradlew publish
else
  ./gradlew publish bintrayUpload
fi
```