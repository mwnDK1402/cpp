



 

 

 

 

 

([C++](Cpp.md)) [std::is\_heap](CppIs_heap.md)
================================================

 

[std::is\_heap](CppIs_heap.md) is an [STL](CppStl.md)
[algorithm](CppAlgorithm.md) to check **[if](CppIf.md)** a
[container](CppContainer.md) is ordered like a heap.

 

-   [Download the Qt Creator project
    'CppIs\_heap' (zip)](CppIs_heap.zip)

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <vector> int main() {   //Create a std::vector   std::vector<int> v = {0,1,2,3,4,5,6,7,8,9};   //Assume std::vector is not a heap yet   assert(!std::is_heap(v.begin(),v.end()));   //make the std::vector a heap   std::make_heap(v.begin(),v.end());   //Assume std::vector is a heap now   assert(std::is_heap(v.begin(),v.end()));   //Assume the std::vector elements are ordered like a heap   assert(v == std::vector<int>( {9,8,6,7,4,5,2,0,3,1} ) ); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 




This page has been created by the [tool](Tools.md)
[CodeToHtml](ToolCodeToHtml.md)