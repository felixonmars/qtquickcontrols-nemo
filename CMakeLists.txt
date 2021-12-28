cmake_minimum_required(VERSION 3.6.0)

project(nemo-qml-components
        VERSION 6.0
        DESCRIPTION "Nemo QML components")

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

option(BUILD_EXAMPLES "Build the example projects" OFF)

include(FindPkgConfig)
include(FeatureSummary)
include(GNUInstallDirs)

set(QT_MIN_VERSION "6.2.0")
find_package(Qt6 COMPONENTS Gui Qml Quick REQUIRED)

find_package(PkgConfig)
pkg_check_modules(MLITE5 mlite5 IMPORTED_TARGET)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "/usr" CACHE PATH "..." FORCE)
endif()

add_subdirectory(src)

if(BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)

