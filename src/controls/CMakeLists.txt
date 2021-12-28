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

set(SRC editfilter.cpp
    nemofocussingleton.cpp
    nemopage.cpp
    qquickfilteringmousearea.cpp
    sizing.cpp
    hacks.cpp
    nemoimageprovider.cpp
    nemowindow.cpp
    qquicknemocontrolsextensionplugin.cpp
    ringindicator.cpp
    theme.cpp
    themedaemon/mlocalthemedaemonclient.cpp
    themedaemon/mabstractthemedaemonclient.cpp)

set(HEADERS editfilter.h
    nemofocussingleton.h
    nemopage.h
    qquickfilteringmousearea.h
    ringindicator.h
    theme.h
    hacks.h
    nemoimageprovider.h
    nemowindow.h
    qquicknemocontrolsextensionplugin.h
    sizing.h
    themedaemon/mlocalthemedaemonclient.h
    themedaemon/mabstractthemedaemonclient.h)

qt_add_qml_module(nemocontrolsplugin6
    URI "QtQuick.Controls.Nemo"
    VERSION 2.0
    PLUGIN_TARGET nemocontrolsplugin6
    CLASS_NAME QQuickNemoControlsExtensionPlugin
    QML_FILES
        qml/ActionButton.qml
        qml/ApplicationWindow.qml
        qml/Button.qml
        qml/ButtonRow.qml
        qml/Checkbox.qml
        qml/DatePicker.qml
        qml/ErrorStackPage.qml
        qml/GlacierRollerItem.qml
        qml/GlacierRoller.qml
        qml/Header.qml
        qml/HeaderToolsLayout.qml
        qml/IconButton.qml
        qml/InverseMouseArea.qml
        qml/Label.qml
        qml/ListViewItemWithActions.qml
        qml/ListView.qml
        qml/NemoIcon.qml
        qml/Page.qml
        qml/ProgressBar.qml
        qml/ScrollDecorator.qml
        qml/Slider.qml
        qml/Spinner.qml
        qml/TextField.qml
        qml/TimePicker.qml
        qml/ToolButton.qml
        qml/Wallpaper.qml
    SOURCES ${SRC} ${HEADERS})

target_link_libraries(nemocontrolsplugin6 PUBLIC
    Qt6::Gui
    Qt6::Qml
    Qt6::Quick
    PkgConfig::MLITE5)

FindQtInstallQml()
install(TARGETS nemocontrolsplugin6 DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Nemo)
install(DIRECTORY qml DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Nemo)
install(DIRECTORY images DESTINATION ${QT_INSTALL_QML}/QtQuick/Controls/Nemo)
