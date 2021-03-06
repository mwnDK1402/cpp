# ([C++](Cpp.md)) [NDS graphic modes](CppNdsGraphicModes.md)

The [NDS](CppNds.md) has seven [NDS graphic
modes](CppNdsGraphicModes.md) \[1\]:

 * 0: all backgrounds in text mode
 * 1: background 3 in rotation mode
 * 2: background 2 and 3 in rotation mode
 * 3: background 3 in extended rotation mode
 * 4: background 2 in rotation mode, background 3 in extended rotation mode
 * 5: background 2 and 3 in extended rotation mode
 * 6: background 1 in large bitmap background mode

Note that background 0 is always in text mode.

## [References](CppReferences.md)

1.  [libnds documentation, under the enum
    VideoMode](http://libnds.devkitpro.org)

```
Main 2D engine
______________________________
|Mode | BG0 | BG1 | BG2 |BG3 |   T = Text
|  0  |  T  |  T  |  T  |  T |   R = Rotation
|  1  |  T  |  T  |  T  |  R |   E = Extended Rotation
|  2  |  T  |  T  |  R  |  R |   L = Large Bitmap background
|  3  |  T  |  T  |  T  |  E |
|  4  |  T  |  T  |  R  |  E |
|  5  |  T  |  T  |  E  |  E |
|  6  |     |  L  |     |    |
-----------------------------

Sub 2D engine
______________________________
|Mode | BG0 | BG1 | BG2 |BG3 |
|  0  |  T  |  T  |  T  |  T |
|  1  |  T  |  T  |  T  |  R |
|  2  |  T  |  T  |  R  |  R |
|  3  |  T  |  T  |  T  |  E |
|  4  |  T  |  T  |  R  |  E |
|  5  |  T  |  T  |  E  |  E |
-----------------------------
``` 

