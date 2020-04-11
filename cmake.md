# BEST PRACTICES

- Think in terms of targets and properties
- Don't use glob files because cmake does not detect file addition/removal
- Use lower-case for function/macros because they are case insensitive (myfunc() is same as myFun())
- Always specify cmake_minimum_required because it conditions checks/policies being used

# BUILD SYSTEM GENERATION

- Generates build scripts to 'build' folder
```bash
    > mkdir build
    > cd build
    > cmake <sources_path>
```
- Compile project
```bash
    > cd build
    > make
    or
    > cmake -S <sources_path> -B <build_folder_path>
```

# SCRIPTING

## VARIABLES BASICS

- By default variables are visible only within the scope they are defined (add_subdirectory or function)
- Variables can be promoted to the parent scope by specifying PARENT_SCOPE
```cmake
    set(MY_VAR "value" PARENT_SCOPE)
``` 
- Variables identifiers are case sensitive
```cmake
    # Different
    set(MY_VAR "value")
    set(my_var "value")
```
- Unquoted words are treated as strings
```cmake
   # Same
   set(MY_VAR "value")
   set(MY_VAR value) 

   # Same
   my_fun("value") 
   my_fun(value)
```
- Supported value types are: String, Bool, Number and List of values
- Boolean are actually treated like strings and are case insensitive
```cmake
    # Same
    set(BOOL_VAR TRUE)
    set(BOOL_VAR TruE)
    set(BOOL_VAR "TRUE")
    set(BOOL_VAR "TrUe")
```
- Set/Get environment variable
```cmake
    set(ENV{MY_ENV_VAR} "my value")
    set(MY_VAR $ENV{MY_ENV_VAR})
```

## LIST

- Lists are stored in variables as semi-column separated values and initialized either using their internal representation or list of individual values 
```cmake
    # Same
    set(MY_LIST a b c)
    set(MY_LIST "a" "b" "c")
    set(MY_LIST "a;b;c")
```
- List values can be unpacked via ${} and packed via ""
- List manipulation (add, remove, join, etc.) can be done through 'list' macro

## CACHED VARIABLE

- Up-on startup, cmake is loading variables from a cache (CMakeCache.txt) located in build folder
- New cached variable can be added/initialized from script using CACHE keyword but only if it does not already exist in the cache i.e. 'set' has no effect and the underlying value not modified if already present in the cache 
```cmake
    set(MY_CACHED_VAR "my value" CACHE STRING "My variable description visible in UI")
```
- Cached variables are visible and settable from both the cmake-ui and command-line via -D<var_name>=<new value>. Setting cached variable this way is updating the CMake cache
- You can still modify the variable value in the current execution, but it will not be updated in the cache
```cmake
    set(MY_CACHED_VAR "my value" CACHE STRING "My variable description visible in UI")

    # MY_CACHED_VAR is already in the cache and 'set' has no effect i.e. MY_CACHED_VAR="my value"
    set(MY_CACHED_VAR "my new value" CACHE STRING "My new description")
   
    # MY_CACHED_VAR is modified just for this execution i.e. MY_CACHED_VAR="my new value" but still "my value" in the cache
    set(MY_CACHED_VAR "my new value")
```
- It is also possible to update the variable value in the cmake cache from the script by specifying FORCE
```cmake
    set(MY_CACHED_VAR "my value" CACHE STRING "My variable description visible in UI")

    # Even if MY_CACHED_VAR is already in the cache, its value is forced to "my new value" for both the current execution and the cache
    set(MY_CACHED_VAR "my new value" CACHE STRING "My new description" FORCE)
```
- A cached variable can be hidden from cmake-ui and the command line -D by either specifying INTERNAL or using mark_as_advanced
```cmake
    set(MY_CACHED_VAR "my value" CACHE INTERNAL "")
    # Same as
    set(MY_CACHED_VAR "my value" CACHE "")
    mark_as_advanced(MY_CACHED_VAR)
```
- Since bool cached variable are commonly used (e.g. enable feature X), there is a shortcut for these
```cmake
    option(MY_OPTION "My test option" OFF)
    # Same as
    set(MY_OPTION OFF CACHE BOOL "My test option")
```

## CONTROL FLOW

- 'if' is special in a way that it evaluates/expands variables
```cmake
    set(MY_VAR "value")

    # Same
    if(MY_VAR)
    endif()

    if(${MY_VAR})
    endif()
```
- 'if' is actually expanding variables until they expand to one of the value below
```cmake
    if(variable)
        # If variable is `ON`, `YES`, `TRUE`, `Y`, or non zero number
    else()
        # If variable is `0`, `OFF`, `NO`, `FALSE`, `N`, `IGNORE`, `NOTFOUND`, `""`, or ends in `-NOTFOUND`
    endif()
   # If variable does not expand to one of the abovint ae, CMake will expand it then try again
```

## TARGETS

- PUBLIC/PRIVATE/INTERFACE
    - PRIVATE: Properties required to build the target (e.g. external include dir to build cpp) and NOT passed to targets which depend on it
    - INTERFACE: Properties not needed to build the target but passed to targets which depend on it (e.g. commonly used compilation options)
    - PUBLIC: PRIVATE+INTERFACE 

# PITFALLS

- cmake_minimum_required has to be set to the latest version because it defines cmake policies/behavior being used
- CMake functions and macros are case insensitive i.e. foo() and FoO() is the same 
- When a variable may contain list separator token (';'), always surround value extraction with double quotes to avoid the result to be expanded to multiple separated values
```
    set(MY_VAR "Hello ; world")
   
    # Output: "Hello ; world"
    message("${MY_VAR}")
    # Output: "Hello world"
    message(${MY_VAR})
```

# TIPS

- More verbose generation: pass -V or --verbose to cmake generetion
- More verbose build: 
    - set(CMAKE_VERBOSE_MAKEFILE ON) in script 
    - Pass -DCMAKE_VERBOSE_MAKEFILE:BOOL=ON-D to cmake
    - via make: ">VERBOSE=1 make" or ">make VERBOSE=1"
- Enable CMake developers warnings: pass -Wdev to cmake
- Use CMake as script language
```bash
    > cmake -P <file_path>
```
