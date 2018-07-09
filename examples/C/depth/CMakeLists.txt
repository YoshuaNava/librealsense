#  minimum required cmake version: 3.1.0
cmake_minimum_required(VERSION 3.1.0)

project(RealsenseExamples-Depth)

# Save the command line compile commands in the build output
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

add_executable(any-rs-depth rs-depth.c ../example.h)
target_link_libraries(any-rs-depth ${DEPENDENCIES})
set_target_properties (any-rs-depth PROPERTIES
FOLDER "Examples/C"
)

install(
TARGETS

any-rs-depth

RUNTIME DESTINATION
${CMAKE_INSTALL_PREFIX}/bin
)

