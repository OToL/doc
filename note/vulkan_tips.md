# Init sequence

    1. Create Vulkan Instance
    2. Create Destination surface from the window manager (e.g. glfw)
    3. Enumerate phyical devices and find the most appropriate one based on ...
        - Surface compatibility
        - Extensions
        - etc.
    4. Create Vulkan logical device from the selected physical device
    5. Create the swap chain and extract the list of VkImage

# Vertex transform

    World Coordinate (x,y,z) -> Clip Coordinate (x,y,z,w) -> Normalized device coordinates (x/w,y/w,z/w,1)

# Normalized Device Coordinates

(-1,-1) -------------------- (1,-1)
|                                 |
|                                 |
|                                 |
|              (0,0)              |
|                                 |
|                                 |
|                                 |
(-1,1) ---------------------- (1,1)

# Depth

Between [0,1] where 1 lies on the far clip plane

# UV

(0,0) ----------------------- (1,0)
|                                 |
|                                 |
|                                 |
|                                 |
|                                 |
|                                 |
|                                 |
(0,1) ----------------------- (1,1)
