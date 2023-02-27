# r-minimal-2.0 aka R-Nimbus

The fastest and most reliable way to build R-based containers.

## Introduction
When building an R container, it's important to ensure that all the required packages and dependencies are available, as some packages may not be supported by Alpine. Additionally, some R packages may require a specific version of a package and may not require all of their dependencies. In this documentation, we'll cover how to create a container for an R package that relies on packages not supported by Alpine and for packages that need a specific version of a package without their dependencies.

## Creating a container for an R package
This sample Dockerfile has three steps:

- In the first step, we use the rocker/r-ver image to build an R environment and install any system dependencies required by the R packages.
- In the second step, we add a **fictional** R package called **my-r-package** using the install2.r function. We then use the remotes::prune_installed() function to safely remove any unnecessary dependencies of the package, which will help reduce the size of the final image.
- In the third step, we copy the installed R packages from the second step to a smaller Alpine image. We also add the bash package using the apk package manager.

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
