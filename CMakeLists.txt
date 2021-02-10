cmake_minimum_required(VERSION 3.16)

project(Chat)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
include(Util)
find_or_get(GMock)
find_or_get(GTest)
find_or_get(Boost)
find_package(Threads)
set(CXX_STANDARD_REQUIRED ON)

add_executable(server chat_server.cpp)
target_include_directories(server PUBLIC ${GMOCK_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
set_property(TARGET server PROPERTY CXX_STANDARD 17)
target_link_libraries(server Threads::Threads ${GMOCK_BOTH_LIBRARIES} ${GTEST_BOTH_LIBRARIES} ${Boost_LIBRARIES})

add_executable(client chat_client.cpp)
target_include_directories(client PUBLIC ${GMOCK_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
set_property(TARGET client PROPERTY CXX_STANDARD 17)
target_link_libraries(client Threads::Threads ${GMOCK_BOTH_LIBRARIES} ${GTEST_BOTH_LIBRARIES} ${Boost_LIBRARIES})
