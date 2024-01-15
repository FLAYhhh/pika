set(CXXFLAGS "-DROCKSDB_PLATFORM_POSIX -DROCKSDB_LIB_IO_POSIX -DOS_LINUX -Wall -W -DDEBUG -g -O2 -D__XDEBUG__ -fPIC -Wno-unused-function -std=c++17")

set(SRC_DIR .)
aux_source_directory(${SRC_DIR} BASE_OBJS)

add_executable(redis-copy ${BASE_OBJS})

target_include_directories(redis-copy PRIVATE ${INSTALL_INCLUDEDIR})

target_link_libraries(redis-copy ${HIREDIS_LIBRARY})
set_target_properties(redis-copy PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}
    CMAKE_COMPILER_IS_GNUCXX TRUE
    COMPILE_FLAGS ${CXXFLAGS})
add_dependencies(redis-copy hiredis)