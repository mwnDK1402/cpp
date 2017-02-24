



 

 

 

 

 

([C++](Cpp.md)) [SafeIntToCli](CppSafeIntToCli.md)
====================================================

 

[SafeIntToCli](CppSafeIntToCli.md) is a [cln::cl\_I](CppCl_I.md)
[conversion](CppConvert.md) [code snippets](CppCodeSnippets.md) to
[convert](CppConvert.md) an [integer](CppInt.md) to a
[cln::cl\_I](CppCl_I.md) safely.

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <string> #include <boost/lexical_cast.hpp> //--------------------------------------------------------------------------- #include <cln/cln.h> //--------------------------------------------------------------------------- ///SafeIntToCli converts an int to cln::cl_I safely. ///From http://www.richelbilderbeek.nl/CppSafeIntToCli.htm const cln::cl_I SafeIntToCli(const int i) {   //A cln::cl_I can handle integer values to 2^29 in its constructor   if (i < 536870912)   {     return cln::cl_I(i);   }   const std::string s = boost::lexical_cast<std::string>(i);   return cln::cl_I(s.c_str()); } //--------------------------------------------------------------------------- #include <boost/numeric/conversion/bounds.hpp> //--------------------------------------------------------------------------- ///GetMaxInt returns the highest possible value of a int. ///From http://www.richelbilderbeek.nl/CppGetMaxInt.htm int GetMaxInt() {   return boost::numeric::bounds<int>::highest(); } //--------------------------------------------------------------------------- #include <iostream> //--------------------------------------------------------------------------- int main() {   const cln::cl_I i(GetMaxInt()); //Will not work properly   const cln::cl_I j = SafeIntToCli(GetMaxInt());   std::cout     << "i (wrong): " << i << '\n'     << "j: " << j << '\n'; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Screen output:

 

  --------------------------------
  ` i (wrong): -1 j: 2147483647`
  --------------------------------

 

 

 

 

 





 


