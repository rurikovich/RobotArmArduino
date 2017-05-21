cmake_minimum_required(VERSION 2.8.4)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/cmake/ArduinoToolchain.cmake)
set(PROJECT_NAME robotArm)
project(${PROJECT_NAME})

set(mega.build.mcu atmega2560)
set(mega.upload.protocol stk500v2)
set(mega.upload.speed 115200)

link_directories(${ARDUINO_SDK}/libraries)


generate_arduino_library(robotArm_lib
        SRCS robotArm_lib/RampsStepper.cpp robotArm_lib/robotCommand.cpp robotArm_lib/fanControl.cpp robotArm_lib/gripper.cpp robotArm_lib/interpolation.cpp robotArm_lib/robotGeometry.cpp
        HDRS robotArm_lib/RampsStepper.h robotArm_lib/robotCommand.h robotArm_lib/fanControl.h robotArm_lib/gripper.h robotArm_lib/interpolation.h robotArm_lib/robotGeometry.h robotArm_lib/pinout.h robotArm_lib/queue.h
        BOARD mega)

#generate_arduino_library(robotArm_lib
#        SRCS robotArm_lib/RampsStepper.cpp
#        HDRS robotArm_lib/RampsStepper.h
#        BOARD mega)



set(${CMAKE_PROJECT_NAME}_BOARD mega)
set(${CMAKE_PROJECT_NAME}_PORT /dev/tty.usbmodem1421)
set(${CMAKE_PROJECT_NAME}_LIBS robotArm_lib)
set(${CMAKE_PROJECT_NAME}_SKETCH robotArm.ino)

generate_arduino_firmware(${CMAKE_PROJECT_NAME})

