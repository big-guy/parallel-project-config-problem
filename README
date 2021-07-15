# Parallel project problem investigation

`./gradlew --scan resolving:resolveIt`

Normal looking evaluation of resolving project:
https://scans.gradle.com/s/g4nes3nn3xz74/performance/configuration/by-project?details=project-:resolving!resolving/build.gradle&expandedDependencies=WyJjb2RlLXVuaXQtcmVzb2x2aW5nL2J1aWxkLmdyYWRsZSE6cmVzb2x2aW5nIl0&openProjects=WyJwcm9qZWN0LTpyZXNvbHZpbmciXQ

`./gradlew --scan resolving:resolveIt -Pbreak`

Strange looking evaluation of resolving project:
https://scans.gradle.com/s/6ddsmwxia6qse/performance/configuration/by-project?details=project-:resolving!resolving/build.gradle&expandedDependencies=WyJjb2RlLXVuaXQtcmVzb2x2aW5nL2J1aWxkLmdyYWRsZSE6cmVzb2x2aW5nIl0&openProjects=WyJwcm9qZWN0LTpyZXNvbHZpbmciXQ

I see the same behavior with Gradle 6.8.3 and master (7.2).

Resolving a configuration at configuration time that has project dependencies causes the un-evaluated projects to be evaluated.  See the `configurations.resolve.resolvedConfiguration` line in `resolving/build.gradle`. The "real" build is doing something similar.

Here's a PR that reproduces the problem in an integration test:
https://github.com/gradle/gradle/pull/17732

It checks that no `sub0-4` project has an overlapping configurate project build operation with project `resolving`.
