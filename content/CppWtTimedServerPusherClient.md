



 

 

 

 

 

([C++](Cpp.md)) [WtTimedServerPusherClient](CppWtTimedServerPusherClient.md)
==============================================================================

 

 

 

 

 

 

Technical facts
---------------

 

[Application type(s)](CppApplication.md)

-   ![Web](PicWeb.png) [Web application](CppWebApplication.md)

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 11.04 (natty)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 2.0.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.5.2

[Libraries](CppLibrary.md) used:

-   ![Boost](PicBoost.png) [Boost](CppBoost.md): version 1.42
-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.5.2
-   ![Wt](PicWt.png) [Wt](CppWt.md): version 3.1.9

 

 

 

 

 

wttimedserverpusherclient.cpp
-----------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* WtTimedServerPusherClient, client of WtTimedServerPusher Copyright (C) 2011 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program. If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppWtTimedServerPusherClient.htm //--------------------------------------------------------------------------- #include <boost/bind.hpp> //--------------------------------------------------------------------------- #include <Wt/WApplication> //--------------------------------------------------------------------------- #include "wttimedserverpusher.h" #include "wttimedserverpusherclient.h" //--------------------------------------------------------------------------- WtTimedServerPusherClient::WtTimedServerPusherClient() {   Wt::WApplication::instance()->enableUpdates(true);   WtTimedServerPusher::GetInstance()->Connect(     this,boost::bind(&WtTimedServerPusherClient::OnServer,this));    //Never call virtual functions during construction or destroyion   //Scott Meyers, Effective C++, item 9   //OnServer(); } //--------------------------------------------------------------------------- WtTimedServerPusherClient::~WtTimedServerPusherClient() {   Wt::WApplication::instance()->enableUpdates(false);   WtTimedServerPusher::GetInstance()->Disconnect(this); } //--------------------------------------------------------------------------- const std::string WtTimedServerPusherClient::GetVersion() {   return "1.0"; } //--------------------------------------------------------------------------- const std::vector<std::string> WtTimedServerPusherClient::GetVersionHistory() {   std::vector<std::string> v;   v.push_back("2011-08-05: version 1.0: initial version");   return v; } //--------------------------------------------------------------------------- void WtTimedServerPusherClient::OnServer() {   OnTimedServerPush();   Wt::WApplication::instance()->triggerUpdate(); } //--------------------------------------------------------------------------- `
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

wttimedserverpusherclient.h
---------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- #ifndef WTTIMEDSERVERPUSHERCLIENT_H #define WTTIMEDSERVERPUSHERCLIENT_H //--------------------------------------------------------------------------- #include <string> #include <vector> //--------------------------------------------------------------------------- ///WtTimedServerPusherClient is a client responding to WtTimedServerPusher ///and to be used as a base class struct WtTimedServerPusherClient {   virtual ~WtTimedServerPusherClient();    ///Get the version of this class   static const std::string GetVersion();    ///Get the version history of this class   static const std::vector<std::string> GetVersionHistory();    ///UpdatePage is called when the WtTimedServerPusher triggers an update by timer   virtual void OnTimedServerPush() = 0;    protected:   ///WtTimedServerPusherClient constructor is protected   ///because it is to be used as a base class   WtTimedServerPusherClient();    private:   ///Respond to the server   void OnServer(); }; //--------------------------------------------------------------------------- #endif // WTTIMEDSERVERPUSHERCLIENT_H `
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 


