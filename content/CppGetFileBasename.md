



 

 

 

 

 

([C++](Cpp.md)) [GetFileBasename](CppGetFileBasename.md)
==========================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppGetFileBasename/CppGetFileBasename.pro
------------------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) include(../../Libraries/BoostAll.pri)  SOURCES += main.cpp`
  -----------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppGetFileBasename/main.cpp
-----------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/filesystem.hpp> #include <boost/xpressive/xpressive.hpp> #pragma GCC diagnostic pop  std::string GetFileBasenameBoostFilesystem(const std::string& filename) {   return boost::filesystem::basename(filename); }  std::string GetFileBasenameBoostXpressive(const std::string& filename) {   const boost::xpressive::sregex rex     = boost::xpressive::sregex::compile(       "((.*)(/|\\\\))?([0-9A-Za-z_]*)((\\.)([A-Za-z]*))?" );   boost::xpressive::smatch what;    if( boost::xpressive::regex_match( filename, what, rex ) )   {     return what[4];   }    return ""; }  int main() {   //Tests for easy copy-paste   assert(GetFileBasenameBoostFilesystem("") == std::string(""));   assert(GetFileBasenameBoostFilesystem("tmp.txt") == std::string("tmp"));   assert(GetFileBasenameBoostFilesystem("test_output.fas") == std::string("test_output"));   assert(GetFileBasenameBoostFilesystem("test_output_0.fas") == std::string("test_output_0"));   assert(GetFileBasenameBoostFilesystem("tmp") == std::string("tmp"));   assert(GetFileBasenameBoostFilesystem("MyFolder/tmp") == std::string("tmp"));   assert(GetFileBasenameBoostFilesystem("MyFolder/tmp.txt") == std::string("tmp"));   //assert(GetFileBasenameBoostFilesystem("MyFolder\\tmp.txt") == std::string("tmp"));   assert(GetFileBasenameBoostFilesystem("MyFolder/MyFolder/tmp") == std::string("tmp"));   assert(GetFileBasenameBoostFilesystem("MyFolder/MyFolder/tmp.txt") == std::string("tmp"));   //assert(GetFileBasenameBoostFilesystem("MyFolder/MyFolder\\tmp.txt") == std::string("tmp"));    assert(GetFileBasenameBoostXpressive("") == std::string(""));   assert(GetFileBasenameBoostXpressive("tmp.txt") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("test_output.fas") == std::string("test_output"));   assert(GetFileBasenameBoostXpressive("test_output_0.fas") == std::string("test_output_0"));   assert(GetFileBasenameBoostXpressive("tmp") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("MyFolder/tmp") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("MyFolder/tmp.txt") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("MyFolder\\tmp.txt") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("MyFolder/MyFolder/tmp") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("MyFolder/MyFolder/tmp.txt") == std::string("tmp"));   assert(GetFileBasenameBoostXpressive("MyFolder/MyFolder\\tmp.txt") == std::string("tmp")); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)