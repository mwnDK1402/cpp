



 

 

 

 

 

([C++](Cpp.md)) [BoostUnitsExample3](CppBoostUnitsExample3.md)
================================================================

 

![Cpp98](PicCpp98.png)![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![Windows](PicWindows.png)

 

[Boost.Units example 3: creating a Length, Width and Area
classes](CppBoostUnitsExample3.md) is a
[Boost.Units](CppBoostUnits.md) example.

 

-   [Download the Qt Creator project
    'CppBoostUnitsExample3' (zip)](CppBoostUnitsExample3.zip)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppBoostUnitsExample3/CppBoostUnitsExample3.pro
------------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostUnitsExample3/main.cpp
--------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <iostream>  #include <boost/units/systems/si/prefixes.hpp> #include <boost/units/systems/si/length.hpp> #include <boost/units/systems/si/io.hpp> #include <boost/units/physical_dimensions/area.hpp>  struct Length {   Length(const boost::units::quantity<boost::units::si::length>& length) : m_length(length)   {     const boost::units::quantity<boost::units::si::length> zero(0);     assert(m_length >= zero);   }   const boost::units::quantity<boost::units::si::length> m_length; };  struct Width {   Width(const boost::units::quantity<boost::units::si::length>& width) : m_width(width)   {     const boost::units::quantity<boost::units::si::length> zero(0);     assert(m_width >= zero);   }   const boost::units::quantity<boost::units::si::length> m_width; };  struct Area {   Area(const Length& length, const Width& width)     : m_area(length.m_length * width.m_width)   {     assert(length.m_length >= width.m_width);   }   const boost::units::quantity<boost::units::si::area> m_area; };  int main() {   using namespace boost::units;   using namespace boost::units::si;   const Length my_length( quantity<length>(1.23456789*micro*meter) );   const Width my_width( quantity<length>(2.3456789*nano*meter) );   const Area my_area(my_length,my_width);   std::cout     << "Length: " << my_length.m_length << '\n'     << "Width: "  << my_width.m_width << '\n'     << "Area: "   << my_area.m_area << '\n'   ; }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)