



 

 

 

 

 

([C++](Cpp.md)) [GmtlExample1](CppGmtlExample1.md)
====================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppGmtlExample1/CppGmtlExample1.pro
------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp  # # # gmtl # #  unix {   message(Unix: gmtl: not tested) }  win32 {   message(Windows: gmtl: include path)   INCLUDEPATH+= ../../Libraries/gmtl-0.6.1 }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppGmtlExample1/main.cpp
--------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <iostream> #include <gmtl/gmtl.h>  int main() {   const gmtl::Vec3f a { 1.0, 2.0,  3.0 };   const gmtl::Vec3f b { 4.0, 8.0, 12.0 };   gmtl::Vec3f result;    const float w = 1.0 / 3.0;    ///Obtain the weighted vector between a and b, closest to a:   /// a[1] = 2.0   /// b[1] = 8.0   /// w    = 1.0 / 3.0                       //weight   /// d    = b[1] - a[1] = 6.0               //distance between a[1] and b[1]   /// d_a  = w * d = (1.0 / 3.0) * 6.0 = 2.0 //distance from a[1]   /// r[1] = a[1] + d_a = 2.0 + 2.0 = 4;     //resulting value   gmtl::lerp( result, w, a, b );    const double e = 0.000001;   assert(result[0] > 2.0 - e && result[0] < 2.0 + e);   assert(result[1] > 4.0 - e && result[1] < 4.0 + e);   assert(result[2] > 6.0 - e && result[2] < 6.0 + e); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)