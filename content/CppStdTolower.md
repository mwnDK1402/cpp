
 

 

 

 

 

([C++](Cpp.md)) [std::tolower](CppTolower.md)
===============================================

 

[std::tolower](CppTolower.md) is a [function](CppFunction.md)
[defined](CppDefinition.md) in the [header file](CppHeaderFile.md)
[cctype.h](CppCctypeH.md) to [convert](CppConvert.md) a
[char](CppChar.md) to lower case.

 

 

 

 

 

Example: [StrToLower](CppStrToLower.md) using a [for](CppFor.md) loop
-----------------------------------------------------------------------

 

[StrToLower](CppStrToLower.md) can be implemented using a
[for](CppFor.md) loop, but prefer [algorithm](CppAlgorithm.md) calls
over hand-written loops \[1\]\[2\]. View [Exercise \#9: No
for-loops](CppExerciseNoForLoops.md) for other ways of replacing
for-loops by algorithms.

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cctype> #include <string>  //From http://www.richelbilderbeek.nl/CppStrToLower.htm const std::string StrToLower(std::string s) {   std::transform(s.begin(), s.end(), s.begin(),std::ptr_fun(std::tolower));   return s; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 

1.  [Bjarne Stroustrup](CppBjarneStroustrup.md). The C++ Programming
    Language (3rd edition). 1997. ISBN: 0-201-88954-4. Chapter 18.12.1:
    'Prefer algorithms to loops.
2.  [Scott Meyers](CppScottMeyers.md). Effective STL.
    ISBN: 0-201-74962-9. Item 43: 'Prefer algorithm calls over
    hand-written loops'.

 

 

 

 

 

 

