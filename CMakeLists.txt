cmake_minimum_required(VERSION 3.13)

set(PROJECT_NAME Herring54)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Pico SDK
include(extern/pico-sdk/pico_sdk_init.cmake)

project(${PROJECT_NAME} C CXX ASM)

pico_sdk_init()

# FreeRTOS Kernel
inclde(extern/FreeRTOS-Kernel/portable/ThirdParty/GCC/RP2040/FreeRTOS_Kernel_import.cmake)

# u8g2 (graphics)
add_library(u8g2 STATIC
    extern/u8g2/csrc/u8g2_bitmap.c
    extern/u8g2/csrc/u8g2_box.c
    extern/u8g2/csrc/u8g2_buffer.c
    extern/u8g2/csrc/u8g2_circle.c
    extern/u8g2/csrc/u8g2_cleardisplay.c
    extern/u8g2/csrc/u8g2_d_memory.c
    extern/u8g2/csrc/u8g2_d_setup.c
    extern/u8g2/csrc/u8g2_font.c
    extern/u8g2/csrc/u8g2_fonts.c
    extern/u8g2/csrc/u8g2_hvline.c
    extern/u8g2/csrc/u8g2_input_value.c
    extern/u8g2/csrc/u8g2_intersection.c
    extern/u8g2/csrc/u8g2_kerning.c
    extern/u8g2/csrc/u8g2_line.c
    extern/u8g2/csrc/u8g2_ll_hvline.c
    extern/u8g2/csrc/u8g2_message.c
    extern/u8g2/csrc/u8g2_polygon.c
    extern/u8g2/csrc/u8g2_selection_list.c
    extern/u8g2/csrc/u8g2_setup.c
    extern/u8g2/csrc/u8x8_8x8.c
    extern/u8g2/csrc/u8x8_byte.c
    extern/u8g2/csrc/u8x8_cad.c
    extern/u8g2/csrc/u8x8_d_ssd1306_128x32.c  # Updated for 128x32 SSD1306
    extern/u8g2/csrc/u8x8_debounce.c
    extern/u8g2/csrc/u8x8_display.c
    extern/u8g2/csrc/u8x8_fonts.c
    extern/u8g2/csrc/u8x8_gpio.c
    extern/u8g2/csrc/u8x8_input_value.c
    extern/u8g2/csrc/u8x8_message.c
    extern/u8g2/csrc/u8x8_selection_list.c
    extern/u8g2/csrc/u8x8_setup.c
    extern/u8g2/csrc/u8x8_string.c
    extern/u8g2/csrc/u8x8_u8toa.c
    extern/u8g2/csrc/u8x8_u16toa.c
)

target_include_directories(u8g2 PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/extern/u8g2/csrc
)

# Link u8g2 libraries
target_link_libraries(u8g2
    pico_stdlib
    hardware_i2c
)

# Add binaries
add_executable(${PROJECT_NAME}
    src/main.cpp
)

# Link main libraries
target_link_libraries(${PROJECT_NAME}
    pico_stdlib
    pico_multicore
    hardware_pio
    hardware_uart
    hardware_i2c
    FreeRTOS-Kernel-Heap4
    u8g2
    tinyusb_device
    tinyusb_board
)

# Disable stdio on USB and UART as USB will conflict, and the UART pins are used
# by the matrix.
pico_enable_stdio_usb(${PROJECT_NAME} 0)
pico_enable_stdio_uart(${PROJECT_NAME} 0)

pico_add_extra_outputs(${PROJECT_NAME})
