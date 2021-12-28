set(SRC main.cpp)

add_executable(glacier6-sizeview ${SRC} ${RESOURCES})

find_package(PkgConfig)
pkg_check_modules(GLACIER6 REQUIRED glacierapp-qt6 IMPORTED_TARGET)

target_link_libraries(glacier6-sizeview
    Qt6::Qml
    Qt6::Quick
    PkgConfig::GLACIER6)


install(TARGETS glacier6-sizeview RUNTIME
    DESTINATION ${CMAKE_INSTALL_BINDIR})

install(FILES glacier6-sizeview.qml
        DESTINATION ${CMAKE_INSTALL_DATADIR}/glacier6-sizeview/qml)
