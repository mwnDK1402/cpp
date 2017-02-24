



 

 

 

 

 

([C++](Cpp.md)) [QtExample2](CppQtExample2.md)
================================================

 

![Qt](PicQt.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![Ubuntu](PicUbuntu.png)

 

[Qt example 2: moving many sprites over a background in
2D](CppQtExample2.md) is a [Qt example](CppQtExample.md) shows an 250
images moving over a background image, like [this screenshot
(png)](CppQtExample2.png).

 

-   [Download the Qt Creator project file
    'CppQtExample2' (zip)](CppQtExample2.zip)

Technical facts
---------------

 

[Application type(s)](CppApplication.md)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.md)

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![GUI](PicGui.png) [GUI application](CppGuiApplication.md)

[C++ standard](CppStandard.md):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![Qt](PicQt.png) [Qt](CppQt.md): version 5.4.1 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQtExample2/CppQtExample2.pro
--------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists(../../DesktopApplication.pri) {   include(../../DesktopApplication.pri) } !exists(../../DesktopApplication.pri) {   QT += core gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   TEMPLATE = app    CONFIG(debug, debug|release) {     message(Debug mode)   }    CONFIG(release, debug|release) {     message(Release mode)     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }    QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra    unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../../Projects/Libraries/boost_1_55_0   } }  RESOURCES += CppQtExample2.qrc  SOURCES += main.cpp`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample2/main.cpp
------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/shared_ptr.hpp>  #include <QApplication> #include <QBitmap> #include <QFile> #include <QGraphicsPathItem> #include <QGraphicsPixmapItem> #include <QGraphicsScene> #include <QGraphicsView> #include <QTimer> #pragma GCC diagnostic pop  struct Background : public QGraphicsPixmapItem {   explicit Background(const std::string& filename)   {     QPixmap m(filename.c_str());     this->setPixmap(m);   } };  struct TransparentSprite : public QGraphicsPixmapItem {   explicit TransparentSprite(     const std::string& filename,     const QColor& transparency_color = QColor(0,255,0)) //Lime green     : dx( ((std::rand() >> 4) % 3) - 1), //Random direction       dy( ((std::rand() >> 4) % 3) - 1), //Random direction       maxx(0),       maxy(0)   {     QPixmap pixmap(filename.c_str());     const QBitmap mask = pixmap.createMaskFromColor(transparency_color);     pixmap.setMask(mask);     this->setPixmap(pixmap);   }   void advance(int)   {     int new_x = this->x();     int new_y = this->y();     new_x+=dx;     new_y+=dy;     if (new_x<0 || new_x>maxx) dx= -dx;     if (new_y<0 || new_y>maxy) dy= -dy;     this->setX(new_x);     this->setY(new_y);   }   void setRect(const int width, const int height)   {     maxx = width - this->pixmap().width();     maxy = height - this->pixmap().height();   }   private:   int dx;   int dy;   int maxx;   int maxy; };  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   QGraphicsScene s;   QGraphicsView v(&s);    assert(QFile::exists(":/images/Bubblegum_2.png"));   Background background(":/images/Bubblegum_2.png");   s.addItem(&background);    std::vector<boost::shared_ptr<TransparentSprite> > sprites;    //Add multiple sprites   const int n_sprites = 250;   for (int i=0; i!=n_sprites; ++i)   {     assert(QFile::exists(":/images/Bloem.png"));     boost::shared_ptr<TransparentSprite> sprite(new TransparentSprite(":/images/Bloem.png"));     const int maxx = background.pixmap().width() - sprite->pixmap().width();     const int maxy = background.pixmap().height() - sprite->pixmap().height();     sprite->setX(std::rand() % maxx);     sprite->setY(std::rand() % maxy);     sprite->setRect(background.pixmap().width(),background.pixmap().height());     s.addItem(sprite.get());     sprites.push_back(sprite);   }    v.show();    boost::shared_ptr<QTimer> timer(new QTimer(&s));   timer->connect(timer.get(), SIGNAL(timeout()), &s, SLOT(advance()));   timer->start(20);    return a.exec(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)