**`MakeItSo (with no parameters)`**

If you run `MakeItSo` with no command-line parameters, it will look for a `.sln` file in the working directory and convert it and the projects it contains.

**`-file=[path-to-sln-file]`**

Example: `MakeItSo -file=e:\code\test\test.sln`

MakeItSo will convert the solution file specified. The converted makefile will go into the solution's root folder, and not into the working directory that the command was issued from.

If the `-file` parameter is not provided, MakeItSo will look for a `.sln` file in the working folder.


**`-cygwin=[true/false]`**

Example: `MakeItSo -cygwin=true`

If this is set to `true`, MakeItSo will create a makefile that builds a cygwin project. In particular, shared-objects projects are build as `.dll` files instead of `.so` files.

If the `-cygwin` parameter is not provided, MakeItSo defaults to a Linux (ie, non-cygwin) build .