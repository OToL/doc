# DESIGN

- Coherent API: naming, parameters, etc.
- Extension based API: similar to DLL i.e. you have to get function address by name (vkGetInstanceProcAddr) before using it
- Lightweight API: no check on state nor input parameters
- Layers: plugin-like components adding extra verification(s)/debug features
- C-like interface: functions + POD structures
- All objects are returned using handles
- Structures
    - Type is always stored as first member (sType) allowing cheap RTTI
    - Extensible via a chain of opaque pointers (void * pNext)

# MAIN CONCEPTS & OBJECTS

- Vulkan Instance (VkInstance)
    - Vulkan API instance
    - Only one instance created at startup
    - Holds some application metadata (name, version, etc.)
    - Validation layers (parameters check, etc.) and extensions (KHR surface, etc.) can be enumerated and enabled
- Presentation surface (VkSurfaceKHR)
    - Swap chain output
    - Could be the Window's surface provided by the Window System (glfw, sdl, etc.)
    - It is an extension because it highly depends on the target Operating System. By default, Vulkan can only render to in-memory images
- Physical device(s) (VkPhysicalDevice)
    - 1:1 correspondance with graphics HW
    - Extensions (e.g. Swap Chain support) can be enumerated and enabled
    - Swap chain support should be tested against the target "Presentation surface"
    - Each physical device has a different set of queues serving one or more purposes (graphics, presentation, compute, DMA copy, etc.). Queues are the pipe of communication between the application and the Graphics card
    - Target physical device shall be selected based on its properties and capabilities (queues, extensions, etc.)
- Logical device (VkDevice)
    - Created from a physical device
    - Multiple logical devices can be created from 1 physical device
    - Queues (graphics, presentation, etc.) are created with the Logical device
    - Supports validation layers and extensions (e.g. physical device extensions)
- Queue (VkQueue)
    - Communication pipe between the application and the graphics card
    - A queue can serve one or more purposes (graphics, presentation, compute, DMA copy, etc.)
- Swap Chain (VkSurfaceFormatKHR)
    - Similarly to the "Presentation surface", swap chain is an extension
    - Owns one or more images used for buffering
    - How images are handled/presented (letter box, etc.) depends on available HW capabilities
    - Images' format & size depend to the target "Presentation surface"
    - Requires to know what queue(s) will access (read/write) its images e.g. presentation ("copy to presentation surface") and grpahics (rendering) queues
- Image (VkImage)
    - Raw image data i.e. block of pixels with a certain format (VkFormat), Color space & array count (normal vs stereoscopic rendering)
- Image view (VkImageView)
    - Defines how the Image data (VkImage) should be interpreted/accessed e.g. 2D vs 3D, Mip levels, etc.
    - Used to frame buffers
- Render Pass (VkRenderPass)
    - Defines the list of attachments (frame buffers, etc.) used by the different sub passes, load/store operations and layout transformation
    - Defines the list of sub passes and their inter dependencies
- Frame buffer (VkFramebuffer)
    - Encapsulate/reference one or more image view(s)
    - "I m under the impression the image views referenced by the frame buffers will be the render pass attachments"
    - Associated to a unique render pass
- Graphics Pipeline (VkPipeline)
    - Defines the state of every single graphics pipeline stage (programmable or not)
    - Owns shader modules binary data
    - Fully static except for push constants (VkPipelineLayout)
    - Uniquely associated to a render subpass i.e. requires a render pass object and sub pass index
- Command pool (VkCommandPool)
    - Pool of memory from which command buffers are created
    - Uniquely associated to one queue (VkQueue) i.e. it can create command buffers for only one queue
- Command buffers (VkCommandBuffer)
    - Used to record a list of commands (VkCmd*)
    - They can be used once or multiple times
- Semaphore
    - GPU/GPU sync
- Fence
    - Created signaled by default
    - CPU/GPU sync

# QUESTIONS

- Are the framebuffer's attachment the same thing as associated render pass' attachments?

# VERTEX TRANSFORMATION

    World Coordinate (x,y,z) -> Clip Coordinate (x,y,z,w) -> Normalized device coordinates (x/w,y/w,z/w,1)

# NORMALIZED COORDINATE SYSTEM

(-1,-1) -------------------- (1,-1)
|                                 |
|                                 |
|                                 |
|              (0,0)              |
|                                 |
|                                 |
|                                 |
(-1,1) ---------------------- (1,1)

# DEPTH

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
