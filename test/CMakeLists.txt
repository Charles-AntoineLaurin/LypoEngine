cmake_minimum_required(VERSION 3.8)

project(lypo_engine_test)

include_directories(src)
enable_testing()

#Dependencies include
add_subdirectory(dependencies/googletest)
include_directories(dependencies/googletest/googletest/include)
include_directories(dependencies/googletest/googlemock/include)

include_directories(../LypoEngine/src)

file(GLOB_RECURSE TEST_SOURCES src/*cpp src/*.h)

# Activer AddressSanitizer pour la compilation
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    target_compile_options(test_executable PRIVATE -fsanitize=address -g)
    target_link_libraries(test_executable PRIVATE -fsanitize=address)
endif()

add_executable(lypo_engine_test ${TEST_SOURCES} )

# To be changed once it works
# target_link_libraries(lypo_engine_test lypo_engine gtest)
target_link_libraries(lypo_engine_test gtest)