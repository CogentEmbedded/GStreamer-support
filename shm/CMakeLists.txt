cmake_minimum_required (VERSION 2.8)
project("shm")
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

install(TARGETS ${PROJECT_NAME} DESTINATION lib)
# Install common headers
INSTALL(FILES ${PROJECT_SOURCE_DIR}/shmpipe.h DESTINATION include)