
 

 

 

 

 

([C++](Cpp.md)) [std::partition](CppStdPartition.md)
===================================================

 

[std::partition](CppStdPartition.md) is an [STL](CppStl.md)
[algorithm](CppAlgorithm.md) to partition elements in a
[container](CppContainer.md) by a certain
[predicate](CppPredicate.md). For example, in the code shown below, a
[std::vector](CppStdVector.md) is partitioned into primes and non-primes.
Note that the order of the non-primes has changed. If the ordering must
remain, use [std::stable\_partition](CppStdStable_partition.md).

 

-   [Download the Qt Creator project
    'CppPartition' (zip)](CppPartition.zip)

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <cmath> #include <iostream> #include <iterator> #include <vector>  //From http://www.richelbilderbeek.nl/CppIsPrime.htm bool IsPrime(const int x) {   const int max   = static_cast<int>(       std::sqrt(static_cast<double>(x))     ) + 1;    for (int i=2; i!=max; ++i)   {     if (x % i == 0) return false;   }    return true; }  int main() {   std::vector<int> v;   for (int i=1; i!=10; ++i) v.push_back(i);    //Partition the std::vector in primes and non-primes   typedef std::vector<int>::iterator Iterator;   const Iterator p_end = std::partition(v.begin(),v.end(),IsPrime);    std::cout << "Primes: ";   std::copy(v.begin(),p_end,std::ostream_iterator<int>(std::cout," "));   std::cout << "\nNon-primes: ";   std::copy(p_end,v.end(),std::ostream_iterator<int>(std::cout," ")); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Screen output:

 

  -------------------------------------------
  ` Primes: 1 2 3 7 5  Non-primes: 6 4 8 9`
  -------------------------------------------

 

 

 

 

 

External links
--------------

 

-   [cplusplus.com page about
    std::partition](http://www.cplusplus.com/reference/algorithm/partition)

 

 

 

 

 

 

