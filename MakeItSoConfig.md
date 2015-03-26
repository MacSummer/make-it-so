### Overview ###
To convert some solutions into makefiles, MakeItSo needs extra information given to it that it cannot get from the Visual Studio project and solution files. You can provide this information in a `MakeItSo.config` file.

The `MakeItSo.config` file lets you tell the build to:

  * [Remove specified Windows libraries and use Linux versions instead.](MakeItSoConfig#Add_and_remove_libraries.md)
  * [Use different library paths for the Linux build.](MakeItSoConfig#Add_and_remove_library_paths.md)
  * [Use different include paths for the Linux build.](MakeItSoConfig#Add_and_remove_include_paths.md)
  * [Remove pre-processor definitions, and replace them with others.](MakeItSoConfig#Add_and_remove_preprocessor_definitions.md)
  * [Remove compiler flags and replace them with others.](MakeItSoConfig#Add_and_remove_compiler_flags.md)
  * [Specify an alternative compiler.](MakeItSoConfig#Specify_an_alternative_compiler.md)
  * [Convert a static library to a shared-objects library.](MakeItSoConfig#Convert_a_static_library_to_a_shared-objects_library.md)
  * [Ignoring a project](MakeItSoConfig#Ignoring_a_project.md)


**'Self-contained solutions'**

MakeItSo can convert many Visual Studio solutions without needing any extra information. If a solution is 'self-contained' then it should be able to be converted without any extra information being needed. A self-contained solution is one which contains all its dependencies (for example libraries) as projects within the solution.

Some solutions are not self-contained. They link in 'external' libraries that are not built as part of the solution itself. If these are provided as pre-built Windows libraries, you will not be able to build them into a Linux version of the build. You will need to tell the Linux version to use pre-build Linux versions of these external libraries instead.


**Add and remove vs. replace**

In most cases, the MakeItSo.config file specifies settings to add or remove rather than specifying replacements. This lets you replace a single Windows library with more than one Linux library if there is not a one-to-one match, for example. Or you could add a preprocessor definition to the Linux build without removing an existing one.


### MakeItSo.config file format ###
```
<MakeItSo>
  
  <!-- Settings that apply to all projects in the solution -->
  <AllProjects>

  </AllProjects>

  <!-- Settings for specific named projects -->
  <Project name="App">

  </Project>
  
</MakeItSo>
```

Any settings in the `<AllProjects>` section apply to all projects in the solution, unless there is a specific `<Project name="[name]">` section for the project. If there are specific settings for a project, it must contain all settings for that project. Specific projects do not inherit properties from the `<AllProjects>` section.


### Add and remove libraries ###
If a project links in Windows-specific external libraries you will need
to replace these with Linux equivalents. For example:
```
    <RemoveLibrary library="TextLibrary.lib"/>
    <AddLibrary configuration="Debug" library="libTextLibD.a"/>
    <AddLibrary configuration="Release" library="libTextLibR.a"/>
```

### Add and remove library paths ###
If you are replacing libraries, you may need to replace library paths as well. For example:
```
    <RemoveLibraryPath path="Externals/TextLibrary/Libs/Windows x86/Debug"/>
    <RemoveLibraryPath path="Externals/TextLibrary/Libs/Windows x86/Release"/>
    <AddLibraryPath configuration="Debug" path="Externals/TextLibrary/libs/gcc/Debug"/>
    <AddLibraryPath configuration="Release" path="Externals/TextLibrary/libs/gcc/Release"/>
```
Paths are specified relative to the solution root folder.


### Add and remove include paths ###
You may want to use different include paths with a Linux build. For example:
```
    <RemoveIncludePath path="Include/WindowsTemplates"/>
    <AddIncludePath configuration="Debug" path="Include/gccTemplates"/>
    <AddIncludePath configuration="Release" path="Include/gccTemplates"/>
```
Paths are specified relative to the solution root folder.


### Add and remove preprocessor definitions ###
You can add and remove preprocessor definitions. For example:
```
    <RemovePreprocessorDefinition definition="TO_REPLACE" />
    <AddPreprocessorDefinition configuration="Debug" definition="REPLACEMENT_DEBUG" />
    <AddPreprocessorDefinition configuration="Release" definition="REPLACEMENT_RELEASE" />
```
MakeItSo automatically removes `WIN32` and adds `GCC_BUILD`.


### Add and remove compiler flags ###
You can add and remove compiler flags. For example:
```
    <RemoveCompilerFlag flag="-O2"/>
    <AddCompilerFlag configuration="Release" flag="-O3"/>
```


### Specify an alternative compiler ###
By default MakeItSo will use the default installation of these compilers:
  * gcc for C files
  * g++ for C++ files
  * gmcs for C# files

You can specify alternative compilers for any one of these languages. For example:
```
       <CSharpCompiler compiler="dmcs"/>
       <CCompiler compiler="gcc2.1"/>
       <CPPCompiler compiler="g++4.3"/>
```


### Convert a static library to a shared-objects library ###
By default MakeItSo converts Windows static libraries to Linux static libraries, and Windows DLLs to Linux shared-objects libraries. You can specify that Windows static libraries are converted into Linux shared-objects libraries instead:
```
    <ConvertStaticLibraryToSharedObjects convert="true"/>
```


### Ignoring a project ###
You make have a project in the solution that cannot be converted and which should be excluded from the Linux makefiles. You can specify that projects can be ignored in the main part of the config file, ie outside the `<AllProjects>` or project-specific sections. For example:
```
<MakeItSo>
  <IgnoreProject project="App1"/>
</MakeItSo>
```