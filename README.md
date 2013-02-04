mvn-repo
========

A simple GitHub based repository for maven artifacts.

## Using the repository in projects ##

```xml
  <repositories>
    <repository>
      <id>kth-github</id>
      <url>https://github.com/KTHse/mvn-repo/raw/master/releases/</url>
    </repository>
  </repositories>
```

For snapshot versions replace `releases` with `snapshots` in the URL.

## Deploying to the repo ##

Deploying to the repository is not exactly simple, but relatively straight
forward once you realize how it works. Maven can deploy natively to proper
maven repositories. For this simple github repo, we need to deploy via
a local git version of the repo and then push the changes to github.

First of all, clone the mvn-repo if you haven't already, this obviously only
needs to be done once, but you may want to update your copy with a 
`git pull --rebase` instead

```
git clone git@github.com:KTHse/mvn-repo.git
```

Configure your maven project to deploy to use the mvn-repo in the 
distributionManagement section of pom.xml.

```xml
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

Deploy your artifacts to the repo the normal mvn way, but supplying the path 
to the local mvn-repo git repository to put the data there.

```
cd some-project
mvn -DaltDeploymentRepository=snapshot-repo::default::file:../mvn-repo/snapshots/ clean deploy
```

To deploy to the releases repo, specify the repo and the path to releases

```
mvn -DaltDeploymentRepository=repo::default::file:../mvn-repo/releases/ clean deploy
```

Optionally you may want to include a source jar for that truly open source 
feeling and to make it easier to use your code in, e.g., Eclipse.

```
mvn -DaltDeploymentRepository=snapshot-repo::default::file:../mvn-repo/snapshots/ clean source:jar deploy
```

Commit the changes to the mvn-repo and push the changes.

```
cd ../mvn-repo
git status
git add <something>
git commit -m "Some comment"
git push
```

Now your artifacts can be used by projects as mentioned above.
