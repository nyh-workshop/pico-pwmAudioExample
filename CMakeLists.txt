# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
set(PICO_SDK_PATH "E:/pico-sdk")

set(PICO_EXTRAS_PATH "E:/pico-extras")

set(PICO_BOARD pico CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

# We also need PICO EXTRAS
include(pico_extras_import.cmake)

if (PICO_SDK_VERSION_STRING VERSION_LESS "1.4.0")
  message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.4.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

project(pico-pwmAudio C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(pico-pwmAudio pico-pwmAudio.c audio_pwm.c sample_encoding.cpp)

pico_generate_pio_header(pico-pwmAudio ${CMAKE_CURRENT_LIST_DIR}/audio_pwm.pio)

pico_set_program_name(pico-pwmAudio "pico-pwmAudioExample")
pico_set_program_version(pico-pwmAudio "0.1")

pico_enable_stdio_uart(pico-pwmAudio 1)
pico_enable_stdio_usb(pico-pwmAudio 0)

# Add the standard library to the build
target_link_libraries(pico-pwmAudio
pico_audio
pico_stdlib)

# Add the standard include files to the build
target_include_directories(pico-pwmAudio PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}
  ${CMAKE_CURRENT_LIST_DIR}/.. # for our common lwipopts or any other standard includes, if required
)

# Add the standard library to the build
target_link_libraries(pico-pwmAudio pico_stdlib pico_audio pico_multicore)

# Add any user requested libraries
target_link_libraries(pico-pwmAudio
        hardware_dma
        hardware_pio
        hardware_interp
        )

pico_add_extra_outputs(pico-pwmAudio)

