
 

 

 

 

 

([C++](Cpp.md)) [GetHtmlFilesInFolder](CppGetHtmlFilesInFolder.md)
====================================================================

 

[GetHtmlFilesInFolder](CppGetHtmlFilesInFolder.md) is a [file
I/O](CppFileIo.md) [code snippet](CppCodeSnippets.md) to obtain all
HTML filenames in a folder.

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <string> #include <vector> #include <boost/foreach.hpp> #include <boost/regex.hpp>  ///GetHtmlFilesInFolder returns the filenames of *.htm and *.html ///in folder given. ///From http://www.richelbilderbeek.nl/CppGetHtmlFilesInFolder.htm const std::vector<std::string> GetHtmlFilesInFolder(const std::string& folder) {   //Get all filenames   const std::vector<std::string> v = GetFilesInFolder(folder);    //Create the regex for a correct HTML filename   const boost::regex html_file_regex(".*\\.(html|htm)\\z");    //Create the resulting std::vector   std::vector<std::string> w;    //Copy all filenames matching the regex in the resulting std::vector   BOOST_FOREACH(const std::string& s, v)   {     if (boost::regex_match(s,html_file_regex)) w.push_back(s);   }   return w; } `
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

