



 

 

 

 

 

([C++](Cpp.md)) [WideToStr](CppWideToStr.md)
==============================================

 

Converts a WideString to a std::string.

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <string>  //From http://www.richelbilderbeek.nl/CppWideToStr.htm std::string WideToStr(const WideString& s) {   const AnsiString a(s);   return a.c_str(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)