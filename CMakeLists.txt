cmake_minimum_required(VERSION 3.22)
project(Eigensolver) # Eigensolver is the name of the project

set(CMAKE_CXX_STANDARD 17)  

# Set the location of the madness directory (where the source code is located)
set(MADNESS_DIR "../madness")

# Include my one header files
include_directories(${CMAKE_SOURCE_DIR}/Eigensolver/include)

# Specify your source files
set(SOURCE_FILES
    Eigensolver/src/eigensolver.cc
    # Add any other .cc files in src/ here
    )

find_package(MADNESS CONFIG REQUIRED)

file(COPY ${CMAKE_SOURCE_DIR}/Eigensolver/plot/run_eigensolver.sh
     DESTINATION ${CMAKE_BINARY_DIR})

# Create the executable from your source files
add_executable(Eigensolver ${SOURCE_FILES})

# Link the madness library to your project
target_link_libraries(Eigensolver madness)

