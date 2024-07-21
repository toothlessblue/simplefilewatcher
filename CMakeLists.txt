cmake_minimum_required(VERSION 3.29.4)

project(
    FileWatcher 
)

add_library(FileWatcher SHARED
    source/FileWatcher.cpp
    source/FileWatcherLinux.cpp
    source/FileWatcherOSX.cpp
    source/FileWatcherWin32.cpp
) 

set_target_properties(FileWatcher PROPERTIES VERSION 1.0.0)
set_target_properties(FileWatcher PROPERTIES PUBLIC_HEADER include/FileWatcher/FileWatcher.h)

target_include_directories(FileWatcher PRIVATE include)
target_include_directories(FileWatcher PRIVATE source)

include(GNUInstallDirs)

install(
    TARGETS FileWatcher
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

configure_file(FileWatcher.pc.in FileWatcher.pc @ONLY)

install(FILES ${CMAKE_BINARY_DIR}/FileWatcher.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)

