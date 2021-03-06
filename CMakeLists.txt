cmake_minimum_required (VERSION 3.2)
cmake_policy(SET CMP0054 NEW)

project (starter)

# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Specify bin path
set (EXECUTABLE_OUTPUT_PATH bin/)

# Specify source files
set(SRC_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp)

# Specify executable
add_executable(starter ${SRC_FILES})

# Configure the AFF3CT library before compiling it
option(AFF3CT_COMPILE_EXE        ""      OFF            )
option(AFF3CT_COMPILE_STATIC_LIB ""      ON             )
option(AFF3CT_COMPILE_SHARED_LIB ""      OFF            )
option(AFF3CT_LINK_GSL           ""      OFF            )
option(AFF3CT_LINK_MKL           ""      OFF            )
set   (AFF3CT_PREC               "MULTI" CACHE STRING "") # can be '8', '16', '32', '64' or 'MULTI'

# Compile the AFF3CT library
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/lib/aff3ct/)

# Link with AFF3CT
target_link_libraries(starter PRIVATE aff3ct-static-lib)
