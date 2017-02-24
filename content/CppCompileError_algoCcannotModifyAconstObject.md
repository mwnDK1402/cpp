



 

 

 

 

 

([C++](Cpp.md)) [\_algo.c: Cannot modify a const object](CppCompileError_algoCcannotModifyAconstObject.md)
============================================================================================================

 

[Compile error](CppCompileError.md).

 

 

 

 

 

Full error message
------------------

 

  -----------------------------------------------------------------
  ` [C++ Error] _algo.c(151): E2024 Cannot modify a const object`
  -----------------------------------------------------------------

 

The [compiler](CppCompiler.md) takes you to the following line in
\_algo.c:

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` // search_n.  Search for __count consecutive copies of __val.   template <class _ForwardIter, class _Integer, class _Tp> _ForwardIter search_n(_ForwardIter __first, _ForwardIter __last,                       _Integer __count, const _Tp& __val) {   _STLP_DEBUG_CHECK(__check_range(__first, __last))   if (__count <= 0)     return __first;   else {     __first = find(__first, __last, __val);     while (__first != __last) {       _Integer __n = __count - 1;       _ForwardIter __i = __first;       ++__i;       while (__i != __last && __n != 0 && *__i == __val) {         ++__i;         --__n; // <---THIS LINE       }       if (__n == 0)         return __first;       else         __first = find(__i, __last, __val);     }     return __last;   } }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Cause
-----

 

[IDE](CppIde.md): [C++ Builder](CppBuilder.md) 6.0

[Compiler](CppCompiler.md): Borland BCC32.EXE version 6.0.10.157

Project type: Console Application

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <string>  int main() {   const std::string s = "abc***def";   const int n = 3; //Number of repeats   std::search_n( s.begin(),s.end(),n,'*'); } `
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Solution/workaround
-------------------

 

Remove the [const](CppConst.md) of the [int](CppInt.md) for the number
of repeats, by [static\_cast](CppStatic_cast.md)ing it in the
[function](CppFunction.md) call.

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <string> #include <algorithm>  int main() {   const std::string s = "abc***def";   const int n = 3; //Number of repeats   std::search_n( s.begin(),s.end(),static_cast<int>(n),'*'); //n must be copied to int type }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Note that a [const\_cast](CppConst_cast.md) does not work. Personally,
I would find this more appropriate, but I do not understand why this
keeps giving the same error.

 

 

 

 

 

In-depth cause and better solution for advanced programmers
-----------------------------------------------------------

 

The actual problem is in \_algo.c. I have made all relevant information
**strong**:

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` // search_n.  Search for __count consecutive copies of __val.   template <class _ForwardIter, class _Integer, class _Tp> _ForwardIter search_n(_ForwardIter __first, _ForwardIter __last,                       _Integer __count, const _Tp& __val) {   _STLP_DEBUG_CHECK(__check_range(__first, __last))   if (__count <= 0)     return __first;   else {     __first = find(__first, __last, __val);     while (__first != __last) {       _Integer __n = __count - 1;       _ForwardIter __i = __first;       ++__i;       while (__i != __last && __n != 0 && *__i == __val) {         ++__i;         --__n;       }       if (__n == 0)         return __first;       else         __first = find(__i, __last, __val);     }     return __last;   } }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Because \_Integer is a [template](CppTemplate.md) type, the
[constness](CppConst.md) of the \_\_count argument is also taken into
account. The [local](CppLocal.md) \_Integer \_\_n, however, must not be
[const](CppConst.md).

 

A better solution would be to make \_\_n of non-[const](CppConst.md)
\_\_integer type, so the user can write
[const-correct](CppConstCorrect.md) code.

 

 

 

 

 





 


