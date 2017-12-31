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
- [ ] Compilation time : http://ourmachinery.com/post/physical-design/
- [ ] Stingray engine walkthrough: https://www.youtube.com/watch?v=LgbSYxf9vT4&list=PLUxuJBZBzEdxzVpoBQY9agA8JUgNkeYSV
    1. Overview
        - Good pillars
        - Interesting packaging system to download all dependencies using S3
        - Remote file system for consoles which is also taking care of data compilation
        - Plugin system with C like interface similar to "Hot DLL reloading"
    2. Memory