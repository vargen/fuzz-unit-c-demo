cmake_minimum_required(VERSION 3.16)
project(cmake_example)

enable_testing()

find_package(cifuzz)
enable_fuzz_testing()

add_subdirectory(src)

add_executable(${PROJECT_NAME} main.cpp )
target_link_libraries(${PROJECT_NAME} PRIVATE exploreMe)

# Unit Test Code
add_executable(my_unit_test my_unit_test.cpp)
target_link_libraries(my_unit_test PRIVATE exploreMe)

# define tests
add_test(
  NAME my_unit_test
  COMMAND $<TARGET_FILE:my_unit_test>
)

add_fuzz_test(my_fuzz_test my_fuzz_test.cpp)
target_link_libraries(my_fuzz_test PRIVATE exploreMe)


