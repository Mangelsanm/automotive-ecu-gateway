# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)

# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.2.0)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.2.0-a4)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico2_w CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(automotive-ecu-gateway C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(automotive-ecu-gateway
        src/app/main.c
        src/app/app_tasks.c
        src/app/app_state.c
        src/drivers/hal_timer.c
        src/drivers/uart.c
        src/kernel/timebase.c
        src/kernel/scheduler.c
        src/kernel/soft_timer.c
        src/kernel/event.c
        )

pico_set_program_name(automotive-ecu-gateway "automotive-ecu-gateway")
pico_set_program_version(automotive-ecu-gateway "0.1")

# Modify the below lines to enable/disable output over UART/USB
pico_enable_stdio_uart(automotive-ecu-gateway 0)
pico_enable_stdio_usb(automotive-ecu-gateway 0)

# Add the standard library to the build
target_link_libraries(automotive-ecu-gateway
        pico_stdlib)

# Add the standard include files to the build
target_include_directories(automotive-ecu-gateway PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}/src/kernel
        ${CMAKE_CURRENT_LIST_DIR}/src/drivers
        ${CMAKE_CURRENT_LIST_DIR}/src/app
        ${CMAKE_CURRENT_LIST_DIR}/src/hal/pico2
        )

# Add any user requested libraries
target_link_libraries(automotive-ecu-gateway

        )

pico_add_extra_outputs(automotive-ecu-gateway)
