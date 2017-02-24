



 

 

 

 

 

([C++](Cpp.md)) [ArduinoExample1](CppArduinoExample1.md)
==========================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Arduino](PicArduino.png)

 

[Arduino example 1](CppArduinoExample1.md) is an
[Arduino](CppArduino.md) [example](CppExample.md).

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppArduinoExample1/CppArduinoExample1.pro
------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  INCLUDEPATH += ../../Libraries/Arduino/hardware/arduino/cores/arduino  SOURCES += \     mymain.cpp \     ../../Libraries/Arduino/hardware/arduino/cores/main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppArduinoExample1/mymain.cpp
-------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <wiring_digital.h>  //int main is defined in ../../Libraries/Arduino/hardware/arduino/cores/main.cpp //so only need to implement loop and setup void setup() {   pinMode(3,OUTPUT); }  void loop() {   digitalWrite(3,HIGH);   delay(1000);   digitalWrite(3,LOW);   delay(1000); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)