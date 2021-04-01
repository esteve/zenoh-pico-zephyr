# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.13.1)
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(zenoh_app_intree)

set(ZENOH_PICO_SRC_PATH $ENV{ZENOH_PICO_SRC_PATH})

if("${ZENOH_PICO_SRC_PATH}" STREQUAL "")
  message(FATAL_ERROR
    "Please set ZENOH_PICO_SRC_PATH environment variable to where your copy of the zenoh-pico repository is")
endif()

target_sources(app PRIVATE
  ${ZENOH_PICO_SRC_PATH}/src/codec.c
  ${ZENOH_PICO_SRC_PATH}/src/collection.c
  ${ZENOH_PICO_SRC_PATH}/src/iobuf.c
  ${ZENOH_PICO_SRC_PATH}/src/utils.c
  ${ZENOH_PICO_SRC_PATH}/src/compat/strdup.c
  ${ZENOH_PICO_SRC_PATH}/src/net/codec.c
  ${ZENOH_PICO_SRC_PATH}/src/net/internal.c
  ${ZENOH_PICO_SRC_PATH}/src/net/lease_task.c
  ${ZENOH_PICO_SRC_PATH}/src/net/msgcodec.c
  ${ZENOH_PICO_SRC_PATH}/src/net/property.c
  ${ZENOH_PICO_SRC_PATH}/src/net/read_task.c
  ${ZENOH_PICO_SRC_PATH}/src/net/rname.c
  ${ZENOH_PICO_SRC_PATH}/src/net/session.c
  ${ZENOH_PICO_SRC_PATH}/src/net/zephyr/network.c
  ${ZENOH_PICO_SRC_PATH}/src/net/zephyr/system.c
  src/main.c)
target_include_directories(app PRIVATE ${ZENOH_PICO_SRC_PATH}/include/)
target_compile_definitions(app PRIVATE -DZENOH_ZEPHYR -DZENOH_NEEDS_STRDUP)
