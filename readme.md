# Image versions info

java 1.8.0_241 (ibmjava 8)

maven 3.6.3

node 10.19.0

npm 6.13.4

# How to use this image

You can run a Maven project by using the Maven Docker image directly,
passing a Maven command to `docker run`:

    docker run -it --rm --name my-mvn-project -v "$(pwd)":/usr/workdir -w /usr/workdir image:tag mvn verify

    docker run -it --rm --name my-mvn-project -w /usr/workdir -v /user/my-mvn-project:/usr/workdir image:tag mvn package

    docker run -it --rm --name my-mvn-project -v "$(pwd)":/usr/workdir -w /usr/workdir  maven-node:mvn-3.6.3-ibmjdk-8-node-10.19 npm install

    docker run image:tag node --version


# Reusing the Maven local repository

The local Maven repository can be reused across containers by creating a volume and mounting it in `/root/.m2`.

    docker volume create --name maven-repo
    docker run -it -v maven-repo:/root/.m2 maven mvn archetype:generate # will download artifacts
    docker run -it -v maven-repo:/root/.m2 maven mvn archetype:generate # will reuse downloaded artifacts

Or you can just use your home .m2 cache directory that you share e.g. with your Eclipse/IDEA:

    docker run -it --rm -v "$PWD":/usr/src/mymaven -v "$HOME/.m2":/root/.m2 -v "$PWD/target:/usr/src/mymaven/target" -w /usr/src/mymaven maven mvn package  


# This image is based on the Maven and Node Official Images:

### [Maven Official Images](https://hub.docker.com/_/maven)
### [Node Offical Images](https://hub.docker.com/_/node)
### [ibmjava Offical Images](https://hub.docker.com/_/ibmjava)

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us
through a [GitHub issue](https://github.com/50characters/docker-maven/issues).

# License

View [license information](https://www.apache.org/licenses/) for the software contained in this image.


