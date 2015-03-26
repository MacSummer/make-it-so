### Master makefile and project-specific makefiles ###
MakeItSo generates a master makefile called `Makefile` in the root folder of the solution. It also generates one makefile for each project in the solution. These are created in the root folder of each project, and are called `[project-name].makefile`.

**The master makefile**

The master makefile contains these targets:
  * A default target that builds all projects in the solution. You can build this by running `make` with no parameters.
  * A target for each project in the solution. You can build this by running `make [project-name]`.
  * A 'clean' target which cleans all the intermediate and output files for all projects in the solution. You invoke this with `make clean`

**Project-specific makefiles**

Project makefiles contain these targets:
  * A default target that builds all configurations (Debug, Release etc) for the project. You can build this by running `make -f [project-name].makefile`
  * A target for each configuration. You can build this by running `make -f [project-name].makefile [configuration-name]`
  * A 'clean' target which cleans all intermediate and output file for the project. You invoke this with `make -f [project-name].makefile clean`