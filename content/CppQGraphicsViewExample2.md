



 

 

 

 

 

([C++](Cpp.md)) [QGraphicsViewExample2](CppQGraphicsViewExample2.md)
======================================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQGraphicsViewExample2/CppQGraphicsViewExample2.pro
------------------------------------------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------
  ` include(../../DesktopApplication.pri)  SOURCES += qtmain.cpp \     grabber.cpp  HEADERS += \     grabber.h`
  ---------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsViewExample2/grabber.h
------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef GRABBER_H #define GRABBER_H  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <QObject> #pragma GCC diagnostic pop  struct Grabber : public QObject {   Q_OBJECT    public:   Grabber(     const int win_id,     const std::string& filename = "screengrab.png"   );   ~Grabber() noexcept;    public slots:   void Grab() const noexcept;    private:   const std::string m_filename;   const int m_win_id; };  #endif // GRABBER_H`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsViewExample2/grabber.cpp
--------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "grabber.h"  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <QImage> #include <QPixmap> #pragma GCC diagnostic pop  Grabber::Grabber(   const int win_id,   const std::string& filename )   : m_filename{filename},     m_win_id{win_id} {  }  Grabber::~Grabber() noexcept {}  void Grabber::Grab() const noexcept {   const QImage screenshot{QPixmap::grabWindow(m_win_id).toImage()};   screenshot.save(m_filename.c_str()); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQGraphicsViewExample2/qtmain.cpp
-------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include <QApplication> #include <QGraphicsView> #include <QGraphicsSimpleTextItem> #include <QTimer> #include "grabber.h" #pragma GCC diagnostic pop    int main(int argc, char *argv[]) {   QApplication a(argc, argv);   QGraphicsScene s;   QGraphicsSimpleTextItem t;   t.setText("To be grabbed...");   t.setFlags(       QGraphicsItem::ItemIsSelectable     | QGraphicsItem::ItemIsMovable);    s.addItem(&t);   QGraphicsView v(&s);   v.setGeometry(100,100,400,100);   v.show();    Grabber g(     v.winId(),     "CppQGraphicsViewExample2Screengrab.png"   );   QTimer::singleShot(1000,&g,SLOT(Grab()));    return a.exec(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)