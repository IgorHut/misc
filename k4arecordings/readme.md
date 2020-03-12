# Sample recordings from k4a demo.

Recordings are stored in two formats:
* binary with extension filename.rec.bin
* ascii with extension .rec

If you are processing these samples in Matlab and python, please use the ASCII (.rec) format, it's much easier to parse. 

## Understanding the ASCII export structure

ASCII (.rec) is a simple CSV file, where each line represents one frame of the body animation sequence.

Frame consists of the following columns, separated by ',' character, and terminated by end of line.
Description of columns follows:

* frame #0
  * frame time expressed in microseconds (since the start of the epoche)
  * sequence of 32 joints in a single row, where each joint is represented as:
    * joint 0 confidence (0 = none, 1 = shady, 2 = ok)
    * joint 0 position expressed as decimal triplet: x, y, z
    * joint 0 orientation as quaternion quadruplet: x, y, z, w
    * joint 1 confidence (0 = none, 1 = shady, 2 = ok)
    * joint 1 position expressed as decimal triplet: x, y, z
    * joint 1 orientation as quaternion quadruplet: x, y, z, w
    * ...
    * joint 31 confidence (0 = none, 1 = shady, 2 = ok)
    * joint 31 position expressed as decimal triplet: x, y, z
    * joint 31 orientation as quaternion quadruplet: x, y, z, w
  * end of line marks end of frame
* frame #1
  * ... and so on
  
  
  Example line from .rec file:
  
  ``` 
  1584033531968479,2,-0.0442058,-0.0805526,3.26596,-0.485175,0.533064,-0.466695,0.512488,2,-0.044808,-0.259931,3.25178,-0.476821,0.540549,-0.458663,0.519688,2,-0.0455458,-0.402665,3.23388,0.548472,-0.416246,0.577291,-0.438922,2,-0.0484513,-0.613359,3.29345,0.513326,-0.458889,0.540234,-0.483803,2,-0.0140821,-0.578517,3.28647,-0.755757,-0.107146,0.0972147,0.638671,2,0.124063,-0.537263,3.28501,-0.47569,-0.429118,0.487791,0.592989,2,0.167497,-0.262234,3.29751,-0.56445,-0.303019,0.615358,0.459251,2,0.181306,-0.0499926,3.20012,0.48405,0.582691,-0.496229,-0.424173,0,0.161438,0.0448161,3.19312,-0.369101,-0.661512,0.410116,0.507909,0,0.138378,0.143439,3.23336,-0.369101,-0.661512,0.410116,0.507909,0,0.128583,0.0764332,3.18238,-0.242211,-0.086688,0.726523,0.637168,2,-0.0818554,-0.577997,3.28279,0.639009,-0.160231,-0.0689002,0.749164,2,-0.206426,-0.537142,3.26262,0.643914,-0.54549,-0.324563,0.42717,2,-0.261577,-0.258893,3.24898,-0.490969,0.686392,0.210248,-0.49357,2,-0.25431,-0.0500636,3.13737,-0.116382,0.379559,-0.751343,0.527137,0,-0.218928,0.0451861,3.16209,-0.0484297,0.394036,-0.64794,0.650049,0,-0.20284,0.139514,3.21024,-0.0484297,0.394036,-0.64794,0.650049,0,-0.196933,0.0628467,3.14356,-0.30514,0.075095,0.880381,-0.355219,2,0.0476895,-0.0805768,3.26236,-0.492829,0.48865,-0.502866,0.515235,2,0.0409485,0.323131,3.26554,-0.442416,0.534719,-0.44972,0.562224,2,0.0318203,0.700845,3.34401,0.500445,-0.441754,0.553489,-0.498055,2,0.0487454,0.797091,3.18229,-0.0438845,0.661879,-0.0414037,0.747179,2,-0.127072,-0.0805307,3.2692,0.54582,0.564045,0.415115,0.460015,2,-0.119381,0.321864,3.24267,0.628983,0.469505,0.483244,0.38784,2,-0.0834756,0.698342,3.3377,0.526987,0.521785,0.450535,0.497035,2,-0.0931095,0.796675,3.19467,0.745522,-0.000840729,0.665531,0.035564,2,-0.048852,-0.695242,3.30256,-0.512292,0.580451,-0.281281,0.567022,2,-0.0873131,-0.695386,3.14512,-0.512292,0.580451,-0.281281,0.567022,2,-0.0472769,-0.731493,3.16187,0.0481954,0.772686,0.20205,0.599841,2,0.0379715,-0.734802,3.2571,0.580451,0.512292,0.567022,0.281281,2,-0.0986161,-0.739189,3.17113,0.0481954,0.772686,0.20205,0.599841,2,-0.119678,-0.774586,3.29669,-0.512292,0.580451,-0.281281,0.567022
  ```

## Joints map

Joints are dumped in the following order (per frame)"

```
        PELVIS = 0,
        SPINE_NAVEL,
        SPINE_CHEST,
        NECK,
        CLAVICLE_LEFT,
        SHOULDER_LEFT,
        ELBOW_LEFT,
        WRIST_LEFT,
        HAND_LEFT,
        HANDTIP_LEFT,
        THUMB_LEFT,
        CLAVICLE_RIGHT,
        SHOULDER_RIGHT,
        ELBOW_RIGHT,
        WRIST_RIGHT,
        HAND_RIGHT,
        HANDTIP_RIGHT,
        THUMB_RIGHT,
        HIP_LEFT,
        KNEE_LEFT,
        ANKLE_LEFT,
        FOOT_LEFT,
        HIP_RIGHT,
        KNEE_RIGHT,
        ANKLE_RIGHT,
        FOOT_RIGHT,
        HEAD,
        NOSE,
        EYE_LEFT,
        EAR_LEFT,
        EYE_RIGHT,
        EAR_RIGHT = 31    
```


## Joints-to-Bones mapping as per Microsoft Body SDK

```
    std::make_pair(K4ABT_JOINT_SPINE_CHEST, K4ABT_JOINT_SPINE_NAVEL),
    std::make_pair(K4ABT_JOINT_SPINE_NAVEL, K4ABT_JOINT_PELVIS),
    std::make_pair(K4ABT_JOINT_SPINE_CHEST, K4ABT_JOINT_NECK),
    std::make_pair(K4ABT_JOINT_NECK, K4ABT_JOINT_HEAD),
    std::make_pair(K4ABT_JOINT_HEAD, K4ABT_JOINT_NOSE),

    std::make_pair(K4ABT_JOINT_SPINE_CHEST, K4ABT_JOINT_CLAVICLE_LEFT),
    std::make_pair(K4ABT_JOINT_CLAVICLE_LEFT, K4ABT_JOINT_SHOULDER_LEFT),
    std::make_pair(K4ABT_JOINT_SHOULDER_LEFT, K4ABT_JOINT_ELBOW_LEFT),
    std::make_pair(K4ABT_JOINT_ELBOW_LEFT, K4ABT_JOINT_WRIST_LEFT),
    std::make_pair(K4ABT_JOINT_WRIST_LEFT, K4ABT_JOINT_HAND_LEFT),
    std::make_pair(K4ABT_JOINT_HAND_LEFT, K4ABT_JOINT_HANDTIP_LEFT),
    std::make_pair(K4ABT_JOINT_WRIST_LEFT, K4ABT_JOINT_THUMB_LEFT),
    std::make_pair(K4ABT_JOINT_PELVIS, K4ABT_JOINT_HIP_LEFT),
    std::make_pair(K4ABT_JOINT_HIP_LEFT, K4ABT_JOINT_KNEE_LEFT),
    std::make_pair(K4ABT_JOINT_KNEE_LEFT, K4ABT_JOINT_ANKLE_LEFT),
    std::make_pair(K4ABT_JOINT_ANKLE_LEFT, K4ABT_JOINT_FOOT_LEFT),
    std::make_pair(K4ABT_JOINT_NOSE, K4ABT_JOINT_EYE_LEFT),
    std::make_pair(K4ABT_JOINT_EYE_LEFT, K4ABT_JOINT_EAR_LEFT),

    std::make_pair(K4ABT_JOINT_SPINE_CHEST, K4ABT_JOINT_CLAVICLE_RIGHT),
    std::make_pair(K4ABT_JOINT_CLAVICLE_RIGHT, K4ABT_JOINT_SHOULDER_RIGHT),
    std::make_pair(K4ABT_JOINT_SHOULDER_RIGHT, K4ABT_JOINT_ELBOW_RIGHT),
    std::make_pair(K4ABT_JOINT_ELBOW_RIGHT, K4ABT_JOINT_WRIST_RIGHT),
    std::make_pair(K4ABT_JOINT_WRIST_RIGHT, K4ABT_JOINT_HAND_RIGHT),
    std::make_pair(K4ABT_JOINT_HAND_RIGHT, K4ABT_JOINT_HANDTIP_RIGHT),
    std::make_pair(K4ABT_JOINT_WRIST_RIGHT, K4ABT_JOINT_THUMB_RIGHT),
    std::make_pair(K4ABT_JOINT_PELVIS, K4ABT_JOINT_HIP_RIGHT),
    std::make_pair(K4ABT_JOINT_HIP_RIGHT, K4ABT_JOINT_KNEE_RIGHT),
    std::make_pair(K4ABT_JOINT_KNEE_RIGHT, K4ABT_JOINT_ANKLE_RIGHT),
    std::make_pair(K4ABT_JOINT_ANKLE_RIGHT, K4ABT_JOINT_FOOT_RIGHT),
    std::make_pair(K4ABT_JOINT_NOSE, K4ABT_JOINT_EYE_RIGHT),
    std::make_pair(K4ABT_JOINT_EYE_RIGHT, K4ABT_JOINT_EAR_RIGHT)
```

## Instructions for parsing .rec file

```
10 Open file for reading as text file
20 while not end of file
25   read line
30   parse frame time (in microseconds)
35   for i = 0, i < 32, i++
40     read x, y, z of the i joint (3d vector)
50     read x, y, z, w of the i joint (orientation quaternion)
60  

```
