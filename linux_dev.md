- [Steam Dev days] Getting Started with Linux Game Development : https://www.youtube.com/watch?v=Sd8ie5R4CVE
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
- [Steam Dev days] Game Development with SDL 2.0: https://www.youtube.com/watch?v=MeMPCSqQ-34
- [Steam Dev days] Getting Started Debugging on Linux : https://www.youtube.com/watch?v=xTmAknUbpB0
- [Steamworks Development] https://www.youtube.com/user/SteamworksDev
    * To investigate available videos
- [Steamworks Development] Building Unity Games for SteamOS/Linux: https://www.youtube.com/watch?v=WYdOQ_k6YvI
- Porting Games To Linux: https://www.youtube.com/watch?v=d8kfva6G0c4
- [VS2017] Linux development with C++: https://www.youtube.com/watch?v=XIiFuBczd6A & https://www.youtube.com/watch?v=4NenIuAbtGs