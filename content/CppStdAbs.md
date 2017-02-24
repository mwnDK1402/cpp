



 

 

 

 

 

([C++](Cpp.md)) [std::abs](CppAbs.md)
=======================================

 

[std::abs](CppAbs.md) is an [STL](CppStl.md)
[function](CppFunction.md) to take the absolute value of a number (both
[int](CppInt.md) and [double](CppDouble.md)).

 

[std::abs](CppAbs.md) is defined in the [header
files](CppHeaderFile.md) [cmath.h](CppCmathH.md) (for
[doubles](CppDouble.md)) and [cstdlib.h](CppCstdlibH.md) (for
[integers](CppInt.md)).

 

 

 

 

 

[std::abs](CppAbs.md) on [double](CppDouble.md)
-------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <cmath>  int main() {   const double x = 3.14;   const double y = -x;   assert(x == std::abs(y)); }`
  ------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[std::abs](CppAbs.md) on [int](CppInt.md)
-------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <cstdlib>  int main() {   const int x = 3;   const int y = -x;   assert(x == std::abs(y)); }`
  -----------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Difference between [std::abs](CppAbs.md) and [std::fabs](CppFabs.md)
----------------------------------------------------------------------

 

[std::abs](CppAbs.md) can be used to calculate the absolute value of
both an [integer](CppInt.md) and a [double](CppDouble.md), where
[std::fabs](CppFabs.md) can only be used to obtain the absolute value
of a [double](CppDouble.md).

 

 

 

 

 





 


