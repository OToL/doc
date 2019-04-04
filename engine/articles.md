# CMAKE

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

- [] https://lwn.net/Articles/276782/

# ENGINE ARCHITECTURE

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
- [ ] How to Open a Black Box: https://www.youtube.com/watch?v=SYomOZIfeoU
- [ ] Compilation time: http://ourmachinery.com/post/physical-design/
- [ ] Stingray engine walkthrough: https://www.youtube.com/watch?v=LgbSYxf9vT4&list=PLUxuJBZBzEdxzVpoBQY9agA8JUgNkeYSV
    1. Overview
        - Good pillars
        - Interesting packaging system to download all dependencies using S3
        - Remote file system for consoles which is also taking care of data compilation
        - Plugin system with C like interface similar to "Hot DLL reloading"
    2. Memory
- [ ] Data oriented design indexing: https://github.com/dbartolini/data-oriented-design
- [ ] Data oriented design: http://www.dataorienteddesign.com/dodmain/node1.html
- [ ] A transformative approach to game engine development: https://www.youtube.com/watch?v=FXKEiFUXBIo&t=1490s

# HARDWARE

- [ ] Cache coherency primer: https://fgiesen.wordpress.com/2014/07/07/cache-coherency/
- [ ] GCN architecture: https://www.amd.com/Documents/GCN_Architecture_whitepaper.pdf

# PERFORMANCE

- Index of interesting performance/profiling related blogs, videos and articles: https://github.com/fenbf/AwesomePerfCpp
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
