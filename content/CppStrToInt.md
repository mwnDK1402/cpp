



 

 

 

 

 

([C++](Cpp.md)) [StrToInt](CppStrToInt.md)
============================================

 

[StrToInt](CppStrToInt.md) is a [code snippet](CppCodeSnippets.md) to
[convert](CppConvert.md) a [std::string](CppStdString.md) to
[int](CppInt.md). [IntToStr](CppIntToStr.md)
[converts](CppConvert.md) an [int](CppInt.md) to
[std::string](CppStdString.md).

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStrToInt/CppStrToInt.pro
----------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2011-08-05T09:15:49 # #------------------------------------------------- QT       += core QT       -= gui QMAKE_CXXFLAGS += -std=c++0x TARGET = CppStrToInt CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStrToInt/main.cpp
----------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <string>  //From http://www.richelbilderbeek.nl/CppStrToInt.htm int StrToIntStl(const std::string& s) {   return std::atoi(s.c_str()); }  //From http://www.richelbilderbeek.nl/CppStrToInt.htm int StrToIntCpp0x(const std::string& s) {   return std::stoi(s); }  #include <boost/lexical_cast.hpp>  //From http://www.richelbilderbeek.nl/CppStrToInt.htm int StrToIntBoost(const std::string& s) {   return boost::lexical_cast<int>(s); }  bool CanStrToIntStl(const std::string& s) {   const int i = std::atoi(s.c_str());   return i!=0 || s=="0"; }  int CanStrToIntCpp0x(const std::string& s) {   try { std::stoi(s); }   catch (std::exception&) { return false; }   return true; }  int CanStrToIntBoost(const std::string& s) {   try { boost::lexical_cast<int>(s); }   catch (boost::bad_lexical_cast&) { return false; }   return true;  }  #include <cassert>  int main() {   assert(!CanStrToIntStl("a"));   assert(!CanStrToIntCpp0x("a"));   assert(!CanStrToIntBoost("a"));    assert(CanStrToIntStl("0"));   assert(CanStrToIntCpp0x("0"));   assert(CanStrToIntBoost("0"));    assert(CanStrToIntStl("123"));   assert(CanStrToIntCpp0x("123"));   assert(CanStrToIntBoost("123"));    const std::string s = "123";   assert(StrToIntStl(s) == StrToIntCpp0x(s));   assert(StrToIntStl(s) == StrToIntBoost(s)); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)