cmake_minimum_required(VERSION 3.15 FATAL_ERROR)
project(cppmyapp VERSION 1.0 LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
#set(CMAKE_VERBOSE_MAKEFILE  ON) #enable for debugging

set(BUILD_SHARED_LIBS on) # let the users of your library choose what flavor to build.


message(STATUS "Building ${PROJECT_NAME} ${PROJECT_VERSION}")

#find_package(range-v3 REQUIRED)
# https://stackoverflow.com/questions/2368811/how-to-set-warning-level-in-cmake/50882216#50882216
if(MSVC)
  add_compile_options(/W4 /WX)
else()
  # See https://foonathan.net/2018/10/cmake-warnings/
  add_compile_options(-Wall -Wextra -pedantic-errors)
endif()

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

include_directories(include) #global include for all target
add_executable(app src/myapp.cpp)
target_link_libraries(app ${CONAN_LIBS})
target_compile_features(app PUBLIC cxx_std_20)


