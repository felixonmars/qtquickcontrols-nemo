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

set(SRC calendarmodel.cpp
        plugin.cpp)

set(HEADERS calendarmodel.h)

add_library(nemouxmodels6 SHARED ${SRC} ${HEADERS})

target_link_libraries(nemouxmodels6 PUBLIC
        Qt6::Gui
        Qt6::Qml
        Qt6::Quick)

FindQtInstallQml()
install(TARGETS nemouxmodels6 DESTINATION ${QT_INSTALL_QML}/Nemo/UX/Models)
install(FILES qmldir DESTINATION ${QT_INSTALL_QML}/Nemo/UX/Models)
