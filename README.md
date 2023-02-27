# r-minimal-2.0

## Introduction
When building an R container, it's important to ensure that all the required packages and dependencies are available, as some packages may not be supported by Alpine. Additionally, some R packages may require a specific version of a package and may not require all of their dependencies. In this documentation, we'll cover how to create a container for an R package that relies on packages not supported by Alpine and for packages that need a specific version of a package without their dependencies.

## Creating a container for an R package
This sample Dockerfile has two steps:

- In the first step, we use the rocker/r-ver image to build an R environment and install any system dependencies required by the R packages. We then use the install2.r function to install specific versions of the R packages required by the R package we want to build.

- In the second step, we add the bash package using the apk package manager. We then copy the installed R packages from the first step to a smaller Alpine image.

## Building

To build the container, save this Dockerfile to a directory on your machine and navigate to that directory in your terminal. Then, run the following command:

```
docker build -t my-r-package-image . 
```

This will build the container with the name my-r-package-image

You can replace the R packages in the example with the ones required by your R package. Also, you can modify the apt-get command in the first step to install any additional system dependencies required by your R package.


## R Command Line Interface

Now, when you run the container using:

```
docker run -it my-r-package-image
```
You can access the R command line interface as well as the bash shell. You can use the exit command to exit the bash shell and return to the R command line interface.
