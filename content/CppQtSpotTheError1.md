



 

 

 

 

 

([C++](Cpp.md)) ![Qt](PicQt.png) [Spot The Error 1](CppQtSpotTheError1.md)
============================================================================

 

Try to [Spot The Error](CppQtSpotTheError.md)...

 

-   [Download the Qt Creator project
    'CppQtSpotTheError1' (zip)](CppQtSpotTheError1.zip)

 

 

 

 

 

Project and source code
-----------------------

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.md): [Qt Creator](CppQt.md) 2.0.0

[Project type](CppQtProjectType.md): Qt4 GUI Application

[Compiler](CppCompiler.md): [G++](CppGpp.md) 4.4.1

[Libraries](CppLibrary.md) used:

-   [Qt](CppQt.md): version 4.7.0 (32 bit)

 

 

 

 

 

### main.cpp

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QtGui/QApplication> #include "dialog.h"  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   Dialog w;   w.show();   return a.exec(); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

### dialog.h

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef DIALOG_H #define DIALOG_H  #include <QDialog>  namespace Ui {     class Dialog; }  class Dialog : public QDialog {     Q_OBJECT  public:     explicit Dialog(QWidget *parent = 0);     ~Dialog();  protected:     void changeEvent(QEvent *e);  private:     Ui::Dialog *ui;  private slots:     void keyPressEvent(QKeyEvent * e); };  #endif // DIALOG_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

### dialog.cpp

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QKeyEvent>  #include "dialog.h" #include "ui_dialog.h"  Dialog::Dialog(QWidget *parent) :     QDialog(parent),     ui(new Ui::Dialog) {     ui->setupUi(this); }  Dialog::~Dialog() {     delete ui; }  void Dialog::changeEvent(QEvent *e) {     QDialog::changeEvent(e);     switch (e->type()) {     case QEvent::LanguageChange:         ui->retranslateUi(this);         break;     default:         break;     } }  void QDialog::keyPressEvent(QKeyEvent * e) {   switch (e->type())   {     case QEvent::KeyPress:       this->setWindowTitle("Key pressed: " + e->key());       break;     case QEvent::KeyRelease:       this->setWindowTitle("Key released: " + e->key());       break;     default:       break;   } }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 


