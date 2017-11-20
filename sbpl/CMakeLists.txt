cmake_minimum_required(VERSION 2.8.3)
project(improved_mha_planner)

set(ROS_BUILD_TYPE Release)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "-std=c++0x")
add_definitions(-DROS)

find_package(Boost REQUIRED)

find_package(catkin REQUIRED COMPONENTS roscpp)

find_package(PkgConfig REQUIRED)
pkg_check_modules(gsl REQUIRED gsl)

find_package(sbpl REQUIRED)

catkin_package(
  CATKIN_DEPENDS roscpp
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

# Download needed data file
# download_test_data(http://pr.willowgarage.com/data/sbpl/env_examples/nav2d/willow-25mm-inflated-env.cfg
#   env_examples/nav2d/willow-25mm-inflated-env.cfg 1b4551eeba6df03b6e597e598bbaa4f3)
