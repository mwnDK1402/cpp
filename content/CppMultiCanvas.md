



 

 

 

 

 

([C++](Cpp.md)) [MultiCanvas](CppMultiCanvas.md)
==================================================

 

Technical facts
---------------

 

 

 

 

 

 

./CppMultiCanvas/CppMultiCanvas.pri
-----------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppMultiCanvas  SOURCES += \     ../../Classes/CppMultiCanvas/multicanvas.cpp  HEADERS  += \     ../../Classes/CppMultiCanvas/multicanvas.h  OTHER_FILES += \     ../../Classes/CppMultiCanvas/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppMultiCanvas/multicanvas.h
------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef MULTICANVAS_H #define MULTICANVAS_H  #include <iosfwd> #include <string> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/signals2.hpp> #include "canvas.h" #include "canvascolorsystem.h" #include "canvascoordinatsystem.h" #pragma GCC diagnostic pop  struct QRegExp;  namespace ribi {  ///A MultiCanvas is an ASCII art class for displaying ///multiple layers of Canvas classes struct MultiCanvas : public Canvas {   MultiCanvas(     const std::vector<boost::shared_ptr<Canvas>>& canvases   ) noexcept;    ///Obtain the height of the canvas is characters   int GetHeight() const noexcept;    ///Obtain the version of this class   static std::string GetVersion() noexcept;    ///Obtain the version history of this class   static std::vector<std::string> GetVersionHistory() noexcept;    ///Obtain the width of the canvas is characters   int GetWidth() const noexcept;    ///Convert the MultiCanvas to std::strings   std::vector<std::string> ToStrings() const noexcept;    private:   const std::vector<boost::shared_ptr<Canvas>> m_canvases;    #ifndef NDEBUG   static void Test() noexcept;   #endif };  std::ostream& operator<<(std::ostream& os, const MultiCanvas& c) noexcept;  } //~namespace ribi  #endif`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppMultiCanvas/multicanvas.cpp
--------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include "multicanvas.h"  #include <iostream> #include <cassert> #include <cmath> #include <algorithm> #include <functional> #include <iterator>  #include <boost/math/constants/constants.hpp> #include <boost/algorithm/string/split.hpp>  #include <QString> #include <QRegExp>  #include "canvascolorsystems.h" #include "canvascoordinatsystems.h" #include "fileio.h" #include "trace.h"  #pragma GCC diagnostic pop  ribi::MultiCanvas::MultiCanvas(   const std::vector<boost::shared_ptr<Canvas>>& canvases ) noexcept : m_canvases(canvases) {  }  int ribi::MultiCanvas::GetHeight() const noexcept {   if (m_canvases.empty()) return 0;   int h = m_canvases[0]->GetHeight();   for (const auto& c: m_canvases) { h = std::min(h,c->GetHeight()); }   return h; }  std::string ribi::MultiCanvas::GetVersion() noexcept {   return "1.0"; }  std::vector<std::string> ribi::MultiCanvas::GetVersionHistory() noexcept {   return {     "2014-01-13: version 1.0: initial version"   }; }  int ribi::MultiCanvas::GetWidth() const noexcept {   if (m_canvases.empty()) return 0;   int w = m_canvases[0]->GetWidth();   for (const auto& c: m_canvases) { w = std::min(w,c->GetWidth()); }   return w; }  std::vector<std::string> ribi::MultiCanvas::ToStrings() const noexcept {   const int maxy = GetHeight();   const int maxx = GetWidth();   if (maxx == 0 || maxy == 0) { return std::vector<std::string>(); }   const int n_layers = static_cast<int>(m_canvases.size());   std::vector<std::vector<std::string>> v;   for (const auto& c: m_canvases) { v.push_back(c->ToStrings()); }   //Let the first canvas be drawn last, to give it the heighest Z order   std::reverse(std::begin(v),std::end(v));    std::vector<std::string> w;   for (int y=0; y!=maxy; ++y)   {     std::string to(maxx,' ');     for (int layer=0; layer!=n_layers; ++layer)     {       assert(layer < static_cast<int>(v.size()));       assert(y < static_cast<int>(v[layer].size()));       const std::string from { v[layer][y] };       for (int x=0; x!=maxx; ++x)       {         assert(x < static_cast<int>(from.size()));         const char c { from[x] };         if (c == ' ') continue;         assert(x < static_cast<int>(to.size()));         to[x] = c;       }     }     w.push_back(to);   }   return w; }  std::ostream& ribi::operator<<(std::ostream& os, const MultiCanvas& c) noexcept {   const auto text = c.ToStrings();   std::copy(text.begin(),text.end(),     std::ostream_iterator<std::string>(os,"\n")   );   return os; }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)