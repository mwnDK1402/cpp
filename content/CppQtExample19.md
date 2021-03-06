
 

 

 

 

 

([C++](Cpp.md)) [QtExample19](CppQtExample19.md)
==================================================

 

![Qt](PicQt.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![Ubuntu](PicUbuntu.png)

 

This [Qt](CppQt.md) example shows how to create a GUI around a program
that displays a rotating image, like [this screenshot
(png)](CppQtExample19.png).

 

-   [Download the Qt Project of 'QtExample19' (zip)](CppQtExample19.zip)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQtExample19/CppQtExample19.pro
----------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists(../../DesktopApplication.pri) {   include(../../DesktopApplication.pri) } !exists(../../DesktopApplication.pri) {   QT += core gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   TEMPLATE = app    CONFIG(debug, debug|release) {     message(Debug mode)   }    CONFIG(release, debug|release) {     message(Release mode)     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }    QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra    unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../../Projects/Libraries/boost_1_55_0   } }  SOURCES += main.cpp SOURCES += dialogmain.cpp HEADERS += dialogmain.h FORMS   += dialogmain.ui RESOURCES += resources.qrc`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample19/dialogmain.h
-----------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef DIALOGMAIN_H #define DIALOGMAIN_H  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QDialog> #pragma GCC diagnostic pop  struct QGraphicsScene; struct QGraphicsPixmapItem;  namespace Ui {   class DialogMain; }  class DialogMain : public QDialog {   Q_OBJECT  public:   explicit DialogMain(QWidget *parent = 0);   DialogMain(const DialogMain&) = delete;   DialogMain& operator=(const DialogMain&) = delete;   ~DialogMain();  private:   Ui::DialogMain *ui;   QTimer * const m_timer;   QGraphicsScene * const m_scene;   QGraphicsPixmapItem * const m_sprite;   double m_angle;     void resizeEvent(QResizeEvent*);   void keyPressEvent(QKeyEvent* e);  private slots:   void onTick();   void onCheck();   void onButtonLeft();   void onButtonRight(); };  #endif // DIALOGMAIN_H`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample19/dialogmain.cpp
-------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "dialogmain.h"  #include <cassert> #include <cmath> #include <iostream>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QDesktopWidget> #include <QGraphicsPixmapItem> #include <QGraphicsScene> #include <QKeyEvent> #include <QTimer>  #include "ui_dialogmain.h" #pragma GCC diagnostic pop  DialogMain::DialogMain(QWidget *parent) :   QDialog(parent),   ui(new Ui::DialogMain),   m_timer(new QTimer(this)),   m_scene(new QGraphicsScene(this)),   m_sprite(new QGraphicsPixmapItem),   m_angle(0.0) {   ui->setupUi(this);    //Load the sprite   m_sprite->setPixmap(QPixmap(":/images/R.png"));   assert(!m_sprite->pixmap().isNull());    //Set the center of the sprite for rotation   m_sprite->setTransformOriginPoint(     static_cast<double>(m_sprite->pixmap().width()) / 2.0,     static_cast<double>(m_sprite->pixmap().height()) / 2.0);    //Add the sprite to the scene   m_scene->addItem(m_sprite);    //Add the scene to the view   ui->graphicsView->setScene(m_scene);    //Connect and start a timer   QObject::connect(m_timer,SIGNAL(timeout()),this,SLOT(onTick()));   QObject::connect(ui->check_auto_rotate,SIGNAL(clicked()),this,SLOT(onCheck()));   QObject::connect(ui->button_left,SIGNAL(clicked()),this,SLOT(onButtonLeft()));   QObject::connect(ui->button_right,SIGNAL(clicked()),this,SLOT(onButtonRight()));     //Start the timer   m_timer->start(100);    this->setGeometry(0,0,     static_cast<int>(640),     static_cast<int>(640));   const QRect screen = QApplication::desktop()->screenGeometry();   this->move( screen.center() - this->rect().center() ); }  DialogMain::~DialogMain() {   delete ui;   delete m_sprite; }  //Sets the scale of the maze void DialogMain::resizeEvent(QResizeEvent*) {   const int size = std::max(     m_sprite->pixmap().width(),     m_sprite->pixmap().height());    const double scale = 0.9     * std::min(ui->graphicsView->width(),         ui->graphicsView->height())     / (static_cast<double>(size) * std::sqrt(2.0));   m_sprite->setScale(scale); }  void DialogMain::keyPressEvent(QKeyEvent* e) {   switch (e->key())   {     case Qt::Key_Left: case Qt::Key_Minus: case Qt::Key_A:       m_angle-=1.0;       m_sprite->setRotation(m_angle);       break;     case Qt::Key_Right: case Qt::Key_Plus: case Qt::Key_D:       m_angle+=1.0;       m_sprite->setRotation(m_angle);       break;   } }  void DialogMain::onTick() {   m_angle+=1.0;   m_sprite->setRotation(m_angle); }  void DialogMain::onCheck() {   if (ui->check_auto_rotate->isChecked())   {     m_timer->start();   }   else   {     m_timer->stop();   }  }  void DialogMain::onButtonLeft() {   m_angle-=1.0;   m_sprite->setRotation(m_angle); }  void DialogMain::onButtonRight() {   m_angle+=1.0;   m_sprite->setRotation(m_angle); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExample19/main.cpp
-------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QApplication> #include "dialogmain.h" #pragma GCC diagnostic pop  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   DialogMain w;   w.show();   return a.exec(); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

