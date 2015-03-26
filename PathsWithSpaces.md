MakeItSo will do its best to convert Visual Studio projects that have paths that contain spaces. Overall it seems that Visual Studio solutions are slightly more tolerant of paths with spaces than makefiles are.

In the generated makefile:
  * Include paths and library paths are quoted.
  * Spaces are removed from project names, so 'The Project' becomes TheProject.
  * Spaces are removed from configuration names, so 'Debug Static' becomes DebugStatic.
  * Spaces are removed from output and intermediate folder names, as tools like ar do not seem to cope well with spaces, even if paths are quoted.