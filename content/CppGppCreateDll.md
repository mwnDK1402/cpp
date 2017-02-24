



 

 

 

 

 

([C++](Cpp.md)) [Create a DLL using g++](CppGppCreateDll.md)
==============================================================

 

Before being able to [call a DLL](CppGppCallDll.md), one has to [create
a DLL using g++](CppGppCreateDll.md) first.

 

To create a [DLL](CppGppDll.md) using [g++](CppGpp.md), do the
following steps:

-   Create a [DLL](CppDll.md) entry point with a WinMain
-   Create a unit with the functions you want to put in a
    [DLL](CppDll.md)
-   Build the [DLL](CppDll.md)

 

 

 

 

 

UnitEntryPoint.cpp
------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- #include <windows.h> //--------------------------------------------------------------------------- int WINAPI DllEntryPoint(HINSTANCE hinst, unsigned long reason, void* lpReserved) {   return 1; } //--------------------------------------------------------------------------- int WINAPI WinMain(           HINSTANCE hInstance,     HINSTANCE hPrevInstance,     LPSTR lpCmdLine,     int nCmdShow) {     return 0; } //---------------------------------------------------------------------------`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

UnitFunctions.h
---------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- #ifndef UnitFunctionsH #define UnitFunctionsH //--------------------------------------------------------------------------- #ifdef __cplusplus extern "C" { #endif  __declspec (dllexport) const int GetAnswerOfLife();  #ifdef __cplusplus } #endif  //--------------------------------------------------------------------------- #endif`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

The function put in the DLL is called GetAnswerOfLife and will return
the value of 42. Note the [\#ifdef](CppIfdef.md)'s before and after the
function. These are obligatory!

 

Now the function GetAnswerOfLife must be defined in UnitFunctions.cpp.
Upon viewing it, the code looks like below

 

 

 

 

 

UnitFunctions.cpp
-----------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- #include "UnitFunctions.h" //--------------------------------------------------------------------------- const int GetAnswerOfLife() {   return 42; } //---------------------------------------------------------------------------`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Building the DLL
----------------

 

Use the following [g++](CppGpp.md) commands:

 

  -------------------------------------------------------------------------------------------------------------
  ` g++ -c UnitFunctions.cpp g++ -c UnitEntryPoint.cpp g++ -o Functions.dll UnitEntryPoint.o UnitFunctions.o`
  -------------------------------------------------------------------------------------------------------------

 

This should yield your first [DLL](CppDll.md).

 

Perhaps you now want to [go to the calling a DLL page using
g++](CppGppCallDll.md).

 

[Or download all source code of this page at once](CppGppCreateDll.zip).

 

 

 

 

 





 


