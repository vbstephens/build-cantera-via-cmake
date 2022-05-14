# build-cantera-via-cmake
Builds and installs Cantera 2.5.1 via CMake's FetchContent and ExternalProject modules for use in C++ codes. 

CMake project options live in the top-level `CMakeLists.txt` file. To change Cantera build options, alter the `ExternalProject_Add` command options in `ext/CmakeLists.txt`. To use a different version of Cantera, change the `GIT_TAG` specifier of the `FetchContent_Declare` statement in `ext/CmakeLists.txt`. Linking is done in `src/CMakeLists.txt` and is set up such that you can also use Cantera's installations of Sundials and yaml-cpp as long as you include the appropriate headers in your C++ code.

Because Cantera is added via ExternalProject, its contents will not be immediately available like they would be if you could use FetchContent. The `cantera` CMake target must be manually built and installed before your project targets for everything to work properly. If you are working from the command line, for instance, you would, after creating and navigating into the `build` directory, run the following commands in this order:
1. `cmake ..`
2. `make cantera`
3. `make`
4. `install`

You should then be able to `#include` whatever parts of Cantera you want to use, and the `Cantera` namespace should be available.