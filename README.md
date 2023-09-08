# th2 conn gRPC library (0.1.0)

This library contains proto messages and `conn` service with RPC methods which can be used in implementation of th2 conn. See [conn.proto](src/main/proto/th2_grpc_conn/conn.proto "conn.proto") file for details. <br>
Tool generates code from `.proto` files and uploads built packages (`.proto` files and generated code) to specified repositories.

## How to maintain project

1. Make your changes.
2. Up version of Java package in `gradle.properties` file.
3. Up version of Python package in `package_info.json` file.
4. Commit everything.

## How to run project

### Java

If you wish to manually create and publish a package for Java, run the following command:

```
gradle --no-daemon clean build publish artifactoryPublish \
       -Purl=${URL} \ 
       -Puser=${USER} \
       -Ppassword=${PASSWORD}
```

`URL`, `USER` and `PASSWORD` are parameters for publishing.

### Python

If you wish to manually create and publish package for Python:

1. Generate services from `.proto` files:
    - Download and build [th2 Python service generator](https://github.com/th2-net/th2-python-service-generator "th2-python-service-generator") project with Gradle:
        ```
        gradle clean build
        ```
    - Run th2 Python service generator:
        ```
        java -jar {path_to_jar} -p src/main/proto/{package_name} -w PythonServiceWriter -o src/gen/main/python/{package_name}
       ```
2. Generate code from `.proto` files and publish everything:
    ```
    pip install -r requirements.txt
    python setup.py generate
    python setup.py sdist
    twine upload --repository-url ${PYPI_REPOSITORY_URL} --username ${PYPI_USER} --password ${PYPI_PASSWORD} dist/*
    ```
   `PYPI_REPOSITORY_URL`, `PYPI_USER` and `PYPI_PASSWORD` are parameters for publishing.

## Release notes

### 0.1.0

+ Updated bom:4.5.0
+ Updated grpc-service-generator:3.4.0
+ Updated mypy-protobuf:3.4