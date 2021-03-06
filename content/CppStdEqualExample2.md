
 

 

 

 

 

([C++](Cpp.md)) [StdEqualExample2](CppStdEqualExample2.md)
============================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStdEqualExample2/CppStdEqualExample2.pro
--------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStdEqualExample2/main.cpp
------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <set> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/shared_ptr.hpp> #pragma GCC diagnostic pop  const std::vector<boost::shared_ptr<int>> Create(const int n) {   assert(n >= 0);   std::vector<boost::shared_ptr<int>> v;   for (int i=0; i!=n; ++i)   {     const boost::shared_ptr<int> p(new int(i));     v.push_back(p);   }   return v; }  int main() {   //Compare two identical std::vectors: prefer operator!=   {     const std::vector<boost::shared_ptr<int>> v { Create(2) };     const std::vector<boost::shared_ptr<int>> w { Create(2) };      //Mismatch: compares the memory addresses of the integers     assert(v != w);     //Less preferred, no unexpected behaviour     assert(!std::equal(v.begin(),v.end(),w.begin()));   }   //Compare two identical std::vectors: prefer operator!=   {     const std::vector<boost::shared_ptr<int>> v { Create(2) };     std::vector<boost::shared_ptr<int>> w(v);      //Match: compares the memory addresses of the integers     assert(v == w);     //Less preferred, no unexpected behaviour     assert(std::equal(v.begin(),v.end(),w.begin()));      std::swap(*w.begin(),*(w.end()-1));      assert(v != w);     //Less preferred, no unexpected behaviour     assert(!std::equal(v.begin(),v.end(),w.begin()));   }   //Compare two different containers   {     const std::vector<boost::shared_ptr<int>> v { Create(2) };     std::set<boost::shared_ptr<int>> w(v.begin(),v.end());      //Less preferred, no unexpected behaviour     assert( (     std::equal(v.begin(),v.end(),w.begin())               || !std::equal(v.begin(),v.end(),w.begin()) )       && "Unknown if the shared_ptrs are allocated in memory at incremental adresses"     );   } }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

