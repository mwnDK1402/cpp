



 

 

 

 

 

([C++](Cpp.md)) [IntToStr](CppIntToStr.md)
============================================

 

[IntToStr](CppIntToStr.md) is a [code snippet](CppCodeSnippets.md) to
[convert](CppConvert.md) an [int](CppInt.md) to
[std::string](CppStdString.md). To [convert](CppConvert.md) a
[std::string](CppStdString.md) to [int](CppInt.md), use
[StrToInt](CppStrToInt.md).

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

-   ![C++11](PicCpp11.png) [C++11](Cpp11.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![Qt](PicQt.png) [Qt](CppQt.md): version 5.4.1 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppIntToStr/CppIntToStr.pro
----------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2011-08-05T19:31:46 # #------------------------------------------------- QT       += core QT       -= gui QMAKE_CXXFLAGS += -std=c++0x TARGET = CppIntToStr CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppIntToStr/main.cpp
----------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <string>  //From http://www.richelbilderbeek.nl/CppIntToStr.htm std::string IntToStrCpp0x(const int x) {   return std::to_string(x); }  #include <sstream> #include <stdexcept> #include <string>  //From http://www.richelbilderbeek.nl/CppIntToStr.htm std::string IntToStrCpp98(const int x) {   std::ostringstream s;   if (!(s << x)) throw std::logic_error("IntToStr failed");   return s.str(); }  #include <string> #include <boost/lexical_cast.hpp>  //From http://www.richelbilderbeek.nl/CppIntToStr.htm std::string IntToStrBoost(const int x) {   return boost::lexical_cast<std::string>(x); }  #include <cassert>  int main() {   assert(IntToStrCpp0x(123) == "123");   assert(IntToStrBoost(123) == "123");   assert(IntToStrCpp98(123) == "123");    assert(IntToStrCpp0x(-123) == "-123");   assert(IntToStrBoost(-123) == "-123");   assert(IntToStrCpp98(-123) == "-123");    assert(IntToStrCpp0x(0) == "0");   assert(IntToStrBoost(0) == "0");   assert(IntToStrCpp98(0) == "0"); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)