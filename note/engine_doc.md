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
