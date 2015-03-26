### Overview ###
MakeItSo converts Visual Studio solutions to gcc makefiles for Linux. It will convert all projects in a solution and create a makefile for each one. It also creates a master makefile that will build them in the correct dependency order.

**Current version (1.2)**

Version 1.2 supports C++ and C# VS 2008 and VS 2010 solutions:
  * **C++** projects are converted to gcc builds. Converts executables, static libraries, and DLLs into equivalent gcc makefiles.
  * **C#** projects are converted to mono builds. Converts executables and libraries (including WinForms executables and WinForms custom controls) into equivalent mono makefiles.

**Do you want to make MakeItSo even better?**

I am no longer actively enhancing MakeItSo. If you want to become a contributor or the 'owner' of this project, please mail me at richard\_s\_shepherd{at}yahoo.co.uk.

**Details and links**

Many self-contained solutions can be converted just by running MakeItSo against the solution file. For more complex solutions, you can provide extra information to MakeItSo, for example to replace Windows-specific external libraries with Linux versions.

  * See [the wiki](MakeItSo.md) for more details about how to convert more complex projects.
  * See [the project roadmap](ProjectRoadmap.md) for planned future developments.
  * See [how to report problems](HowToReportProblems.md) if MakeItSo does not convert a Visual Studio solution correctly.
  * [Thanks and acknowledgements](ThanksAndAcknowledgements.md)

### Quick start ###
  * Download the latest version of MakeItSo from the featured-downloads link.

  * In Windows: run MakeItSo against a solution file (`.sln`). It will generate a master makefile called `Makefile` in the root folder of your solution, and project-specific makefiles in each project folder.

  * In Linux: run `make` from the solution root folder. The build output will be in a folder structure similar to the Visual Studio output, except that folders are prefixed with 'gcc', for example gccDebug instead of Debug. (C# builds prefix the output folders with 'mono'.)

**Running MakeItSo**

If MakeItSo is on the path, you can run it from the solution root folder without any parameters:
```
e:\code\my_solution>MakeItSo
```

If MakeItSo is not on the path, or if you want to convert a solution that is in a different folder from the working directory, you can pass MakeItSo the path and name of the solution to convert:
```
c:\>MakeItSo -file=e:\code\my_solution\my_solution.sln
```

MakeItSo must be run from Windows, as it uses Visual Studio automation to parse the solution and project files.