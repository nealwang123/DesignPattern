cmake_minimum_required(VERSION 3.2)

project(CMakeTemplate)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -O3")

set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR})

set(DP_INSTALL_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)
set(DP_INSTALL_BIN_DIR ${PROJECT_SOURCE_DIR}/bin)
set(DP_INSTALL_LIB_DIR ${PROJECT_SOURCE_DIR}/lib)


include_directories(${DP_INSTALL_INCLUDE_DIR})

#将子目录添加到构建系统中。source_dir指定一个目录，其中存放CMakeLists.txt文件和代码文件。binary_dir指定的目录存放输出文件，如果没有指定则使用source_dir。
#add_subdirectory(source_dir [binary_dir] [EXCLUDE_FROM_ALL])
add_subdirectory(src)
#add_subdirectory(test)