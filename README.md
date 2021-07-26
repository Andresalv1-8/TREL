# TSEL
## TECSpace Engine Lib
This library is still in early development, only debug compiling options for x64 have been configured and tested for Windows and Unix like systems.

## Portability
Given that this library expects to calculate data for rockets in many ways, allowing the same functionality to be 
easily ported to any high level programming language having the basis at C will make the initial effort more 
scalable as it could even be used to interface straight from embedded systems that gather data and compare it to the 
one generated in real time from the library, or also using the basic funtions to create an advanced GUI

# Build process
The current build method uses CMake, modifying the CMakeLists.txt file allows the user to generate a static or dynamic library by changing `"Build Shared Libraries" ON to OFF` depending on what is desired, just as well as `"Build app" ON` can be toggled to generate the testing app which links automatically to the library.

## Usinc CMake

### With GNU make
```
mkdir build && cd build
cmake ..
make
```

### WIth MSVC in Visual Studio
Open the directory in VS, let CMake generate the project, then select on *Build project* at the top of VS and then the final build will be created, currently only Debug x64 exists

### With MSVC for other IDEs/Text editors with Visual Studio avaliable
Guessing you have a `build/`, run cmake from there with `cmake ..`

When the project is built, there will be a `.sln` file which once it's oppened on Visual Studio it will allow to build de project, then leaving the library and app if chosen.

## Using only GCC and make
In case you want to stay away from CMake, this should work for all Unix like systems, but it isn't the recommended route

### Compiling the shared object from a subdirectory build
```
mkdir build && cd build
gcc -c -Wall -Wextra -pedantic -Werror -fpic ../src/*.c -I../include/
gcc -shared -o libapplib.so ./*.o
```
### Building main.c and linking to the lib from the build subdirectory
```
gcc -o app ../main.c -Wall -Wextra -pedantic -Werror -I../include/ -L. -lapplib -lm
export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH
```

