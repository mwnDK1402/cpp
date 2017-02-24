



 

 

 

 

 

([C++](Cpp.md)) [OverrideExample1](CppOverrideExample1.md)
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

-   ![C++11](PicCpp11.png) [C++11](Cpp11.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppOverrideExample1/CppOverrideExample1.pro
--------------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= app_bundle CONFIG -= qt QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ -Werror SOURCES += main.cpp`
  -------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppOverrideExample1/main.cpp
------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  struct Base {   virtual ~Base() noexcept {}   virtual void a() const { std::cout << "Base::a\n"; }   virtual void b() const { std::cout << "Base::b\n"; }   virtual void c() const { std::cout << "Base::c\n";}   virtual void d() const { std::cout << "Base::d\n";}   virtual void e() const { std::cout << "Base::e\n";}   virtual void f() const { std::cout << "Base::f\n";}    void g() const { std::cout << "Base::g\n"; }   void h() const { std::cout << "Base::h\n"; }   void i() const { std::cout << "Base::i\n";}   void j() const { std::cout << "Base::j\n";}   void k() const { std::cout << "Base::k\n";}   void l() const { std::cout << "Base::l\n";} };  struct Derived : public Base {   virtual void a() const { std::cout << "Derived::a\n"; }   virtual void b() const override { std::cout << "Derived::b\n"; }   virtual void c() const override final { std::cout << "Derived::c\n"; }   void d() const { std::cout << "Derived::d\n"; }   void e() const override { std::cout << "Derived::e\n"; }   void f() const override final { std::cout << "Derived::f\n"; }    virtual void g() const { std::cout << "Derived::g\n"; }    //'virtual void Derived::h() const' marked override, but does not override   //virtual void h() const override { std::cout << "Derived::h\n"; }    //error: 'virtual void Derived::i() const' marked override, but does not override   //virtual void i() const override final { std::cout << "Derived::i\n"; }   void j() const { std::cout << "Derived::j\n"; }    //error: 'void Derived::k() const' marked override, but does not override   //void k() const override { std::cout << "Derived::k\n"; }    // error: 'void Derived::l() const' marked final, but is not virtual   // error: 'void Derived::l() const' marked override, but does not override   //void l() const override final { std::cout << "Derived::l\n"; }      virtual void m() const { std::cout << "Derived::m\n"; }   virtual void n() const noexcept { std::cout << "Derived::n\n"; }   virtual void o() const noexcept final{ std::cout << "Derived::o\n";}   // error: 'virtual void Derived::p() const' marked override, but does not override   //virtual void p() const override { std::cout << "Derived::p\n";}    // error: 'virtual void Derived::q() const' marked override, but does not override   //virtual void q() const noexcept override { std::cout << "Derived::q\n";}    // error: 'virtual void Derived::r() const' marked override, but does not override   //virtual void r() const noexcept override final { std::cout << "Derived::r\n";}   void s() const { std::cout << "Derived::s\n"; }   void t() const noexcept { std::cout << "Derived::t\n"; }    // error: 'void Derived::u() const' marked final, but is not virtual   //void u() const noexcept final { std::cout << "Derived::u\n";}    // error: 'void Derived::v() const' marked override, but does not override   //void v() const override { std::cout << "Derived::v\n";}    // error: 'void Derived::v() const' marked override, but does not override   //void w() const noexcept override { std::cout << "Derived::w\n";}    // error: 'void Derived::x() const' marked final, but is not virtual   // error: 'void Derived::x() const' marked override, but does not override   //void x() const noexcept final override { std::cout << "Derived::x\n";}  };   int main() {   const Derived d;   d.a();   d.b();   d.c();   d.d();   d.e();   d.f();   d.g();   d.h();   d.i();   d.j();   d.k();   d.l();   d.m();   d.n();   d.o();   d.s();   d.t();  }  /* Screen output  Derived::a Derived::b Derived::c Derived::d Derived::e Derived::f Derived::g Base::h Base::i Derived::j Base::k Base::l Derived::m Derived::n Derived::o Derived::s Derived::t  */`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)