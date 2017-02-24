



 

 

 

 

 

([C++](Cpp.md)) [BoostUnitsExample8](CppBoostUnitsExample8.md)
================================================================

 

![Cpp98](PicCpp98.png)![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![Windows](PicWindows.png)

 

[Boost.Units example 8: calculating mass from a volume and a mass
density](CppBoostUnitsExample8.md) is a
[Boost.Units](CppBoostUnits.md) example.

 

-   [Download the Qt Creator project
    'CppBoostUnitsExample8' (zip)](CppBoostUnitsExample8.zip)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppBoostUnitsExample8/CppBoostUnitsExample8.pro
------------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostUnitsExample8/main.cpp
--------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <iostream> #include <iomanip>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/units/systems/si/mass.hpp> #include <boost/units/systems/si/mass_density.hpp> #include <boost/units/systems/si/volume.hpp> #include <boost/units/systems/si/io.hpp> #pragma GCC diagnostic pop  struct SteelBar {   static const boost::units::quantity<boost::units::si::mass_density> m_density; };  const boost::units::quantity<boost::units::si::mass_density> SteelBar::m_density(   8000.0 * boost::units::si::kilogrammes_per_cubic_metre);  int main() {   //Increase readability   typedef boost::units::quantity<boost::units::si::mass_density> MassDensity;   typedef boost::units::quantity<boost::units::si::mass> Mass;   typedef boost::units::quantity<boost::units::si::volume> Volume;   using boost::units::si::kilogram;   using boost::units::si::kilogrammes_per_cubic_metre;   using boost::units::si::cubic_meter;    const double d = 8000.0; //Density of stainless steel in kg/m^2   const double v = 0.01;   //One litre = 0.01 m^2    const MassDensity mass_density(d * boost::units::si::kilogrammes_per_cubic_metre);   const Volume volume(v * boost::units::si::cubic_meter);   const Mass mass(volume * mass_density);    //Display law   std::cout     << "m = V * d" << "\n"     << "m: " << mass << "\n"     << "V: " << volume << "\n"     << "d: " << mass_density << "\n";    //Check if calculating the force from the plain doubles is identical   const Mass mass_expected(d * v * kilogram);   assert(mass == mass_expected); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)