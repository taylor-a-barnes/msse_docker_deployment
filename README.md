# Docker Deployment of MOPAC

Use Docker to create a deployment container for the semi-empirical code MOPAC.
The GitHub repository for MOPAC is available here. Note that although there are already Docker containers available for MOPAC, yours must conform to the following constraints: (1) it must use the `ubuntu:22.04` image as a base; (2) it must build MOPAC from source, using CMake (the MOPAC documentation describes how to build using CMake); (3) it must be possible for the end-user to run MOPAC with the following command:

```
docker run --rm -v <volume_options> <image_name> <input_file_name>
```

Follow best practices for container development, and in particular work to make the container as small as possible.

To find the Ubuntu package names for software dependencies that you want to install with apt-get, you can use the [Ubuntu Packages Search](https://packages.ubuntu.com/). For packages with short name abbreviations (such as BLAS), you may want to select the “Search on: Descriptions” option and search for the full name of the library.
You can also usually find the information you need through a more general web search.
Pay careful attention to the CMake output; if something goes wrong, it will usually give you a hint regarding what you need to do.
As an example input file, you can use the following (save it into a file with a “`.mop`” extension).
The normal way to run a MOPAC input file is “`mopac <file_name>.mop`”.

```
AM1
Formic acid
Example of normal geometry definition
O
C 1.20 1
O 1.32 1 116.8 1 0.0 0 2 1
H 0.98 1 123.9 1 0.0 0 3 2 1
H 1.11 1 127.3 1 180.0 0 2 1 3
0 0.00 0 0.0 0 0.0 0 0 0 0
```

Put all of your files (including your Dockerfile, entrypoint script, test input file, etc.) in a GitHub repository.
Create a GitHub Action that runs a MOPAC calculation through your image and prints the output from the **host**.
