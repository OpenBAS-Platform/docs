!!! tip "Prerequisites"

    Ensure you have followed the steps for installing prerequisites according to your development
    platform of choice:

    * [Linux (Ubuntu used as example)](/development/environment_ubuntu)
    * [Windows](/development/environment_windows)
    * MacOS (TBD)

# Building and running from source

## Clone the OpenBAS repository
Obtain a clone of the main OpenBAS repository and navigate to it:
```shell
git clone https://github.com/OpenBAS-Platform/openbas
cd openbas
```

!!! Info "Assumed shell location"

    This documentation assumes that commands listed here are run from the root
    folder of the git repository, unless stated otherwise.

## Backend

!!! tip "IntelliJ IDEA run confgurations"

    The OpenBAS repository provides predefined IntelliJ IDEA run configurations for
    both the backend and the frontend. After loading the OpenBAS cloned repository's root
    directory in IDEA, the run configurations will show up in the Run widget in the top right corner.

### Configuring
Development assumes that you are using a development-specific properties file. The file located at
`./openbas-api/src/main/resources/application.properties` is a versioned-controlled example file and
lacks many of the required configuration settings needed for OpenBAS to execute.

It is strongly recommended to make a copy of the sample `application.properties` file to create
a development-specific profile called `dev`.

Copy and paste the example `application.properties` file into the same directory:
```shell
cp ./openbas-api/src/main/resources/application.properties ./openbas-api/src/main/resources/application-dev.properties
```

#### Required dependencies
Edit the `application-dev.properties` file, according to the .env file created earlier,
and any additional configuration. Make sure the file contains settings for at the very minimum
the following dependencies:

- PostgreSQL
- MinIO
- RabbitMQ
- Elasticsearch

All required settings are listed in the [Configuration documentation](/deployment/configuration#dependencies)


### Building and running
Maven is used for package management and building the main server binary.
OpenBAS is a Spring Boot application and thus can be built and started
in one fell swoop with
```shell
mvn spring-boot:run -Dspring-boot.run.profiles=dev -Dspring-boot.run.main-class=io.openbas.App
```

## Frontend
!!! Info "Change the location of your shell"

    In this section, commands need to be run from a subfolder: ./openbas-front

Navigate to `./openbas-front`.
```shell
cd ./openbas-front
```

### Building
Execute `yarn install` to fetch all dependencies from npmjs.com:
```shell
yarn install
```

### Running
Execute `yarn start` to start a frontend locally:
```shell
yarn start
```
The banner should come up soon after:
```
  VITE v6.3.4  ready in 168 ms

  ➜  Local:   http://localhost:3001/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```
It is possible to navigate to http://localhost:3001/ by default. Note that the backend needs
to be running otherwise the GUI will not come up in the browser.