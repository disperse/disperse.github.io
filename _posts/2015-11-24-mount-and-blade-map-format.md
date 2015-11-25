---
layout: post
title: Mount and Blade Map Format
---

I spent a couple evenings writing a random world map generator for Mount and Blade Warband and wanted to pass on what I have learned about the map format here in case it is of use to any other modders.

The world map is a [face-vertex mesh](https://en.wikipedia.org/wiki/Polygon_mesh#Face-vertex_meshes) stored in a text file, named map.txt, contained in the Module directory. For instance, for the Native module and a standard Steam installation of Mount and Blade Warband, the map.txt is located here:
> C:\Program Files (x86)\Steam\steamapps\common\MountBlade Warband\Modules\Native 

The first line of the file is the number of vertices followed by the x y z coordinates of each vertex. The order of the vertices is important.
``` 
20791
-177.735748 131.522049 -0.000002
-177.735748 128.631454 -0.000002
-177.735748 125.740868 -0.000002
-177.735748 122.850273 -0.000002
```

At the end of the vertex list (starting on line 20793) is the faces list starting with the total number of faces.
```
-36.298168 20.956806 1.360186
-37.549831 20.234156 1.376480
-35.046516 21.679449 1.280673
41387
0 0 3 1 45 0
0 0 3 2 46 1
0 0 3 3 47 2
0 0 3 4 48 3
```

Each face consists of six numbers, the first number ( **0** 0 3 4 48 3 ) is the terrain used to paint the face, defined by the following table:

| index | terrain         |
| ----- |:---------------:|
| 0     | water           | 
| 1     | mountain        |
| 2     | steppe          |
| 3     | plain           |
| 4     | snow            |
| 5     | desert          |
| 6     | bridge          |
| 7     | ???             |
| 8     | river           |
| 9     | mountain forest |
| 10    | steppe forest   |
| 11    | forest          |
| 12    | snow forest     |
| 13    | desert forest   |
| 14    | ???             |
| 15    | deep water      |

The next two numbers ( 0 **0 3** 4 48 3 ) are 0 and 3 for all vertices, (if anyone knows what they represent, let me know.)

The last three numbers ( 0 0 3 **4 48 3** ) are the indices of the vertexes that define the location of the three points of the face. So for this example you would look at lines 5, 49, and 4 (the first line is the # of vertices) to locate the vertices associated with the face.

That's it! It is a fairly simple format. In future posts I'll take a look at the format of the parties.txt file used to position towns and other entities on the world map.
