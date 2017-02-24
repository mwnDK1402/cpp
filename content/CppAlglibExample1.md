



 

 

 

 

 

([C++](Cpp.md)) [AlglibExample1](CppAlglibExample1.md)
========================================================

 

![STL](PicStl.png)![Qt Creator](PicQtCreator.png)

 

[ALGLIB example 1: linear fit](CppAlglibExample1.md) is an
[ALGLIB](CppAlglib.md) [example](CppExample.md).

 

-   [Download the Qt Creator project
    'CppAlglibExample1' (zip)](CppAlglibExample1.zip)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppAlglibExample1/CppAlglibExample1.pro
----------------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp  # # # alglib # #  unix {   message(Lubuntu: alglib not tested)  }  win32 {   message(Windows: alglib: include path)   INCLUDEPATH += ../../Libraries/alglib-3.8.0/src  SOURCES += \     ../../Libraries/alglib-3.8.0/src/statistics.cpp \     ../../Libraries/alglib-3.8.0/src/specialfunctions.cpp \     ../../Libraries/alglib-3.8.0/src/solvers.cpp \     ../../Libraries/alglib-3.8.0/src/optimization.cpp \     ../../Libraries/alglib-3.8.0/src/linalg.cpp \     ../../Libraries/alglib-3.8.0/src/interpolation.cpp \     ../../Libraries/alglib-3.8.0/src/integration.cpp \     ../../Libraries/alglib-3.8.0/src/fasttransforms.cpp \     ../../Libraries/alglib-3.8.0/src/diffequations.cpp \     ../../Libraries/alglib-3.8.0/src/dataanalysis.cpp \     ../../Libraries/alglib-3.8.0/src/ap.cpp \     ../../Libraries/alglib-3.8.0/src/alglibmisc.cpp \     ../../Libraries/alglib-3.8.0/src/alglibinternal.cpp  HEADERS += \     ../../Libraries/alglib-3.8.0/src/statistics.h \     ../../Libraries/alglib-3.8.0/src/specialfunctions.h \     ../../Libraries/alglib-3.8.0/src/solvers.h \     ../../Libraries/alglib-3.8.0/src/optimization.h \     ../../Libraries/alglib-3.8.0/src/linalg.h \     ../../Libraries/alglib-3.8.0/src/interpolation.h \     ../../Libraries/alglib-3.8.0/src/integration.h \     ../../Libraries/alglib-3.8.0/src/fasttransforms.h \     ../../Libraries/alglib-3.8.0/src/diffequations.h \     ../../Libraries/alglib-3.8.0/src/dataanalysis.h \     ../../Libraries/alglib-3.8.0/src/ap.h \     ../../Libraries/alglib-3.8.0/src/alglibmisc.h \     ../../Libraries/alglib-3.8.0/src/alglibinternal.h }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppAlglibExample1/main.cpp
----------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` ///Adapted from http://www.alglib.net/translator/man/manual.cpp.html#lsfit_d_lin%20example  #include <cassert> #include <iostream> #include "interpolation.h"  int main() {   //   // In this example we demonstrate linear fitting by f(x|a) = a*exp(0.5*x).   //   // We have:   // * y - vector of experimental data   // * fmatrix -  matrix of basis functions calculated at sample points   //              Actually, we have only one basis function F0 = exp(0.5*x).   //   const alglib::real_2d_array fmatrix = "[[0.606531],[0.670320],[0.740818],[0.818731],[0.904837],[1.000000],[1.105171],[1.221403],[1.349859],[1.491825],[1.648721]]";   const alglib::real_1d_array y = "[1.133719, 1.306522, 1.504604, 1.554663, 1.884638, 2.072436, 2.257285, 2.534068, 2.622017, 2.897713, 3.219371]";   alglib::ae_int_t info;   alglib::real_1d_array c;   alglib::lsfitreport rep;    //   // Linear fitting without weights   //    alglib::lsfitlinear(y, fmatrix, info, c, rep);    assert(info == 1);   assert(c.tostring(4) == std::string("[1.9865]")); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)