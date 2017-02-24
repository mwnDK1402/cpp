



 

 

 

 

 

([C++](Cpp.md)) ![Boost](PicBoost.png) [boost::shared\_ptr](CppBoostShared_ptr.md))
=====================================================================================

 

 

[boost::shared\_ptr](CppBoostShared_ptr.md) is a type of
[shared\_ptr](CppShared_ptr.md) (which is a type of [smart
pointer](CppSmartPointer.md)) that can be copied safely and cheap,
without copying the object [pointed](CppPointer.md) to. When the last
[boost::shared\_ptr](CppBoostShared_ptr.md) using an object goes out of
[scope](CppScope.md), it will **[delete](CppDelete.md)** the object
[pointed](CppPointer.md)to.

 

 

 

 

 

Creating a [boost::shared\_ptr](CppBoostShared_ptr.md)
-------------------------------------------------------

 

  ---------------------------------------------------------------------------------------
  ` #include <boost/boost::shared_ptr.hpp>  int main() {   boost::shared_ptr<int> p; }`
  ---------------------------------------------------------------------------------------

 

 

 

 

 

[Smart pointers](CppSmartPointer.md) and [null](CppNull.md)
-------------------------------------------------------------

 

[Boost](CppBoost.md) [smart pointers](CppSmartPointer.md) check for
[null](CppNull.md) themselves, so there is no need to check these to be
inititialized. In the example below a [member
variable](CppMemberVariable.md) of a [class](CppClass.md) is requested
from an unitialized [smart pointer](CppSmartPointer.md). The program
will [abort](CppAbort.md) and the [runtime error](CppRuntimeError.md)
will be shown.

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <boost/boost::shared_ptr.hpp>  struct Test {   Test(const int x) : m_x(x) {}   const int m_x; };  int main() {   boost::shared_ptr<Test> p;   p->m_x; //Good: uninitialized pointer detected by Boost }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

The code below shows that initializing a
[boost::shared\_ptr](CppBoostShared_ptr.md) with [null](CppNull.md)
will not be easy, but even when it succeeds,
[boost::shared\_ptr](CppBoostShared_ptr.md) will check itself for
[null](CppNull.md).

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <boost/boost::shared_ptr.hpp>  struct Test {   Test(const int x) : m_x(x) {}   const int m_x; };  Test * CreateNullPointer() { return 0; }  int main() {   boost::shared_ptr<Test> p;   //p.reset(0); //Good: does not compile: 0 is an integer   //p.reset(NULL); //Good: does not compile   p.reset(CreateNullPointer()); //Bad: tricked the compiler   //p->m_x; //Good: uninitialized pointer detected by Boost }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

![Boost](PicBoost.png) [Smart pointers](CppSmartPointer.md) and [==](CppOperatorEqual.md)
-------------------------------------------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <boost/boost::shared_ptr.hpp>  ///A test class struct Test { int m_x; };  ///Class to manage a Test struct TestManager {   ///Construct an initialized Test   TestManager() : m_test(new Test) { m_test->m_x = 1; }    ///Obtain a read-only boost::shared_ptr to the Test managed   const boost::shared_ptr<const Test> GetTest() const { return m_test; }    ///Obtain a read-and-write boost::shared_ptr to the Test managed   const boost::shared_ptr<Test> GetTest()  { return m_test; }    private:   ///The Test managed   boost::shared_ptr<Test> m_test; };  int main() {   TestManager m;   assert(m.GetTest()->m_x == 1); //Read from m   m.GetTest()->m_x = 2; //Write to m   assert(m.GetTest()->m_x == 2); //Read from m   const boost::shared_ptr<const Test> v(m.GetTest());    assert(m.GetTest() == v); //boost::shared_ptr's to same object are evaluated to true by operator==   //v->m_x = 3; //Does not compile: v holds a read-only pointer   const boost::shared_ptr<Test> w(boost::const_pointer_cast<Test>(v));   assert(m.GetTest() == w);  //boost::shared_ptr's to same object are evaluated to true by operator==   assert(v == w);  //boost::shared_ptr's to same object are evaluated to true by operator==   w->m_x = 3; //Does compile   assert(v->m_x == 3);   assert(w->m_x == 3);   assert(m.GetTest()->m_x == 3); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

![Boost](PicBoost.png) [Cast](CppCast.md) from [boost::shared\_ptr](CppBoostShared_ptr.md)&lt;[const](CppConst.md) Test&gt; to [boost::shared\_ptr](CppBoostShared_ptr.md)&lt;Test&gt;
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <boost/boost::shared_ptr.hpp>  ///A test class struct Test { int m_x; };  ///Class to manage a Test struct TestManager {   ///Construct an initialized Test   TestManager() : m_test(new Test) { m_test->m_x = 1; }    ///Obtain a read-only boost::shared_ptr to the Test managed   const boost::shared_ptr<const Test> GetTest() const { return m_test; }    ///Obtain a read-and-write boost::shared_ptr to the Test managed   const boost::shared_ptr<Test> GetTest()  { return m_test; }    private:   ///The Test managed   boost::shared_ptr<Test> m_test; };  int main() {   TestManager m;   assert(m.GetTest()->m_x == 1); //Read from m   m.GetTest()->m_x = 2; //Write to m   assert(m.GetTest()->m_x == 2); //Read from m   const boost::shared_ptr<const Test> v(m.GetTest());    assert(m.GetTest() == v); //boost::shared_ptr's to same object are evaluated to true by operator==   //v->m_x = 3; //Does not compile: v holds a read-only pointer   const boost::shared_ptr<Test> w(boost::const_pointer_cast<Test>(v));   assert(m.GetTest() == w);  //boost::shared_ptr's to same object are evaluated to true by operator==   assert(v == w);  //boost::shared_ptr's to same object are evaluated to true by operator==   w->m_x = 3; //Does compile   assert(v->m_x == 3);   assert(w->m_x == 3);   assert(m.GetTest()->m_x == 3); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

External links
--------------

 

-   [Boost's page about
    boost::shared\_ptr](http://www.boost.org/doc/libs/1_35_0/libs/smart_ptr/shared_ptr.md)

 

 

 

 

 





 


