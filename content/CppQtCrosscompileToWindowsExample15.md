



 

 

 

 

 

([C++](Cpp.md)) [How to cross-compile a Qt Creator project from Ubuntu to a windows executable: example 15: MXE](CppQtCrosscompileToWindowsExample15.md)
==========================================================================================================================================================

 

This is a successful approach to solve the [Qt FAQ](CppQtFaq.md) [How
to cross-compile a Qt Creator project from Ubuntu to a windows
executable?](CppQtCrosscompileToWindows.md), following \[1\].

 

See [MXE](CppMxe.md) for more information about [MXE](CppMxe.md).

 

 

 

 

 

Downloads
---------

 

-   [Download the Qt Creator project
    'CppQtCrosscompileToWindowsExample15' (zip)](CppQtCrosscompileToWindowsExample15.zip)
-   [Download the Windows executable created by the Qt Creator project
    'CppQtCrosscompileToWindowsExample15' (zip)](CppQtCrosscompileToWindowsExample15Exe.zip)

 

 

 

 

 

Technical facts
---------------

 

[Application type(s)](CppApplication.md)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.md)

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Ubuntu](PicUbuntu.png) [Ubuntu](CppUbuntu.md) 10.10 (maverick)
-   ![Windows](PicWindows.png) [Windows](CppWindows.md) XP

[IDE(s)](CppIde.md):

-   ![Command line](PicCl.png) command line
-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 2.0.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.4.5

[Libraries](CppLibrary.md) used:

-   ![Boost](PicBoost.png) [Boost](CppBoost.md): version 1.42
-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.4.5

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): CppQtCrosscompileToWindowsExample15.pro
--------------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2010-09-25T09:43:28 # #------------------------------------------------- QT       += core QT       -= gui LIBS += -lboost_filesystem-mt -lboost_system-mt TARGET = CppQtCrosscompileToWindowsExample15 CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

main.cpp
--------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <string> #include <vector> //--------------------------------------------------------------------------- #include <boost/filesystem.hpp> //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppGetFilesInFolder.htm const std::vector<std::string> GetFilesInFolder(const std::string& folder) {   std::vector<std::string> v;    const boost::filesystem::path my_folder     = boost::filesystem::system_complete(         boost::filesystem::path(folder));    if (!boost::filesystem::is_directory(my_folder)) return v;    const boost::filesystem::directory_iterator j;   for ( boost::filesystem::directory_iterator i(my_folder);         i != j;         ++i)   {     if ( boost::filesystem::is_regular_file( i->status() ) )     {       const std::string filename = i->path().filename();       v.push_back(filename);     }   }   return v; } //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppGetPath.htm const std::string GetPath(const std::string& filename) {   return boost::filesystem::path(filename).parent_path().string(); } //--------------------------------------------------------------------------- int main(int, char* argv[]) {   const std::vector<std::string> v = GetFilesInFolder(GetPath(argv[0]));   std::copy(v.begin(),v.end(),std::ostream_iterator<std::string>(std::cout,"\n"));   std::cout << "Number of files: " << v.size() << '\n'; } //---------------------------------------------------------------------------`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Process
-------

 

For installation, follow the approach by described by \[1\].

 

In the folder with your project

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ``  richel@richel1-desktop:~/2Projects/Website/CppQtCrosscompileToWindowsExample15$ i686-pc-mingw32-qmake  richel@richel1-desktop:~/2Projects/Website/CppQtCrosscompileToWindowsExample15$ make  make -f Makefile.Release make[1]: Entering directory `/home/richel/qtsdk-2010.04/bin/Projects/Website/CppQtCrosscompileToWindowsExample15' i686-pc-mingw32-g++ -c -pipe -O2 -frtti -fexceptions -mthreads -Wall -DUNICODE -DQT_LARGEFILE_SUPPORT -DQT_NO_DEBUG -DQT_CORE_LIB -DQT_THREAD_SUPPORT -I'/home/richel/mingw-cross-env-2.15/usr/i686-pc-mingw32/include/QtCore' -I'/home/richel/mingw-cross-env-2.15/usr/i686-pc-mingw32/include' -I'/home/richel/mingw-cross-env-2.15/usr/i686-pc-mingw32/include/ActiveQt' -I'release' -I'/home/richel/mingw-cross-env-2.15/usr/i686-pc-mingw32/mkspecs/unsupported/win32-g++-cross' -o release/main.o main.cpp i686-pc-mingw32-g++ -enable-stdcall-fixup -Wl,-enable-auto-import -Wl,-enable-runtime-pseudo-reloc -Wl,-s -Wl,-subsystem,console -mthreads -Wl -o release/CppQtCrosscompileToWindowsExample15.exe release/main.o  -L'/home/richel/mingw-cross-env-2.15/usr/i686-pc-mingw32/lib' -lboost_filesystem-mt -lboost_system-mt -lQtCore -lkernel32 -luser32 -lshell32 -luuid -lole32 -ladvapi32 -lws2_32 -lz  make[1]: Leaving directory `/home/richel/qtsdk-2010.04/bin/Projects/Website/CppQtCrosscompileToWindowsExample15'  richel@richel1-desktop:~/2Projects/Website/CppQtCrosscompileToWindowsExample15$ ``
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Now the Windows executable can be found in the /release folder.

 

 

 

 

 

External links
--------------

 

-   [MinGW cross compiling environment
    homepage](http://mingw-cross-env.nongnu.org)

 

 

 

 

 

Acknowledgements
----------------

 

Thanks to Mark Brand for contacting me: at the first try this approach
failed and Mark let me try this approach again.

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 

 

 

 

 

\[1\] http://mingw-cross-env.nongnu.org/\#tutorial
--------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ``  Tutorial Step 1: Download and Unpack  First, you should ensure that your system meets mingw-cross-env's requirements. You probably need to install some stuff.  When everything is fine, download the latest release:  wget http://download.savannah.nongnu.org/releases/mingw-cross-env/mingw-cross-env-2.15.tar.gz  and unpack the tarball:  tar -xzvf mingw-cross-env-2.15.tar.gz  If you don't mind installing it in your home directory, just skip the following step and go straight to step 3. Step 2: System-wide Installation (optional)  Now you should save any previous installation of the mingw-cross-env. Assuming you've installed it under /opt/mingw (any other directory will do as well), you should execute the following commands:  su mv /opt/mingw /opt/mingw.old exit  Then you need to transfer the entire directory to its definitive location. We will assume again you use /opt/mingw, but feel free to use any other directory if you like.  su mv mingw-cross-env-2.15 /opt/mingw exit  We're almost done. Just change to your newly created directory and get going:  cd /opt/mingw  Step 3: Build mingw-cross-env  Enter the directory where you've unpacked the mingw-cross-env. Now it depends on what you actually want ? or need.  If you choose to enter:  make  you're in for a long wait, because it compiles a lot of packages. On the other hand it doesn't require any intervention, so you're free to do whatever you like ? like watch a movie or go for a night on the town. When it's done you'll find that you've installed a very capable Win32 cross compiler onto your system.  If you only need the most basic tools you can also use:  make gcc  and add any additional packages you need later on. You can also supply a host of packages on the command line, e.g.:  make gtk lua libidn  You'll always end up with a consistent cross compiling environment.  After you're done it just needs a little post-installation. Step 4: Environment Variables  Edit your .bashrc script in order to change $PATH:  export PATH=/where mingw-cross-env is installed/usr/bin:$PATH  Note that any compiler related environment variables (like $CC, $LDFLAGS, etc.) may spoil your compiling pleasure, so be sure to delete or disable those.  Congratulations! You're ready to cross compile anything you like. Step 5a: Cross compile your Project (Autotools)  If you use the Autotools, all you have to do is:  ./configure --host=i686-pc-mingw32 make  Don't worry about a warning like this:  configure: WARNING: If you wanted to set the --build type, don't use --host. If a cross compiler is detected then cross compile mode will be used.  Everything will be just fine. Step 5b: Cross compile your Project (Qt)  If you have a Qt application, all you have to do is:  i686-pc-mingw32-qmake make  If you are using Qt plugins such as database drivers or graphics plugins, you should also have a look at the Qt documentation about static plugins. Step 5c: Cross compile your Project (Makefile)  If you have a handwritten Makefile, you probably will have to make a few adjustments to it:  CC=$(CROSS)gcc LD=$(CROSS)ld AR=$(CROSS)ar  You may have to add a few others, depending on your project.  Then, all you have to do is:  make CROSS=i686-pc-mingw32-  That's it! Step 5d: Cross compile your Project (OSG)  Using static OpenSceneGraph libraries requires a few changes to your source. The graphics subsystem and all plugins required by your application must be referenced explicitly. Use a code block like the following:  #ifdef OSG_LIBRARY_STATIC USE_GRAPHICSWINDOW() USE_OSGPLUGIN(<plugin1>) USE_OSGPLUGIN(<plugin2>) ... #endif  Look at examples/osgstaticviewer/osgstaticviewer.cpp in the OpenSceneGraph source distribution for an example. This example can be compiled with the following command:  i686-pc-mingw32-g++ \     -o osgstaticviewer.exe examples/osgstaticviewer/osgstaticviewer.cpp \     `i686-pc-mingw32-pkg-config --cflags openscenegraph-osgViewer openscenegraph-osgPlugins` \     `i686-pc-mingw32-pkg-config --libs openscenegraph-osgViewer openscenegraph-osgPlugins`  The i686-pc-mingw32-pkg-config command from mingw-cross-env will automatically add -DOSG_LIBRARY_STATIC to your compiler flags.  ``
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 


