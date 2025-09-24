# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

add_library(mbed-caju INTERFACE)

target_sources(mbed-caju
    INTERFACE
        PeripheralPins.c
)

target_include_directories(mbed-caju
    INTERFACE
        .
)

target_link_libraries(mbed-caju INTERFACE mbed-stm32h743xi)
