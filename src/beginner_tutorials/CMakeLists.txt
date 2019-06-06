cmake_minimum_required(VERSION 2.8.3)
project(beginner_tutorials)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation	
)

## Generate messages in the 'msg' folder
 add_message_files(
   FILES
   Num.msg
 )

## Generate services in the 'srv' folder
 add_service_files(
   FILES
   AddTwoInts.srv
 )

## Generate added messages and services with any dependencies listed here
 generate_messages(
   DEPENDENCIES
   std_msgs
 )

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES beginner_tutorials
  CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

 add_executable(talker src/talker.cpp)
 add_dependencies(talker beginner_tutorials_generate_messages_cpp)
 target_link_libraries(talker
   ${catkin_LIBRARIES}
 )

 add_executable(listener src/listener.cpp)
 add_dependencies(listener beginner_tutorials_generate_messages_cpp)
 target_link_libraries(listener
   ${catkin_LIBRARIES}
 )




 add_executable(add_two_ints_server src/add_two_ints_server.cpp)
 add_dependencies(add_two_ints_server beginner_tutorials_gencpp)
 target_link_libraries(add_two_ints_server ${catkin_LIBRARIES})


 add_executable(add_two_ints_client src/add_two_ints_client.cpp)
 add_dependencies(add_two_ints_client beginner_tutorials_gencpp)
 target_link_libraries(add_two_ints_client ${catkin_LIBRARIES})

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_beginner_tutorials.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
