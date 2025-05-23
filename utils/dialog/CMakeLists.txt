cmake_minimum_required(VERSION 3.16)

project(hyprland-dialog VERSION ${VER} LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.5 REQUIRED COMPONENTS Widgets Quick QuickControls2 WaylandClient)
find_package(PkgConfig REQUIRED)

pkg_check_modules(hyprutils REQUIRED IMPORTED_TARGET hyprutils)

qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable(hyprland-dialog
    main.cpp
    Dialog.cpp
)

qt_add_qml_module(hyprland-dialog
    URI org.hyprland.dialog
    VERSION 1.0
    QML_FILES main.qml
)

target_link_libraries(hyprland-dialog PRIVATE
    Qt6::Widgets Qt6::QuickControls2 Qt6::WaylandClientPrivate PkgConfig::hyprutils
)


include(GNUInstallDirs)
install(TARGETS hyprland-dialog
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
