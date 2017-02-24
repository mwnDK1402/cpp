



 

 

 

 

 

([C++](Cpp.md)) [QmlClaudioExample](CppQmlClaudioExample.md)
==============================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQmlClaudioExample/CppQmlClaudioExample.pro
----------------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app  QT += qml quick  SOURCES += main.cpp  RESOURCES += qml.qrc  # Additional import path used to resolve QML modules in Qt Creator's code model QML_IMPORT_PATH =  # Default rules for deployment. include(deployment.pri)`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/deployment.pri
-------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` android-no-sdk {     target.path = /data/user/qt     export(target.path)     INSTALLS += target } else:android {     x86 {         target.path = /libs/x86     } else: armeabi-v7a {         target.path = /libs/armeabi-v7a     } else {         target.path = /libs/armeabi     }     export(target.path)     INSTALLS += target } else:unix {     isEmpty(target.path) {         qnx {             target.path = /tmp/$${TARGET}/bin         } else {             target.path = /opt/$${TARGET}/bin         }         export(target.path)     }     INSTALLS += target }  export(INSTALLS)`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/main.cpp
-------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QGuiApplication> #include <QQmlApplicationEngine>  int main(int argc, char *argv[]) {     QGuiApplication app(argc, argv);      QQmlApplicationEngine engine;     engine.load(QUrl(QStringLiteral("qrc:///main.qml")));      return app.exec(); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/timer.h
------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef TIMER_H #define TIMER_H  #include <QObject>  class Timer : public QObject {     Q_OBJECT public:     explicit Timer(QObject *parent = 0);  signals:  public slots:  };  #endif // TIMER_H`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/timer.cpp
--------------------------------

 

  --------------------------------------------------------------------------------
  ` #include "timer.h"  Timer::Timer(QObject *parent) :     QObject(parent) { }`
  --------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)