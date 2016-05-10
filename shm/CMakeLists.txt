cmake_minimum_required (VERSION 2.8)
project("gstshm")
include(GNUInstallDirs)

# set version number
SET(GSTSHM_VERSION_MAJOR "1")
SET(GSTSHM_VERSION_MINOR "1")
SET(GSTSHM_VERSION_PATCH "0-ts")
SET(GSTSHM_VERSION "${GSTSHM_VERSION_MAJOR}.${GSTSHM_VERSION_MINOR}.${GSTSHM_VERSION_PATCH}")

set (PROJECT_INCLUDE_DIR ${PROJECT_SOURCE_DIR})
set (PROJECT_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

# search for additional CMake modules
SET(CMAKE_MODULE_PATH
        ${CMAKE_MODULE_PATH}
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake-modules"
)

# ...add sources
set(PRJ_SRC
    ${PROJECT_SOURCE_DIR}/shmalloc.c
    ${PROJECT_SOURCE_DIR}/shmpipe.c
)

include_directories(
    ${PROJECT_INCLUDE_DIR}
    ${GLIB_INCLUDE_DIRS}
    ${GSTREAMER_INCLUDE_DIR}
)

add_library(${PROJECT_NAME} SHARED ${PRJ_SRC})
target_link_libraries(${PROJECT_NAME}
    ${GSTREAMER_LIBRARIES}
    ${GLIB_GOBJECT_LIBRARIES}
    rt
)
set_target_properties(${PROJECT_NAME}
  PROPERTIES
    VERSION ${GSTSHM_VERSION}
    SOVERSION 2
)

message(STATUS "${CMAKE_INSTALL_LIBDIR}")

install(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_LIBDIR})
# Install common headers
INSTALL(FILES ${PROJECT_SOURCE_DIR}/shmpipe.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

add_subdirectory(packaging)

