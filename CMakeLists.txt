cmake_minimum_required(VERSION 3.21)
project(MizuRunner CXX)

add_subdirectory(argparse)
add_subdirectory(mizuvm)

add_executable(${PROJECT_NAME} runner.cpp)
set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "mizu")
target_link_libraries(${PROJECT_NAME} PUBLIC mizu::vm argparse)

