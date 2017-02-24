



 

 

 

 

 

([C++](Cpp.md)) [CreateSloppyMaze](CppCreateSloppyMaze.md)
============================================================

 

[CreateSloppyMaze](CppCreateSloppyMaze.md) is a [maze](CppMaze.md)
[code snippet](CppCodeSnippets.md) that creates a maze that is as
'sloppy' as requested: a 'perfect' maze has no circular paths in it. The
sloppier the maze the more circular paths will be in. The problem with a
perfect maze, is that it takes much time to add to last extra walls to
make it perfect. For a perfect maze, use the algorithm
[CreateMaze](CppCreateMaze.md).

 

 

 

 

 

Project and source code
-----------------------

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.md): [Qt Creator](CppQt.md) 2.0.0

[Project type](CppQtProjectType.md): Qt4 [GUI](CppGui.md) Application

[Compiler](CppCompiler.md): [G++](CppGpp.md) 4.4.1

[Libraries](CppLibrary.md) used:

-   [Qt](CppQt.md): version 4.7.0 (32 bit)
-   [STL](CppStl.md): from [GCC](CppGcc.md), shipped with [Qt
    Creator](CppQt.md) 2.0.0

 

 

 

 

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <cassert>  //From http://www.richelbilderbeek.nl/CppCreateSloppyMaze.htm std::vector<std::vector<int> > CreateSloppyMaze(const int size, const double fractionPerfect) std::vector<std::vector<int> > CreateSloppyMaze(const int size, const double fractionPerfect) {   //Size must be odd   assert( size % 2 == 1);   assert( fractionPerfect >= 0.0 && fractionPerfect <= 1.0);    std::vector<std::vector<int> > maze(size, std::vector<int>(size,0));    //Draw outer walls   for (int i=0; i!=size; ++i)   {     maze[0]     [i     ] = 1;     maze[size-1][i     ] = 1;     maze[i]     [0     ] = 1;     maze[i]     [size-1] = 1;   }    //Draw pillars   for (int y=2; y!=size-1; y+=2)   {     for (int x=2; x!=size-1; x+=2)     {       maze[y][x] = 1;     }   }    //Check around pillars   const int nWallsToAdd     = static_cast<int>(fractionPerfect       * static_cast<double>(((size / 2) - 1) * ((size / 2) - 1)));   assert(nWallsToAdd <=(((size / 2) - 1) * ((size / 2) - 1)));    for (int i=0; i < nWallsToAdd; ) //'<' as there might be 2 walls added   {      for (int y=2; y!=size-1; y+=2)     {       for (int x=2; x!=size-1; x+=2)       {         const int nWalls           = (maze[y-1][x] == 0 ? 0 : 1)           + (maze[y+1][x] == 0 ? 0 : 1)           + (maze[y][x+1] == 0 ? 0 : 1)           + (maze[y][x-1] == 0 ? 0 : 1);         if ( nWalls == 0)         {           switch(std::rand() % 4)           {             case 0: maze[y-1][x] = 1; break;             case 1: maze[y+1][x] = 1; break;             case 2: maze[y][x+1] = 1; break;             case 3: maze[y][x-1] = 1; break;           }           ++i;         }         else if (nWalls == 1)         {           switch(std::rand() % 6)           {             case 0: std::swap(maze[y-1][x], maze[y+1][x]); break;             case 1: std::swap(maze[y-1][x], maze[y][x+1]); break;             case 2: std::swap(maze[y-1][x], maze[y][x-1]); break;             case 3: std::swap(maze[y+1][x], maze[y][x+1]); break;             case 4: std::swap(maze[y+1][x], maze[y][x-1]); break;             case 5: std::swap(maze[y][x+1], maze[y][x-1]); break;           }         }       }     }   }   return maze; } `
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 


