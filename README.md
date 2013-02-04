mvn-repo
========

A repository for maven artifacts.

Ok, so there is nothing here yet, but eventually this repo can be used with the following pom.xml setup.

```
<distributionManagement>
    <repository>
        <id>repo</id>
        <url>https://github.com/KTHse/mvn-repo/raw/master/releases</url>
    </repository>
    <snapshotRepository>
        <id>snapshot-repo</id>
        <url>https://github.com/KTHse/mvn-repo/raw/master/snapshots</url>
    </snapshotRepository>
</distributionManagement>
```
