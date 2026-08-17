cmake_minimum_required(VERSION 3.10)
project(csdr-skimmer)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")

# Find required packages
find_package(PkgConfig REQUIRED)
pkg_check_modules(CSDR REQUIRED csdr++)
pkg_check_modules(FFTW REQUIRED fftw3f)

# Include directories
include_directories(${CSDR_INCLUDE_DIRS} ${FFTW_INCLUDE_DIRS})

# Link directories
link_directories(${CSDR_LIBRARY_DIRS} ${FFTW_LIBRARY_DIRS})

# Common library
add_library(bufmodule OBJECT bufmodule.cpp)

# CW Skimmer executable
add_executable(csdr-cwskimmer cw-skimmer.cpp $<TARGET_OBJECTS:bufmodule>)
target_link_libraries(csdr-cwskimmer ${CSDR_LIBRARIES} ${FFTW_LIBRARIES})

# RTTY Skimmer executable
add_executable(csdr-rttyskimmer rtty-skimmer.cpp $<TARGET_OBJECTS:bufmodule>)
target_link_libraries(csdr-rttyskimmer ${CSDR_LIBRARIES} ${FFTW_LIBRARIES})

# Testing
enable_testing()
add_test(NAME cwskimmer_help COMMAND csdr-cwskimmer --help WILL_FAIL)
add_test(NAME rttyskimmer_help COMMAND csdr-rttyskimmer --help WILL_FAIL)
