# Configure opencv environment in Clion 
0. need MinGW and CMake
1. cmake generate
2. mingw32-make
3. mingw32-make install
4. add D:\Software\opencv\mingw_build\install\x86\mingw\bin to path
5. CMakeLists.txt
```
cmake_minimum_required(VERSION 3.14)
project(example)

set(CMAKE_CXX_STANDARD 11)

set(OpenCV_DIR "D:\\Software\\opencv\\mingw_build\\install")
set(CMAKE_MODULE_PATH $(CMAKE_MODULE_PATH) "${CMAKE_SOURCE_DIR}\\cmake\\")

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# add executable
add_executable(example main.cpp)

# add libs
set(OpenCV_LIBS opencv_core opencv_highgui opencv_imgproc opencv_imgcodecs)

# linking
target_link_libraries(example ${OpenCV_LIBS})

```