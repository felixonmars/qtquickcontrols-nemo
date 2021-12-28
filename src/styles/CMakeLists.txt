### Sets QT_INSTALL_QML to the directory where QML Plugins should be installed
function(FindQtInstallQml)
    find_program(QMAKE NAMES qmake-qt6 qmake6)
    if(NOT QMAKE)
    message(FATAL_ERROR "qmake not found")
    endif()
    execute_process(
        COMMAND ${QMAKE} -query QT_INSTALL_QML
        OUTPUT_VARIABLE PROC_RESULT
        OUTPUT_STRIP_TRAILING_WHITESPACE
    )
    set(QT_INSTALL_QML ${PROC_RESULT} PARENT_SCOPE)
endfunction()

set(SRC qquicknemostyleextensionplugin.cpp)

set(HEADERS qquicknemostyleextensionplugin.h)

add_library(nemostyleplugin6 SHARED ${SRC} ${HEADERS})

target_link_libraries(nemostyleplugin6 PUBLIC
        Qt6::Gui
        Qt6::Qml
        Qt6::Quick)

FindQtInstallQml()
install(TARGETS nemostyleplugin6 DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Styles/Nemo)
install(DIRECTORY qml DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Styles/Nemo)
install(DIRECTORY images DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Styles/Nemo)
install(DIRECTORY themes DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Styles/Nemo)
