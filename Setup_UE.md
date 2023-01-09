# Setup Procedures and Trouble Shooting
## General Procedure
https://docs.unrealengine.com/5.1/en-US/downloading-unreal-engine-source-code/ \
Remember to pay attention to the steps stated in README.md\
Please install Visual Studio with the components required before running 
**GenerateProjectFiles.bat**.\
Make sure you have the internet connection when something goes wrong.\
https://docs.unrealengine.com/5.1/en-US/building-unreal-engine-from-source/

## Debug Step by Step into the C++ source code
After that, try to add a breakpoint to start debugging.

## Detailed steps quoted from the Unreal Engine 5.1.0 / README.md
### Windows
1.  Install **[GitHub Desktop for Windows](https://desktop.github.com/)** then **[fork and clone our repository](https://guides.github.com/activities/forking/)**. 

    When GitHub Desktop is finished creating the fork, it asks, **How are you planning to use this fork?**. Select **For my own purposes**. This will help ensure that any changes you make stay local to your repository and avoid creating unintended pull requests. You'll still be able to make pull requests if you want to submit modifications that you make in your fork back to our repository.

    Other options:

    -   To use Git from the command line, see the [Setting up Git](https://help.github.com/articles/set-up-git/) and [Fork a Repo](https://help.github.com/articles/fork-a-repo/) articles.

    -   If you'd prefer not to use Git, you can get the source with the **Download ZIP** button on the right. Note that the zip utility built in to Windows marks the contents of .zip files downloaded from the Internet as unsafe to execute, so right-click the .zip file and select **Properties…** and **Unblock** before decompressing it.

2.    Install **Visual Studio 2019**.

    All desktop editions of Visual Studio 2019 can build UE5, including [Visual Studio Community 2019](http://www.visualstudio.com/products/visual-studio-community-vs), which is free for small teams and individual developers.

    To install the correct components for UE5 development, make sure the **Game Development with C++** workload is checked. Under the **Installation Details** section on the right, also choose the following components:

    -   **C++ profiling tools**
    -   **C++ AddressSanitizer** (optional)
    -   **Windows 10 SDK** (10.0.18362 or newer)
    -   **Unreal Engine Installer**

3.  Open your source folder in Windows Explorer and run **Setup.bat**. This will download binary content for the engine, install prerequisites, and set up Unreal file associations.

    On Windows 8, a warning from SmartScreen may appear. Click **More info**, then **Run anyway** to continue.

    A clean download of the engine binaries is currently 20-21 GiB, which may take some time to complete. Subsequent runs will be much faster, as they only download new and updated content.

4.  Run **GenerateProjectFiles.bat** to create project files for the engine. It should take less than a minute to complete.  

5.  Load the project into Visual Studio by double-clicking the new **UE5.sln** file.

6.  Set your solution configuration to **Development Editor** and your solution platform to **Win64**, then right click the **UE5** target and select **Build**. It may take anywhere between 10 and 40 minutes to finish compiling, depending on your system specs.

7.  After compiling finishes, you can run the editor from Visual Studio by setting your startup project to **UE5** and pressing **F5** to start debugging.

### Linux / WSL

1.  Install a **[visual Git client](https://git-scm.com/download/gui/linux)**, then **[fork and clone our repository](https://guides.github.com/activities/forking/)**.

    Other options:
    
    -   To use Git from the command line instead, see the [Setting up Git](https://help.github.com/articles/set-up-git/) and [Fork a Repo](https://help.github.com/articles/fork-a-repo/) articles.

    -   If you'd prefer not to use Git, use the **Download ZIP** button on the right to get the source as a zip file.

2.  Open your source folder and run **Setup.sh** to download binary content for the engine.

3.  Both cross-compiling and native builds are supported.

    -   **Cross-compiling** is handy for Windows developers who want to package a game for Linux with minimal hassle. It requires a cross-compiler toolchain to be installed. See the [Linux cross-compiling page in the documentation](https://docs.unrealengine.com/linux-development-requirements-for-unreal-engine/).

    -   **Native compilation** is discussed in [a separate README](Engine/Build/BatchFiles/Linux/README.md) and [community wiki page](https://unrealcommunity.wiki/building-on-linux-qr8t0si2).

## Trouble Shooting
### ERROR when installing
```
Checking dependencies...                                                                                                                        Updating dependencies:   0% (0/97590)...                                                                                  
Unhandled exception. System.PlatformNotSupportedException: Thread abort is not supported on this 
platform.     at System.Threading.Thread.Abort() . . . 
```
**Solution**:
Make sure you have the internet connection when something goes wrong.

### ERROR when running GenerateProjectFiles.bat 
```
Some Platforms were skipped due to invalid SDK setup: Mac, IOS, Android, Linux, LinuxArm64, TVOS, PS4.
See the log file for detailed information
```
**Solution**:
Make sure you have required VS installed.

### ERROR Message from Unreal Engine 5.1 
The installed version of the Intel graphics driver has known issues.

**Solution**:
Update through  **intel website**, Device Manager / Display adapters, PC Manager.
If you can't update the driver due to the PC manufacturer, please install Unreal Engine4.27 instead.

### ERROR MSB3073 from Unreal Engine 
The command ... exicted with code 6.

**Solution**:There are multiple reasons to this problem, including adding some wrong letters.
Try to redo the whole process will solve it.

### Error C4668: “__cplusplus” not defined from Unreal Engine: Undefined Identifier Warning
**Solution**:
Engine/Source/Program/UnrealBuildTool/Configuration/ModuleRule.cs
set bEnableUndefinedIdentifierWarning=false

### Others ERROR
Try to search online for solutions.
