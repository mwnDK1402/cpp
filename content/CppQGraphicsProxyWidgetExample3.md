
 

 

 

 

 

([C++](Cpp.md)) ![Qt](PicQt.png) [QGraphicsProxyWidget example 3](CppQGraphicsProxyWidgetExample3.md)
=======================================================================================================

 

[QGraphicsProxyWidget example 3](CppQGraphicsProxyWidgetExample3.md) is
a [QGraphicsProxyWidget](CppQGraphicsProxyWidget.md) example.

 

-   ![Lubuntu](PicLubuntu.png) [View a screenshot of
    'CppQGraphicsProxyWidgetExample3' (png)](CppQGraphicsProxyWidgetExample3.png)
-   ![Wine](PicWine.png) [View a screenshot of
    'CppQGraphicsProxyWidgetExample3' (png)](CppQGraphicsProxyWidgetExample3Wine.png)
-   ![Qt Creator](PicQtCreator.png) [Download the Qt Creator project
    'CppQGraphicsProxyWidgetExample3' (zip)](CppQGraphicsProxyWidgetExample3.zip)
-   ![Windows](PicWindows.png) [Download the Windows executable of
    'CppQGraphicsProxyWidgetExample3' (zip)](CppQGraphicsProxyWidgetExample3Exe.zip)

 

 

 

 

 

Technical facts
---------------

 

[Application type(s)](CppApplication.md)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.md)

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 12.10 (quantal)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 2.5.2

[Project type](CppQtProjectType.md):

-   ![GUI](PicGui.png) [GUI application](CppGuiApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.7.2

[Libraries](CppLibrary.md) used:

-   ![Qt](PicQt.png) [Qt](CppQt.md): version 4.8.3 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.7.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): CppQGraphicsProxyWidgetExample3.pro
----------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` QT       += core QT       += gui QMAKE_CXXFLAGS += -Wextra -Werror TARGET = CppQGraphicsProxyWidgetExample3 CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp `
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

main.cpp
--------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <cmath> #include <QApplication> #include <QDesktopWidget> #include <QGraphicsProxyWidget> #include <QGraphicsScene> #include <QGraphicsView> #include <QLineEdit> #include <QLabel> #include <QVBoxLayout> #include <QDialog> #include <QGraphicsSceneMouseEvent> #include <QPointer>  struct MyWidget : public QDialog {   MyWidget(QWidget *parent = 0, Qt::WindowFlags f = 0)     : QDialog(parent,f),       m_edit(new QLineEdit(this)),       m_label(new QLabel(this))   {     assert(!this->layout());     QVBoxLayout * const layout = new QVBoxLayout(this);     this->setLayout(layout);     layout->addWidget(m_label);     layout->addWidget(m_edit);   }   QLineEdit * const m_edit;   QLabel * const m_label; };  int main(int argc, char **argv) {   //Create the application   QApplication app(argc, argv);    //Create the Qt Graphics Framework components   QGraphicsScene scene;   QGraphicsView view(&scene);   view.setGeometry(0,0,600,400);   {     //Put the dialog in the screen center     const QRect screen = QApplication::desktop()->screenGeometry();     view.move( screen.center() - view.rect().center() );   }   view.show();    //Create the QLineEdit instances   const int sz = 10;   std::vector<QGraphicsProxyWidget *> proxies;   for (int i=0; i!=sz; ++i)   {     MyWidget * const mywidget = new MyWidget;     mywidget->setGeometry(0,0,64,22);     mywidget->m_label->setText(QString("#") + QString::number(i));     mywidget->m_edit->setText(QString("Text ") + QString::number(i));     //Add the QWidget and obtain its proxy     QGraphicsProxyWidget * const proxy = scene.addWidget(mywidget,Qt::Window);     proxies.push_back(proxy);   }    const double ray = 150.0; //pixels   for (int i=0; i!=sz; ++i)   {     const double angle = 2.0 * M_PI * static_cast<double>(i) / static_cast<double>(sz);     const int x = static_cast<int>(0.0 + (std::sin(angle) * ray));     const int y = static_cast<int>(0.0 - (std::cos(angle) * ray));     QGraphicsProxyWidget * const proxy = proxies[i];     proxy->setRotation(angle * 360.0 / (2.0 * M_PI));     proxy->setPos(x,y);     //proxy->setFlag(QGraphicsItem::ItemIsMovable,true); //No need to set this flag   }   return app.exec(); } `
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

