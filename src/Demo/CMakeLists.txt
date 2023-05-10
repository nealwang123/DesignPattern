#指定CMake的最小~最大版本，一般只需指定最小版本。
cmake_minimum_required(VERSION 3.0.0)
#指定项目名称及版本号，初始化项目相关变量。
project(Demo VERSION 1.0.0)

#指定C++标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
# 设置变量
#set(ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR})


if (MSVC)
    # warning level 4 and all warnings as errors
    add_compile_options(/W4 /WX)
else()
    # lots of warnings and all warnings as errors
    add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()


# add_library根据源码来生成一个库供他人使用。<name>是个逻辑名称，在项目中必须唯一。完整的库名依赖于具体构建方式（可能为lib<name>.a or <name>.lib）。
# STATIC指静态库，SHARED指动态库，MODULE指在运行期通过类似于dlopen的函数动态加载。
#add_library(<name> [STATIC | SHARED | MODULE] [EXCLUDE_FROM_ALL] [<source>...])


# link_libraries 这个API已经废弃，请参考target_link_libraries()的用法。
# link_libraries([item1 [item2 [...]]] [[debug|optimized|general] <item>] ...)


#为目标文件链接依赖的库。PUBLIC修饰的库或目标会被链接，并成为链接接口的一部分。PRIVATE修饰的目标或库会被链接，但不是链接接口的一部分。
#INTERFACE修饰的库会追加到链接接口中，但不会用来链接目标文件<target>。
# target_link_libraries(<target>
#                       <PRIVATE|PUBLIC|INTERFACE> <item>...
#                      [<PRIVATE|PUBLIC|INTERFACE> <item>...]...)


# 头文件查找目录
# 将指定目录添加到编译器的头文件搜索路径之下，指定目录被解释为当前源码路径的相对路径。[AFTER|BEFORE]定义了追加指定目录的方式在头还是尾。[SYSTEM]告诉编译器在一些平台上指定目录被当作系统头文件目录。
# include_directories([AFTER|BEFORE] [SYSTEM] dir1 [dir2 ...])


#从指定的文件加载、运行CMake代码。如果指定文件，则直接处理。如果指定module，则寻找module.cmake文件，首先在${CMAKE_MODULE_PATH}中寻找，然后在CMake的module目录中查找。
#include(<file|module> [OPTIONAL] [RESULT_VARIABLE <VAR>] [NO_POLICY_SCOPE])


# 在编译目标文件<target>时指定头文件。<target>必须是通过add_executable()或add_library()创建，且不能是ALIAS目标。<INTERFACE|PUBLIC|PRIVATE>修饰其紧跟参数items的作用范围。
# target_include_directories(<target> [SYSTEM] [AFTER|BEFORE]
#   <INTERFACE|PUBLIC|PRIVATE> [items1...]
#   [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])


# 库文件查找目录
#为链接器添加库的搜索路径，此命令调用之后生成的目标才能生效。link_directories()要放在add_executable()之前。
#link_directories([AFTER|BEFORE] directory1 [directory2 ...])


# find_package一般用于加载外部库到项目中，并且会加载库的细节信息。如上find_package有两种模式：Module与Config。
# ## 共支持两种模式
# # mode1: Module, 此模式需访问Find<PackageName>.cmake文件
# find_package(<PackageName> [version] [EXACT] [QUIET] [MODULE]
#              [REQUIRED] [[COMPONENTS] [components...]]
#              [OPTIONAL_COMPONENTS components...]
#              [NO_POLICY_SCOPE])

# # mode2: Config, 此模式需访问<lowercasePackageName>-config.cmake or <PackageName>Config.cmake
# find_package(<PackageName> [version] [EXACT] [QUIET]
#              [REQUIRED] [[COMPONENTS] [components...]]
#              [OPTIONAL_COMPONENTS components...]
#              [CONFIG|NO_MODULE]
#              [NO_POLICY_SCOPE]
#              [NAMES name1 [name2 ...]]
#              [CONFIGS config1 [config2 ...]]
#              [HINTS path1 [path2 ... ]]
#              [PATHS path1 [path2 ... ]]
#              [PATH_SUFFIXES suffix1 [suffix2 ...]]
#              [NO_DEFAULT_PATH]
#              [NO_PACKAGE_ROOT_PATH]
#              [NO_CMAKE_PATH]
#              [NO_CMAKE_ENVIRONMENT_PATH]
#              [NO_SYSTEM_ENVIRONMENT_PATH]
#              [NO_CMAKE_PACKAGE_REGISTRY]
#              [NO_CMAKE_BUILDS_PATH] # Deprecated; does nothing.
#              [NO_CMAKE_SYSTEM_PATH]
#              [NO_CMAKE_SYSTEM_PACKAGE_REGISTRY]
#              [CMAKE_FIND_ROOT_PATH_BOTH |
#               ONLY_CMAKE_FIND_ROOT_PATH |
#               NO_CMAKE_FIND_ROOT_PATH])


#使用指定的源文件来生成目标可执行文件。具体分为三类：普通、导入、别名。此处我们就以普通可执行文件进行说明。
# # 第一种：Normal Executables
# add_executable(<name> [WIN32] [MACOSX_BUNDLE]
# [EXCLUDE_FROM_ALL]
# [source1] [source2 ...])
# # 第二种：Imported Executables
# add_executable(<name> IMPORTED [GLOBAL])
# # 第三种：Alias Executables
# add_executable(<name> ALIAS <target>)
#其中<name>是可执行文件的名称，在cmake工程中必须唯一。WIN32用于在windows下创建一个以WinMain为入口的可执行文件。MACOSX_BUNDLE用于mac系统或者IOS系统下创建一个GUI可执行应用程序。

add_executable(Demo01 main.cpp)

install(TARGETS Demo01 DESTINATION ${DP_INSTALL_BIN_DIR})
install(TARGETS Demo01 DESTINATION bin)