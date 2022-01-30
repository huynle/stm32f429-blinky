# Template CMakeLists.txt configuration for STM32 MCUS
cmake_minimum_required(VERSION 3.12)
# ##############################################################################
# Edit your MCU information up to the next border
project(stm32-blinky)

set(PROJECT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Blinky)

set(MCU_FAMILY STM32F4xx)
set(MCU_MODEL STM32F429xx)
set(CPU_PARAMETERS
    -mcpu=cortex-m4
    -mthumb
    -mfpu=fpv4-sp-d16
    -mfloat-abi=hard)

set(STARTUP_SCRIPT ${CMAKE_CURRENT_SOURCE_DIR}/CubeMX/startup_stm32f429xx.s)
set(MCU_LINKER_SCRIPT ${CMAKE_CURRENT_SOURCE_DIR}/CubeMX/STM32F429ZITx_FLASH.ld)
# ##############################################################################
#
set(EXECUTABLE ${CMAKE_PROJECT_NAME})
enable_language(C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)

# Headers
set(CUBEMX_INCLUDE_DIRECTORIES
    ${CMAKE_CURRENT_SOURCE_DIR}/Core/Inc
    ${CMAKE_CURRENT_SOURCE_DIR}/USB_HOST/App
    ${CMAKE_CURRENT_SOURCE_DIR}/USB_HOST/Target
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/${MCU_FAMILY}_HAL_Driver/Inc
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/${MCU_FAMILY}_HAL_Driver/Inc/Legacy
    ${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/Third_Party/FreeRTOS/Source/include
    ${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS
    ${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F
    ${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/ST/STM32_USB_Host_Library/Core/Inc
    ${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/ST/STM32_USB_Host_Library/Class/CDC/Inc
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/CMSIS/Device/ST/${MCU_FAMILY}/Include
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/CMSIS/Include
    )

set(PROJECT_INCLUDE_DIRECTORIES
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_DIR}
    )

  # Sources
  file(GLOB_RECURSE STM32CUBEMX_SOURCES
    # ${CMAKE_CURRENT_SOURCE_DIR}/Core/*.c
    # ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/*.c
    # ${CMAKE_CURRENT_SOURCE_DIR}/USB_HOST/*.c
    # ${CMAKE_CURRENT_SOURCE_DIR}/Middlewares/*.c
    ./Core/Src/main.c
    ./Core/Src/freertos.c
    ./Core/Src/stm32f4xx_it.c
    ./Core/Src/stm32f4xx_hal_msp.c
    ./Core/Src/stm32f4xx_hal_timebase_tim.c
    ./USB_HOST/Target/usbh_conf.c
    ./USB_HOST/Target/usbh_platform.c
    ./USB_HOST/App/usb_host.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_hcd.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_usb.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rcc.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_rcc_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_flash_ramfunc.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_gpio.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dma_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dma.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_pwr.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_pwr_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_cortex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_exti.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_crc.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dma2d.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_ll_fmc.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_sdram.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_i2c.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_i2c_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_ltdc.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_ltdc_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_dsi.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_spi.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_tim.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_tim_ex.c
    ./Drivers/STM32F4xx_HAL_Driver/Src/stm32f4xx_hal_uart.c
    ./Core/Src/system_stm32f4xx.c
    ./Middlewares/Third_Party/FreeRTOS/Source/croutine.c
    ./Middlewares/Third_Party/FreeRTOS/Source/event_groups.c
    ./Middlewares/Third_Party/FreeRTOS/Source/list.c
    ./Middlewares/Third_Party/FreeRTOS/Source/queue.c
    ./Middlewares/Third_Party/FreeRTOS/Source/stream_buffer.c
    ./Middlewares/Third_Party/FreeRTOS/Source/tasks.c
    ./Middlewares/Third_Party/FreeRTOS/Source/timers.c
    ./Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS/cmsis_os.c
    ./Middlewares/Third_Party/FreeRTOS/Source/portable/MemMang/heap_4.c
    ./Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F/port.c
    ./Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_core.c
    ./Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_ctlreq.c
    ./Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_ioreq.c
    ./Middlewares/ST/STM32_USB_Host_Library/Core/Src/usbh_pipes.c
    ./Middlewares/ST/STM32_USB_Host_Library/Class/CDC/Src/usbh_cdc.c
    )

file(GLOB_RECURSE PROJECT_SOURCES FOLLOW_SYMLINKS
    ${PROJECT_DIR}/*.cpp
    ${PROJECT_DIR}/*.c
    )

# Executable files
add_executable(${EXECUTABLE}
    ${STM32CUBEMX_SOURCES} 
    ${PROJECT_SOURCES}
    ${STARTUP_SCRIPT})

# Embedded macros(defines)
target_compile_definitions(${EXECUTABLE} PRIVATE
    ${MCU_MODEL}
    USE_HAL_DRIVER)

# Add header directories (AFTER add_executable !!)
target_include_directories(${EXECUTABLE} PRIVATE
    ${CUBEMX_INCLUDE_DIRECTORIES}
    ${PROJECT_INCLUDE_DIRECTORIES}
    )

# Compiler and linker options
target_compile_options(${EXECUTABLE} PRIVATE
    ${CPU_PARAMETERS}
    -Wall
    -Wextra
    -Wpedantic
    -Wno-unused-parameter
    $<$<COMPILE_LANGUAGE:CXX>:
        -Wno-volatile
        -Wold-style-cast
        -Wuseless-cast
        -Wsuggest-override>
    $<$<CONFIG:Debug>:-Og -g3 -ggdb>
    $<$<CONFIG:Release>:-Og -g0>)

target_link_options(${EXECUTABLE} PRIVATE
    -T${MCU_LINKER_SCRIPT}
    ${CPU_PARAMETERS}
    -Wl,-Map=${CMAKE_PROJECT_NAME}.map
    --specs=nosys.specs
    -Wl,--start-group
    -lc
    -lm
    -lstdc++
    -lsupc++
    -Wl,--end-group
    -Wl,--print-memory-usage)

add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
    COMMAND ${CMAKE_SIZE} $<TARGET_FILE:${EXECUTABLE}>)

add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
    COMMAND ${CMAKE_OBJCOPY} -O ihex $<TARGET_FILE:${EXECUTABLE}>
    ${EXECUTABLE}.hex
    COMMAND ${CMAKE_OBJCOPY} -O binary $<TARGET_FILE:${EXECUTABLE}>
    ${EXECUTABLE}.bin)
