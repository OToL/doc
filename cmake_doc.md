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