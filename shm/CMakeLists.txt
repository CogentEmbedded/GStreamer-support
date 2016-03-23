cmake_minimum_required (VERSION 2.8)
project("gstshm")
include(GNUInstallDirs)

enable_testing()

set (PROJECT_INCLUDE_DIR ${PROJECT_SOURCE_DIR})
set (PROJECT_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

# ...add sources
set(PRJ_SRC
    ${PROJECT_SOURCE_DIR}/shmalloc.c
    ${PROJECT_SOURCE_DIR}/shmpipe.c
)

include_directories(
    ${PROJECT_INCLUDE_DIR}
)

add_library(${PROJECT_NAME} SHARED ${PRJ_SRC})
target_link_libraries(${PROJECT_NAME}
    rt
)
set_target_properties(${PROJECT_NAME}
  PROPERTIES
    VERSION 1.6.3
    SOVERSION 1
)

message(STATUS "${CMAKE_INSTALL_LIBDIR}")

install(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_LIBDIR})
# Install common headers
INSTALL(FILES ${PROJECT_SOURCE_DIR}/shmpipe.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

add_subdirectory(packaging)

