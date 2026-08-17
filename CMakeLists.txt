cmake_minimum_required(VERSION 3.10)
project(csdr-skimmer-romiansyah)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add your source files
add_executable(csdr-skimmer-romiansyah 
    src/main.cpp
    # Add other source files as needed
)

# Add any include directories
target_include_directories(csdr-skimmer-romiansyah PRIVATE include)

# Link any required libraries
# target_link_libraries(csdr-skimmer-romiansyah PRIVATE somelib)

# Enable testing
enable_testing()
add_test(NAME BasicTest COMMAND csdr-skimmer-romiansyah)
