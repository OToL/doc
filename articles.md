# AI
- https://github.com/mlabonne/llm-course
- https://www.linkedin.com/pulse/getting-started-llms-guide-resources-opportunities-wendy-ran-wei/
- https://jalammar.github.io/illustrated-transformer/
- https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/
- https://www.linkedin.com/pulse/transformers-nutshell-dave-burke-l5t0c/
- Friendly Introduction to Neural Network playlist: https://www.youtube.com/playlist?list=PLs8w1Cdi-zvavXlPXEAsWIh4Cgh83pZPO
    - A friendly introduction to Recurrent Neural Networks - https://www.youtube.com/watch?v=UNmqTiOnRfg
- Attention is all what you need:https://arxiv.org/pdf/1706.03762.pdf
    - https://www.youtube.com/watch?v=bCz4OMemCcA
- Intro to large language models: https://www.youtube.com/watch?v=zjkBMFhNj_g&t=4s
- AWS AI Master class:
    - AI Masterclass Part 1: Why AI matters for the public sector: https://www.youtube.com/watch?v=zkEfOv5_2wY
    - AI Masterclass Part 2: Getting started with AI for governments: https://www.youtube.com/watch?v=FG3fBQJ2o3c
    - AI Masterclass Part 3: How to build your first AI solution: https://www.youtube.com/watch?v=_9LJmYN_YX4
    - AI Masterclass Part 4: How to become an AI-driven organization: https://www.youtube.com/watch?v=WEW1qQHeys8

# MEMORY

- [] rpmalloc: https://stoyannk.wordpress.com/2018/01/10/generic-memory-allocator-for-c-part-3/

# MATH

- [ ] immersive linear algebra : http://immersivemath.com/ila/index.html
- [ ] Model View Projection : https://jsantell.com/model-view-projection

# LINUX GAMEDEV

- [x] Getting Started with Linux Game Development : https://www.youtube.com/watch?v=Sd8ie5R4CVE
    * Use SDL2
        * inputs
        * window management
        * atomics
        * performance counter
        * threads
    * Use OpenGL
    * Compilers: Clang, GCC & Intel C++
        * Clang faster to compile
        * GCC produce faster code
    * Parse Visual Studio solutions to generate makefiles, scons, etc.
    * MAKE THINGS COMPILE i.e. LINKAGE and RUNNING later
        * Stub all what you can and tag it to find it easily e.g.
            #define STUBED which is printf it is a stub once
        * Do not try to make things look better or refactoring
          If you start cleaning & refactoring it makes merge back more complicated
    * Shipping with Steam (Steam Runtime) ensure some dependenciees are there
    * FileSystem Pitfalls --> WILL BE VERY PAINFUL FOR COMPILING THE CODE i.e. include paths
        * Paths are /
        * No drive letter (e.g. e:/)
        * User permissions --> have an impact on game saves & config locations
          e.g. write to home or steam user directory
        * Paths are UTF-8
        * Case sensitive
    * IDE
        * QTCreator
        * Eclipse
        * Sublime Text
    * Debug
        * GDB 7 -> includes slow but operational reverse debugging
        * UndoDB -> includes reverse debugging but it is not free
        * QTCreator
        * Visual GDB: https://visualgdb.com/
        * Valgrind
        * LLVM Sanitizers
    * Optimization: 
        * perf
        * rad telemetry
        * ApiTrace
        * Zoom
- [x] Porting Games To Linux: https://www.youtube.com/watch?v=d8kfva6G0c4
    * Steam Runtime: bunch of ubuntu libraries Steam is distributing
    * Bundle dependencies
    * Nice DAG of his port workflow but similar to what I have already heard
    * Case sensitivity again
    * Use platform best practices
        * Get locales
        * Use XDG for application config files
    * Linters: CppCheck
- [ ] Game Development with SDL 2.0: https://www.youtube.com/watch?v=MeMPCSqQ-34
- [ ] Getting Started Debugging on Linux : https://www.youtube.com/watch?v=xTmAknUbpB0
- [ ] Building Unity Games for SteamOS/Linux: https://www.youtube.com/watch?v=WYdOQ_k6YvI
- [ ] Linux development with C++: https://www.youtube.com/watch?v=XIiFuBczd6A & https://www.youtube.com/watch?v=4NenIuAbtGs

# CMAKE

- [] An Introduction to Modern CMake : https://cliutils.gitlab.io/modern-cmake/
- [x] Effective CMake: https://www.youtube.com/watch?v=bsXLMQ6WgIk&t=4699s&pbjreload=10
    - Execute a CMake file as a script i.e. does not generate build files
        ```
        cmake -p <script>.cmake
        ```
    - Variables which are not set are expanded to empty string
    - multi line commmet
        ```
        # [==[
            code here
        # ]==]
        ```
    - Expressions evaluated during project generation as opposed to script execution i.e. later : $<>
    - When 2 commands have the same name, using '_' prefix is calling the older (i.e. shadowed) one
        ```
            function (xx)
            endfunction()

            function (xx)
                # calls the previous xx function
                _xx()
            endfunction()

            # calls the latest one
            xx()
        ```
    - Use macros when wrapping other commands (function or macro) which set variables you are not in control in the parent scope
    - Define a command to be called when a variable is accessed e.g. for deprecation
        ```
        variable_watch(var_name myfunction)
        ```
    - Modern CMake is about targets and properties
    - Don t use file(glob) it is evaluated during script execution i.e. cannot recognize file addition without regenerated projects.
    - Use target_* instead of global CMake variables
    - target_* commands have 2 scopes for their properties
        - PRIVATE (<property>): only applies to the target
        - INTERFACE (INTERFACE_<property>): applies to the targets which depends on it i.e. transitivity
       There is the special PUBLIC scope alias which adds to both (PRIVATE+INTERFACE)
    - Use <target>::<target> to reference another target because otherwise CMake may think it is a library and translate it to -l<target>
    - We can create pure library interface and in this case it will be only about transitive requirements
    - Modules can be found using include() in CMAKE_MODULE_PATH directoriesto
- [x] The Ultimate Guide to Modern CMake: https://rix0r.nl/blog/2015/08/13/cmake-guide/
- [ ] CMake - Introduction and best practices: https://www.slideshare.net/DanielPfeifer1/cmake-48475415

# COMPILER

- [] Linker essay: https://lwn.net/Articles/276782/

# ENGINE ARCHITECTURE

- [x] Writing Tools Faster: https://ourmachinery.com/writing-tools-faster.html
   - Tried different approach for Tools UI
      - WinForm: fast but ugly/hacky
      - WPF: nice looking but the entry barrier is high (c#, wpf, etc.) and windows specific
      - Web: a lot of expertise but the stack of components involved is deep (JS, REST, HTML, etc.) and impacts performance
   - Engine implementation is much faster that the Tools UI i.e. Tools is a bottleneck
   - Tools software stack is a common issue whatever you are using (e.g. WPF/C#Model/C++ManagedBridge/Engine) which is causing ...
      - Team friction       
      - Delay in delivering features or fixes to the users
      - Perf issues
      - The knowledge to be restricted to few people
   - Well-defined universal data representation (aka the Truth) with well defined operations (copy/paste, undo/redo, etc.)
   - The Truth format is basically json i.e. key/value
   - The Truth supports ...
      - Multi-threading: 2 steps ... get the copy of the data to modify and then commit the result
      - Operations (undo/redo, etc.)
      - Internal (owned) and external reference
      - Inheritance + value override (i.e. blueprint)
      - Live collaboration i.e. delta + send
   - Truth cons
      - key/value format does not work for everything e.g. graphics data (vertex buffer, etc.)
      - Looks like a big singleton
   - Use imgui
   - UI Rendering = 1 draw call
   - Actually, they have 1 vertex/primite buffer and multiple index buffers to handle overlays (e.g. pop-ups)
   - Immediate GUI cannot handle everything out of the box but it can be solved by retaining some state
- [x] Hot DLL reloading: http://ourmachinery.com/post/dll-hot-reloading-in-theory-and-practice/
    - Plugin code hot reload
    - Simple C like interface i.e.
        - API (ie functions) is just function pointers
        - Objects are opaque and always passed a API parameters
    - Ideally use reflection serializaton/deserialization to transfer object state between reload
    - When reloading DLL they re-use the same allocator i.e. object/memory can persist
    - DLL reload process
        1. Load new DLL
        2. Copy data between old and new
        3. Unload old DLL
   - Immediate UI is good for debugging and understanding performance issues
- [x] Unity at GDC: https://www.twitch.tv/videos/242024723?t=
    - Very interesting concrete examples of Entity Component System where data and transformation matters
    - Data is stored at a very small granularity (list of floats, vector, etc.)
    - Entity is not a container but just an ID indexing associated components data in the different data
    - The System starts by gathering the streaming of data based on the entities' component types and then transform the result
    - Explains how to handle dependency between entity (Parent --> children) by doing some pre-processing to identity the dependencies before doing the actual transformation
    - They have their own C# compiler handling a subset of the language : High Performance C# aka HPC#
    - Good aliasing examples
    - Transparent SAO native array very similar to Jonathan blow language
- [ ] Job System enkiTS: https://github.com/dougbinks/enkiTS
- [ ] Parallelizing the Naughty Dog engine using fibers: http://twvideo01.ubm-us.net/o1/vault/gdc2015/presentations/Gyrling_Christian_Parallelizing_The_Naughty.pdf
- [ ] How to Open a Black Box: https://www.youtube.com/watch?v=SYomOZIfeoU
- [ ] Compilation time: http://ourmachinery.com/post/physical-design/
- [ ] Our Machinery - Fiber based job system: https://ourmachinery.com/post/fiber-based-job-system/
- [ ] Stingray engine walkthrough: https://www.youtube.com/watch?v=LgbSYxf9vT4&list=PLUxuJBZBzEdxzVpoBQY9agA8JUgNkeYSV
    - Part 1: Overview
        - Good/simple pillars
        - Interesting packaging system to download all dependencies using S3
        - Remote file system for consoles which is also taking care of data compilation
        - Plugin system with C like interface similar to "Hot DLL reloading"

# DATA STRUCTURES AND TRANSFORMATION

- [ ] A transformative approach to game engine development: https://www.youtube.com/watch?v=FXKEiFUXBIo&t=1490s
- [ ] Data-Oriented Design http://www.dataorienteddesign.com/dodbook/

# HARDWARE

- [ ] Cache coherency primer: https://fgiesen.wordpress.com/2014/07/07/cache-coherency/
- [ ] GCN architecture: https://www.amd.com/Documents/GCN_Architecture_whitepaper.pdf

# PERFORMANCE

- [X] https://www.youtube.com/watch?v=DxP--1yEgKQ
  - Flame graph seems useful and supported by many profilers as data post process
  - Good online tool to do micro benchmark: http://quick-bench.com/
  - When benchmarking code (multiple execution) do not always consider min/max/average execution time but also the variance/deviation
- [X] Performance Profiling: https://medium.com/@jcowles/performance-profiling-d5f44b4b6f33
  - It is important to choose the good profiling metrics (e.g. number of dropped frames) i.e. What do I have to optimize? and How to measure it reliably?
  - Both micro (only the problematic code is executed) and synthetic (re-create artificially game conditions) benchmarks are important
  - Maximize the reproduceability of the issue e.g. if the issue occurs when spawning an entity, we should try doing it every frame
  - Always measure every single progress i.e. for each optimization, measure and document the relative improvement (keep all traces, graphs, etc.)
  - Find a graphical way to express your improvements in order to easily communicate them
- [X] RIOT Games - Profiling measurement and analysis: https://engineering.riotgames.com/news/profiling-measurement-and-analysis
  - Good presentation of the profiling methodology
  - Good visualization of cache relative speed
- [ ] RIOT Games - Profiling & optimization: https://engineering.riotgames.com/news/profiling-optimisation
- [ ] Pitfalls of Object Oriented Programming: https://drive.google.com/open?id=1SbmKU0Ev9UjyIpNMOQu7aEMhZBifZkw6

# PHYSICS & SIMULATION
- [] implementation of a methode for hydraulic erosion: https://github.com/OToL/doc/blob/master/engine/implementation%20of%20a%20methode%20for%20hydraulic%20erosion.pdf
- [] Water erosion on heightmap terrain: http://ranmantaru.com/blog/2011/10/08/water-erosion-on-heightmap-terrain/

# C++

- [x] lvalues, rvalues, glvalues, prvalues, xvalues: https://blog.knatten.org/2018/03/09/lvalues-rvalues-glvalues-prvalues-xvalues-help/
  - prvalues (pure rvalue): no identity and moveable
  - lvalue: identity and cannot be moved
  - xvalue: lvalue which can moved
  - gvalue: lvalue + xvalue
  - rvalue: xvalue + prvalue
- [x] Counting bits: https://lemire.me/blog/2018/02/21/iterating-over-set-bits-quickly/
  - Use on one complement (bitset & -bitset) property to implement fast set bit iteration
- [x] Beating up on qsort (for integers): https://travisdowns.github.io/blog/2019/05/22/sorting.html
  - Use radix sort as well as some common low level optimizations (e.g. avoid memory allocations, prefetch, etc.) to beat generic STL sort


# GRAPHICS

- [x] Thoughts on Skinning and LDS: https://turanszkij.wordpress.com/2018/02/03/thoughts-on-skinning-and-lds/
    - Put all bones information into LDS before triggering skinning shader instances
    - Interesting explanation about CU x shader x threads
- [x] Breaking down barriers
    - Part 1: https://mynameismjp.wordpress.com/2018/03/06/breaking-down-barriers-part-1-whats-a-barrier/
        - Good barrieer concept vulgarization i.e. real life -> cpu -> gpu
        - Barriers are not only about synchronizing thread of executions (Draw Call A must be finish before B starts) but also data flow i.e. cache flush, RT internal compression, etc.
        - Since it is very HW specific D3D12 and Vulkan have chosen to use the concept of resource states which implicitely synchronize threads and data (cache, etc.)
    - Part 2: https://mynameismjp.wordpress.com/2018/04/01/breaking-down-barriers-part-2-synchronizing-gpu-threads/
        - Barriers are reducing core(s) occupancy because the dispatches are not executed in parallel and the one in progress may no use all cores: "the performance cost of a flush is directly tied to the decrease in utilization"
        - We can improve core occupancy by interleaving dependent dispatches with independent ones
        - FLUSH command granularity is coarse i.e. it waiting for all previously issued dispatch to be finished
        - We can have much finer grain control with fences/labels
- [X] Octahedral Impostors: http://shaderbits.com/blog/octahedral-impostors
    - Very nice tree imposters technique based on multiple baked views around the model using a octahedral
    - Octahedral is better than a spehere because the vertices repartition is uniform
    - A half-octahedral is often sufficient because we don't care about object's bottom
    - This article also explain cheaper and less accurate techniques such as simple card boards with parallax
- [X] Daily Pathtracer: http://aras-p.info/blog/2018/03/28/Daily-Pathtracer-Part-1-Initial-C--/
    - Basic approach but interesting for people who does not know about it
- [ ] Real-time Realistic Rendering and Lighting of Forests: https://hal.inria.fr/hal-00650120/file/article.pdf
- [ ] Optimizing GPU occupancy: https://gpuopen.com/optimizing-gpu-occupancy-resource-usage-large-thread-groups/
- [x] GPU architectures: https://drive.google.com/file/d/12ahbqGXNfY3V-1Gj5cvne2AH4BFWZHGD/view
    - Very good overview of GPU architecture with exemples From NVidia and AMD
