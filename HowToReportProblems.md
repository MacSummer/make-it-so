### Before reporting a problem ###
Before reporting a problem please note that:

  * MakeItSo is just a solution to makefile converter. It does not convert your code itself. If your code has Windows specific features, you will need to make it more portable, for example by using cross-platform compatible libraries such as boost. MakeItSo does not help with this.

  * Please check if the reason your project does not compile is already in the roadmap or in the Issues list. For example with version 1.0 these feature are not supported, but are in the future development plan: C# projects, custom build steps, VS2010 solutions.

  * Please check whether you can use a [MakeItSo.config file](MakeItSoConfig.md) to tell MakeItSo how to correctly convert your solution.

### Reporting a problem ###
If you have a solution that cannot be correctly converted to a makefile, please:

  * Create a simplified version of the solution. Please do not send a large, complex solution. It will be much more useful if you can create a small solution that is as simple as possible, but which illustrates the problem. For example, see the sample solutions in the `Tests/TestProjects` folder of the MakeItSo source code.

  * Create an Issue and attach the simplified solution to it. I will add it to the development plan.

### Or, fix it yourself... ###
MakeItSo is open-source of course, so feel free to download the code and fix any problems yourself. If you do this, please mail the fix or raise an issue and attach your code, so that I can merge the change back into the main MakeItSo source. Please let me know if you would like to become a contributor to the project.