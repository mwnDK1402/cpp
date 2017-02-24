



 

 

 

 

 

([C++](Cpp.md)) [GetMazeDistancesSlow](CppGetMazeDistancesSlow.md)
====================================================================

 

[GetMazeDistancesSlow](CppGetMazeDistancesSlow.md) is the perhaps more
straightforward, though slower [algorithm](CppAlgorithm.md) of
[GetMazeDistances](CppGetMazeDistances.md).

 

 

 

 

 

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

 

 

 

 

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <assert>  //From http://www.richelbilderbeek.nl/GetMazeDistances.htm std::vector<std::vector<int> > GetMazeDistancesSlow(   const std::vector<std::vector<int> >& maze,   const int x,   const int y) {   //Assume maze is square   assert(maze[0].size() == maze.size());   assert(maze[y][x] == 0); //Assume starting point is no wall    const int size = maze.size();   const int area = size * size;   const int maxDistance = area;   std::vector<std::vector<int> > distances(size, std::vector<int>(size,maxDistance));   std::vector<std::vector<int> > distances(size, std::vector<int>(size,maxDistance));   {     //Calculate the distances     int distance = 0;     distances[y][x] = 0; //Set final point     bool newDistanceFound = true;      while(newDistanceFound == true)     {       ++distance;       newDistanceFound = false;       for (int y=0; y!=size; ++y)       {         for (int x=0; x!=size; ++x)         {           //Check if this spot can be assigned a distance value           if (maze[y][x] != 0) continue; //Continue if here is a wall           if (distances[y][x] != maxDistance) continue; //Continue if already in solution           if (distances[y][x] != maxDistance) continue; //Continue if already in solution           if ( x!=0      && distances[y][x-1] == distance - 1 )           { distances[y][x] = distance; newDistanceFound = true; continue; }           if ( x!=size-1 && distances[y][x+1] == distance - 1 )           { distances[y][x] = distance; newDistanceFound = true; continue; }           if ( y!=0      && distances[y-1][x] == distance - 1 )           { distances[y][x] = distance; newDistanceFound = true; continue; }           if ( y!=size-1 && distances[y+1][x] == distance - 1 )           { distances[y][x] = distance; newDistanceFound = true; continue; }         }       }      }   }   return distances; }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 


