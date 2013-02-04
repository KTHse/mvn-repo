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

## Repo management ##

First of all, clone the mvn-repo if you haven't already, this obviously only needs to be done
once, but you may want to update your copy with a `git pull --rebase` instead

```
git clone git@github.com:KTHse/mvn-repo.git
```

Deploy your artifacts to the repo the normal mvn way, but supplying the path to the 
local mvn-repo git repository to put the data there.

```
cd some-project
mvn -DaltDeploymentRepository=snapshot-repo::default::file:../mvn-repo clean deploy
```

Commit the changes to the mvn-repo and push the changes.

```
cd ../mvn-repo
git status
git add <something>
git commit -m "Some comment"
git push
```
