



 

 

 

 

 

([C++](Cpp.md)) [std::fstream](CppFstream.md)
===============================================

 

[std::fstream](CppFstream.md) is an [STL](CppStl.md)
[stream](CppStream.md) for [file I/O](CppFileIo.md).

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <fstream>  int main() {   {     //Create a new file (or remove its contents)     std::ofstream f;     f.open("my_file.txt");     f << "Hello";   }   {     //Append to file     std::ofstream f;     f.open("my_file.txt",std::ios::app);     f << " world\n";   } }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 


