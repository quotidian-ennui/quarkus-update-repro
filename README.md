# quarkus-update-repro

This is a reproducer for https://github.com/quarkusio/quarkus/issues/37715

Ultimately, if gradle.properties is "gitignored" even if you have explicitly added the file then `gradle quarkusUpdate` results in a gradle.properties file that only contains proposed changes.

```
# There is no .gitignore file 
$ echo gradle.properties >> .gitignore
$ ./gradlew --console plain --stacktrace --init-script openrewrite.gradle rewriteDryRun
### the patch is broken
$ cat ./build/reports/rewrite/rewrite.patch
$ rm .gitignore
$ ./gradlew --console plain --stacktrace --init-script openrewrite.gradle rewriteDryRun
### the patch is correct
$ cat ./build/reports/rewrite/rewrite.patch
```
