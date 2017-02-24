



 

 

 

 

 

([C++](Cpp.md)) [Qt Creator macro](CppQtCreatorMacro.md)
==========================================================

 

[Qt Creator](CppQtCreator.md) has some [macro's](CppMacro.md) supplied
( although these are actually supplied by the [GCC](CppGcc.md)).

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  int main() {   std::cout     << "Date: "     << __DATE__     << '\n'     << "File: "     << __FILE__     << '\n'     << "Function: " << __FUNCTION__ << '\n'     << "Line: "     << __LINE__     << '\n'     << "Time: "     << __TIME__     << '\n'; }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Screen output:

 

  -----------------------------------------------------------------------------------------
  ` Date: Dec 14 2010 File: ../CppQtMacro/main.cpp Function: main Line: 9 Time: 13:09:53`
  -----------------------------------------------------------------------------------------

 

 

 

 

 





 


