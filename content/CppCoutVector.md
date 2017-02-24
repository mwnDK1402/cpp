



 

 

 

 

 

([C++](Cpp.md)) [CoutVector](CppCoutVector.md)
================================================

 

[std::vector](CppVector.md) [code snippet](CppCodeSnippets.md) to
write every element in a [std::vector](CppVector.md) to
[std::cout](CppCout.md). There is also a more general solution for
every [container](CppContainer.md):
[CoutContainer](CppCoutContainer.md). To be also able to read the
[std::vector](CppVector.md), go to [write and read a std::vector
to/from a std::stream](CppVectorToStream.md).

 

Instead of using a [for](CppFor.md)-loop (See question 15 of [Exercise
\#9: No for-loops](CppExerciseNoForLoops.md)), the
[algorithm](CppAlgorithm.md) [std::copy](CppCopy.md) can be used to
copy the contents of a [std::vector](CppVector.md) to
[std::cout](CppCout.md) using the
[std::ostream\_iterator](CppOstream_iterator.md). Prefer algorithms
over loops \[1\]\[2\].

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <iterator> #include <iostream> #include <ostream>  //From http://www.richelbilderbeek.nl/CppCoutVector.htm template <class T> void CoutVector(const std::vector<T>& v) {   std::copy(v.begin(),v.end(),std::ostream_iterator<T>(std::cout,"\n")); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

CoutVector test
---------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <iterator> #include <iostream> #include <ostream>  //From http://www.richelbilderbeek.nl/CppCoutVector.htm template <class T> void CoutVector(const std::vector<T>& v) {   std::copy(v.begin(),v.end(),std::ostream_iterator<T>(std::cout,"\n")); }  int main() {   //Create a vector   std::vector<int> v;   v.push_back(1);   v.push_back(4);   v.push_back(9);   v.push_back(16);   v.push_back(25);    //Show it on screen using CoutVector   CoutVector(v); } `
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 

1.  [Bjarne Stroustrup](CppBjarneStroustrup.md). The C++ Programming
    Language (3rd edition). ISBN: 0-201-88954-4. Chapter 18.12.1 :
    'Prefer algorithms over loops'
2.  [Herb Sutter](CppHerbSutter.md) and [Andrei
    Alexandrescu](CppAndreiAlexandrescu.md). C++ coding standards: 101
    rules, guidelines, and best practices. ISBN: 0-32-111358-6. Chapter
    84: 'Prefer algorithm calls to handwritten loops.'

 

 

 

 

 





 


