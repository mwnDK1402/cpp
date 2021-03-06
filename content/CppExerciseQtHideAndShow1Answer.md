
 

 

 

 

 

([C++](Cpp.md)) [Answer of exercise: Qt hide and show \#1](CppExerciseQtHideAndShow1Answer.md)
================================================================================================

 

[Answer of exercise: Qt hide and show
\#1](CppExerciseQtHideAndShow1Answer.md) is the answer of the
[exercise](CppExercise.md) [Qt hide and show
\#1](CppExerciseQtHideAndShow1.md).

 

 

 

 

 

Solution
--------

 

-   [Download the Qt Creator project
    'CppExerciseQtHideAndShow1Answer' (zip)](CppExerciseQtHideAndShow1Answer.zip)

 

The uninteded behavior is coded in [main](CppMain.md):

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QtGui/QApplication> #include "firstdialog.h"  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   FirstDialog w;   w.exec(); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------

 

I think that this means, that at the moment when FirstDialog is hidden
(for showing the second dialog) and the second dialog closes,
FirstDialog::exec finishes with an error code of zero.

 

Instead, I want that that moment is bridged until the first dialog
closes. In that case [main](CppMain.md) should be:

 

main.cpp
--------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QtGui/QApplication> #include "firstdialog.h"  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   FirstDialog w;   w.show();   a.exec(); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

