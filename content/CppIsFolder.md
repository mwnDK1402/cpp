



 

 

 

 

 

([C++](Cpp.md)) [IsFolder](CppIsFolder.md)
============================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppIsFolder/CppIsFolder.pro
----------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/BoostAll.pri)  SOURCES += main.cpp  RESOURCES += \     CppIsFolder.qrc`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppIsFolder/main.cpp
----------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <string>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QDir>  #include <boost/filesystem.hpp> #pragma GCC diagnostic pop   ///Returns if the name is a folder name //From http://www.richelbilderbeek.nl/CppIsFolder.htm bool IsFolderBoostFilesystem(const std::string& filename) {   return boost::filesystem::is_directory(filename); }  ///Returns if the name is a folder name ///From http://www.richelbilderbeek.nl/CppIsFolder.htm bool IsFolderQt(const std::string& filename) {   return QDir(filename.c_str()).exists(); }  int main(int, char * argv[]) {   assert(!IsFolderBoostFilesystem(argv[0]));   assert(!IsFolderQt(argv[0]));    assert(IsFolderBoostFilesystem("../CppIsFolder"));   assert(IsFolderQt("../CppIsFolder"));    assert(!IsFolderBoostFilesystem("tempfolder"));   assert(!IsFolderQt("tempfolder"));    QDir().mkdir("tempfolder");    assert(IsFolderBoostFilesystem("tempfolder"));   assert(IsFolderQt("tempfolder"));    QDir().rmdir("tempfolder");    assert(!IsFolderBoostFilesystem("tempfolder"));   assert(!IsFolderQt("tempfolder"));    assert(!IsFolderBoostFilesystem(":/images/R.png"));   assert(!IsFolderQt(":/images/R.png")); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)