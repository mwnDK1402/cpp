



 

 

 

 

 

([C++](Cpp.md)) [PdcursesExample1](CppPdcursesExample1.md)
============================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Windows](PicWindows.png)

 

[PDCurses example 1: tutorial](CppPdcursesExample1.md) is a
[PDCurses](CppPdcurses.md) example that is a slight modification of a
tutorial its code.

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppPdcursesExample1/CppPdcursesExample1.pro
--------------------------------------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  include(../../Libraries/Pdcurses.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #       ../../Libraries/pdc25_vc_w32 # #   HEADERS += \ #       ../../Libraries/pdc25_vc_w32/panel.h \ #       ../../Libraries/pdc25_vc_w32/curses.h # #   LIBS += -L../../Libraries/pdc25_vc_w32 -lpdcurses # }  SOURCES += main.cpp`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppPdcursesExample1/main.cpp
------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //Code adapted from http://invisible-island.net/ncurses/ncurses-intro.html  #include <cassert> #include <cstdlib> #include <csignal>  #include "curses.h"  static void finish(int sig);  int main() {   int num = 0;    /* initialize your non-curses data structures here */    std::signal(SIGINT, finish);      /* arrange interrupts to terminate */   initscr();      /* initialize the curses library */   keypad(stdscr, TRUE);  /* enable keyboard mapping */   cbreak();       /* take input chars one at a time, no wait for \n */   echo();         /* echo input - in color */    if (has_colors())   {     start_color();      /*     * Simple color assignment, often all we need.  Color pair 0 cannot     * be redefined.  This example uses the same value for the color     * pair as for the foreground color, though of course that is not     * necessary:     */     init_pair(1, COLOR_RED,     COLOR_BLACK);     init_pair(2, COLOR_GREEN,   COLOR_BLACK);     init_pair(3, COLOR_YELLOW,  COLOR_BLACK);     init_pair(4, COLOR_BLUE,    COLOR_BLACK);     init_pair(5, COLOR_CYAN,    COLOR_BLACK);     init_pair(6, COLOR_MAGENTA, COLOR_BLACK);     init_pair(7, COLOR_WHITE,   COLOR_BLACK);   }    for (;;)   {     int c = getch();     /* refresh, accept single keystroke of input */     attrset(COLOR_PAIR(num % 8));     num++;      /* process the command keystroke */     if (c == KEY_DOWN) finish(0);   }    finish(0);               /* we're done */ }  static void finish(int sig) {   endwin();    /* do your non-curses wrapup here */    std::exit(sig); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)