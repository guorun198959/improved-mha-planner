cmake_minimum_required(VERSION 2.8.3)
project(improved_mha_planner)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "-std=c++11")
add_definitions(-DROS)

find_package(Boost REQUIRED)

find_package(catkin REQUIRED COMPONENTS rosconsole)

find_package(PkgConfig REQUIRED)
pkg_check_modules(gsl REQUIRED gsl)

find_package(sbpl REQUIRED)

catkin_package(
  CATKIN_DEPENDS rosconsole
  DEPENDS gsl
  INCLUDE_DIRS include ${SBPL_INCLUDE_DIRS}
  LIBRARIES sbpl_ros ${SBPL_LIBRARIES})

include_directories(${Boost_INCLUDE_DIRS})
include_directories(${catkin_INCLUDE_DIRS})
include_directories(${gsl_INCLUDE_DIRS})
include_directories(${SBPL_INCLUDE_DIRS})
include_directories(include)

add_library(sbpl_ros src/planners/mha_planner.cpp)
target_link_libraries(sbpl_ros ${gsl_LIBRARIES} ${catkin_LIBRARIES} ${SBPL_LIBRARIES})
