



 

 

 

 

 

([C++](Cpp.md)) [BoostGeometryExample4](CppBoostGeometryExample4.md)
======================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[Boost.Geometry example 4: CalcPlane: determine the plane passing
through three point](CppBoostGeometryExample4.md) is a
[Boost.Geometry](CppBoostGeometry.md) [example](CppExample.md).

 

CalcCrossProduct and CalcPlane are maintained in
[CppGeometry](CppGeometry.md). See [CppGeometry](CppGeometry.md) for
the heavily used, debugged and tested versions of CalcCrossProduct and
CalcPlane.

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppBoostGeometryExample4/CppBoostGeometryExample4.pro
------------------------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` exists(../../ConsoleApplication.pri) {   include(../../ConsoleApplication.pri) } !exists(../../ConsoleApplication.pri) {   QT += core   QT += gui   greaterThan(QT_MAJOR_VERSION, 4): QT += widgets   CONFIG   += console   CONFIG   -= app_bundle   TEMPLATE = app   CONFIG(release, debug|release) {     DEFINES += NDEBUG NTRACE_BILDERBIKKEL   }   QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++   unix {     QMAKE_CXXFLAGS += -Werror   } }  exists(../../Libraries/Boost.pri) {   include(../../Libraries/Boost.pri) } !exists(../../Libraries/Boost.pri) {   win32 {     INCLUDEPATH += \       ../../Libraries/boost_1_55_0   } }  SOURCES += main.cpp`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostGeometryExample4/main.cpp
-----------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <functional> #include <iostream>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-variable" #include <boost/geometry.hpp> #include <boost/geometry/geometries/point_xy.hpp> #include <boost/geometry/geometries/point.hpp> #pragma GCC diagnostic pop  typedef boost::geometry::model::point<int,3,boost::geometry::cs::cartesian> Point3D;  std::function<bool(const Point3D& lhs, const Point3D& rhs)> OrderByX() noexcept {   return [](const Point3D& lhs, const Point3D& rhs)   {     using boost::geometry::get;     if (get<0>(lhs) < get<0>(rhs)) return true;     if (get<0>(lhs) > get<0>(rhs)) return false;     if (get<1>(lhs) < get<1>(rhs)) return true;     if (get<1>(lhs) > get<1>(rhs)) return false;     return get<2>(lhs) < get<2>(rhs);   }; }  std::function<bool(const Point3D& lhs, const Point3D& rhs)> OrderByZ() noexcept {   return [](const Point3D& lhs, const Point3D& rhs)   {     using boost::geometry::get;     if (get<2>(lhs) < get<2>(rhs)) return true;     if (get<2>(lhs) > get<2>(rhs)) return false;     if (get<1>(lhs) < get<1>(rhs)) return true;     if (get<1>(lhs) > get<1>(rhs)) return false;     return get<0>(lhs) < get<0>(rhs);   }; }  std::ostream& operator<<(std::ostream& os, const Point3D& p) {   using boost::geometry::get;   os << "("  << get<0>(p) << "," << get<1>(p) << "," << get<2>(p) << ")";   return os; }  int main() {   std::vector<Point3D> v {     Point3D(0,0,0),     Point3D(0,0,1),     Point3D(0,1,0),     Point3D(0,1,1),     Point3D(1,0,0),     Point3D(1,0,1),     Point3D(1,1,0),     Point3D(1,1,1)   };   std::random_shuffle(v.begin(),v.end());   std::cout << "Random" << '\n';   for (const auto p:v) { std::cout << p << '\n'; }   std::sort(v.begin(),v.end(),OrderByX());    std::cout << "Sorted by X-Y-Z" << '\n';   for (const auto p:v) { std::cout << p << '\n'; }   std::sort(v.begin(),v.end(),OrderByZ());    std::cout << "Sorted by Z-Y-X" << '\n';   for (const auto p:v) { std::cout << p << '\n'; } }  /* Screen output  Random (1,0,0) (0,0,1) (1,1,0) (0,1,0) (0,0,0) (1,0,1) (1,1,1) (0,1,1) Sorted by X-Y-Z (0,0,0) (0,0,1) (0,1,0) (0,1,1) (1,0,0) (1,0,1) (1,1,0) (1,1,1) Sorted by Z-Y-X (0,0,0) (1,0,0) (0,1,0) (1,1,0) (0,0,1) (1,0,1) (0,1,1) (1,1,1) Press <RETURN> to close this window...  */`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)