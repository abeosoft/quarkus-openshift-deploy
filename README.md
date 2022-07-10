# getting-started Project

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/getting-started-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Related Guides

- RESTEasy Reactive ([guide](https://quarkus.io/guides/resteasy-reactive)): A JAX-RS implementation utilizing build time processing and Vert.x. This extension is not compatible with the quarkus-resteasy extension, or any of the extensions that depend on it.

## Provided Code

### RESTEasy Reactive

Easily start your Reactive RESTful Web Services

[Related guide section...](https://quarkus.io/guides/getting-started-reactive#reactive-jax-rs-resources)

## Build and Deploy to Openshift using Quarkus Maven Tooling

Run this command to build the docker image and deploy it to Openshift. You need to be logged in to Openshift to be able to deploy.

```shell script
  mvn clean package \
  -Pocdeploy \
  -Dquarkus.profile=dev \
  -Dquarkus.container-image.group=app-group \
  -Dquarkus.application.name=quarkus-openshift-deploy \
  -Dquarkus.container-image.name=quarkus-openshift-deploy \
  -Dquarkus.openshift.labels.application=quarkus-openshift-deploy \
  -Dquarkus.container-image.tag=1.0.0 \
  -Dquarkus.container-image.build=true \
  -Dquarkus.container-image.builder=docker \
  -Dquarkus.container-image.push=true \
  -Dquarkus.container-image.registry=registry.corp.io \
  -Dquarkus.kubernetes.deploy=true \
  -Dquarkus.kubernetes.deployment-target=openshift \
  -Dquarkus.container-image.username=$(oc whoami) \
  -Dquarkus.container-image.password=$(oc whoami -t) \
  -Dquarkus.kubernetes-client.trust-certs=true \
  -Dquarkus.openshift.deployment-kind=DeploymentConfig
```

### Additional Useful Command Options
* -DskipTests
* -Dmaven.settings
* -Dquarkus.openshift.env.configmaps
* -Dquarkus.openshift.secret-volumes.<volume-name>.secret-name
* -Dquarkus.openshift.mounts.<volume-name>.path
* -Dquarkus.openshift.env.mapping.<environment-variable-name>.from-secret
* -Dquarkus.openshift.env.mapping.<environment-variable-name>.with-key
* and many more