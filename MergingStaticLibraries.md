### Overview ###
Sometimes you want to merge a number of static libraries into one. VS2008 and VS2010 handle this differently to each other. This page describes the differences, and how to make sure that MakeItSo can generate the correct makefile in this case.

### Examples ###
In the examples below we are imagining that we have two static libraries: mammals.lib and dinosaurs.lib, and that we want to combine them into one library: animals.lib.

### Visual Studio 2008 ###
  * Create an animals.lib static library project
  * Set up the project dependencies so that animals.lib depends on mammals.lib and dinosaurs.lib.
  * In animals.lib's project linker settings, set Link Library Dependencies to true.
  * You need to have some code in animals.lib, otherwise it won't build. If you have no code to add, you can add an empty dummy.cpp/.h class.

When you build animals.lib, the resulting library will include the code from the two other libraries.

### Visual Studio 2010 ###
VS2010 has the option to Link Library Dependencies like VS2008, but it doesn't seem to work. In many cases VS2010 uses References instead of dependencies, but this doesn't work in this case. Instead you should:
  * Create an animals.lib static library project
  * Set up the project dependencies so that animals.lib depends on mammals.lib and dinosaurs.lib.
  * In animals.lib's project linker settings, set Link Library Dependencies to true.
  * Add a post-build step to link the libraries together. This will look something like this: `lib /out:animals.lib mammals.lib dinosaurs.lib`
  * (You do not need any dummy code in VS2010.)

This is really doing two different things:
  * The post-build step works in the Visual Studio build.
  * The Link Library Dependencies does not do anything in the Visual Studio build, but it does tell MakeItSo to link the libraries together.