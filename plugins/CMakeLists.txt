add_subdirectory(camera)
add_subdirectory(clock)
add_subdirectory(controlboard)
add_subdirectory(externalwrench)
add_subdirectory(fakecontrolboard)
add_subdirectory(forcetorque)
add_subdirectory(imu)

# This plugin will be removed soon ( https://github.com/robotology/gazebo-yarp-plugins/issues/213 )
# for the time being do not update it for compliance with Gazebo 9
if (GAZEBO_VERSION VERSION_LESS 9.0)
    add_subdirectory(jointsensors)
endif()

add_subdirectory(showmodelcom)
add_subdirectory(multicamera)
add_subdirectory(maissensor)

find_package(OpenCV QUIET)
option(GAZEBO_YARP_PLUGINS_HAS_OPENCV "Compile plugins that depend on OpenCV" ${OpenCV_FOUND})

if(GAZEBO_YARP_PLUGINS_HAS_OPENCV)
    add_subdirectory(videotexture)
else()
    message(STATUS "GAZEBO_YARP_PLUGINS_HAS_OPENCV CMake option set to off, disabling videotexture plugin.")
endif()

if( GAZEBO_VERSION VERSION_GREATER 3.9 )
    add_subdirectory(worldinterface)
else()
    message(WARNING "Gazebo version is lower than 4.0, disabling worldinterface plugin.")
endif()

if( (NOT (GAZEBO_VERSION VERSION_LESS 6)) AND (NOT (YARP_VERSION VERSION_LESS 2.3.68)) )
    add_subdirectory(lasersensor)
else()
    message(STATUS "Gazebo version is lower than 6 or YARP version is lower than 2.3.68, disabling  lasersensor plugin.")
endif()

# disabling depthCamera plugin until it is updated to latest changes in yarp
if( (NOT (GAZEBO_VERSION VERSION_LESS 7)) AND (NOT (YARP_VERSION VERSION_LESS 2.3.67)) )
    add_subdirectory(depthCamera)
else()
    message(STATUS "Gazebo version is lower than 7 or YARP version is lower than 2.3.67, disabling depthCamera  plugin.")
endif()

