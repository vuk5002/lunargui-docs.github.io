# Graphics in Lunar

<span style="font-size:18px ; font-weight: bold;">As of 1.0.5 Lunar supports 3 graphics APIs (actually 5)</span>
- DepthCore
    -   DepthRT [Built on top of DepthCore, adds a ray tracing shader]
    -   Depth2D [Built on top of DepthCore, removes all 3D support]
- OpenGL 4.6
- Vulkan [WIP, only supports functions from 1.0, will get 100% support later on]

|    API Name    |    Best case use    |
|    :---:    |    :---:    |
|    DepthCore    |    Most basic 3D programs, you can make a game if you want    |
|    DepthRT    |    Really only meant for static ray tracing scenes, can be real time RT    |
|    Depth2D    |    Only for 2D shape drawing    |
|    OpenGL    |    Really any 3D / 2D game    |
|    Vulkan    |    High performance programs & RT-heavy games    |



