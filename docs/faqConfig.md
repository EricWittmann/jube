### Configuration Questions

#### How do I configure remote repositories?

Jube loads its [image zips](imageZips.html) from Maven repositories in a similar way to Docker loading its images from Docker Registries. Using maven means that Java developers can easily release [image zips](imageZips.html) along with their other artifacts (jars, wars, bundles, ears etc).

Many folks use internal maven repositories for making internal releases of software. Jube can use those repositories; though it needs configuring to know where to look.

You can configure the list of remote maven repositories to use via the **$JUBE_REMOTE_MAVEN_REPOS** environment variable

    export JUBE_REMOTE_MAVEN_REPOS=http://repo1.maven.org/maven2@id=central,http://repository.jboss.org/nexus/content/groups/public@id=jboss-public

The format is a list of comma separated URLs. You can append the URL with @key-value to further configure the URLs; for example you can add **@id=foo** so that the repository is given a server ID of _foo_ which can then be used to associate login and passwords from the **~/.m2/settings.xml** file.

#### How do I run Jube on multiple hosts?

To run Jube on multiple hosts you just need to point each Jube node at the ZooKeeper ensemble to use to connect all the nodes together.

You can run your own ZooKeeper ensemble then point each Jube node at it via the **$ZOOKEEPER_URL** environment variable:

    export ZOOKEEPER_URL=somehost:2181

If no **ZOOKEEPER_URL** environment variable is specified, Jube will create a default ZooKeeper server and use that. If you then want to connect a second Jube node to the first, just note the host and port that Jube created the ZooKeeper server on (it writes this to its logs), then set the **$ZOOKEEPER_URL** environment variable for each other Jube node you want to connect:

    export ZOOKEEPER_URL=somehost:2181

#### How do I specify a different **processes** folder?

Jube uses a folder called **processes* inside the Jube installation by default.

You can configure where this folder lives on the file system using the **JUBE_PROCESS_DIR** environment variable

    export JUBE_PROCESS_DIR=/var/local/myjube/processes

