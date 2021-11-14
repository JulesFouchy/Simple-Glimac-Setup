# Simple-Glimac-Setup

This is an alternative setup to follow [these tutorials](https://igm.univ-mlv.fr/~biri/Enseignement/IMAC2/opengl-TPs/opengl.php?section=teaching&teaching=opengl&teaching_section=tds). It has the advantage that **it is easy to use an all platforms** (Linux, Windows and Mac). It also fixes an annoying thing with the original setup: with this one you don't need to re-run CMake when you modify your shaders. The changes will be detected and handled automatically.

## Compiling

You need to install [CMake](https://cmake.org/download/).

To use CMake I recommend this VS Code extension : [ms-vscode.cmake-tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools). You will need to setup the extension with a compiler. Here is [the tutorial](https://code.visualstudio.com/docs/cpp/cmake-linux). It is based on Linux but at the bottom of the page you will find the explanations to adapt it for [Windows](https://code.visualstudio.com/docs/cpp/config-msvc) and [Mac](https://code.visualstudio.com/docs/cpp/config-clang-mac).

Alternatively you can just create a *build* folder at the root of this project, open a terminal and run `cmake ..` ; chances are it will detect what compiler you have installed and generate the appropriate Makefile / Visual Studio solution / Xcode project.

## TPs

I have already made 9 TP directories that are ready for you to code.
If you ever need more, simply duplicate one of them and update CMakeLists.txt (at the bottom of the file you will see the registration of all the TP folders : 
```cmake
setup_tp(TP1)
setup_tp(TP2)
# ...
```

## User inputs

To learn more about the parameters you receive in the callbacks, read [glfw's documentation](https://www.glfw.org/docs/latest/input_guide.html).

## assets

The *assets* folder will be copied to the folder where your executable is created. You can put all the assets that your project needs in there, like textures, shaders, 3D models *etc.*
