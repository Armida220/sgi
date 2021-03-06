INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})

if(SGI_USE_FFMPEG AND FFMPEG_FOUND)
    include_directories(${FFMPEG_INCLUDE_DIR})
    LIST(APPEND TARGET_DEFINITIONS SGI_USE_FFMPEG)
endif()

SET(CMAKE_SHARED_MODULE_PREFIX ${SGI_PLUGIN_PREFIX})

SET(LIB_NAME sgi)


SET(SGI_VERSION ${SGI_VERSION_MAJOR}.${SGI_VERSION_MINOR}.${SGI_VERSION_PATCH})

FAST_SET_TARGET_AND_PRODUCT_VERSION(SGI)
SET(TARGET_NO_TRANSLATION 1)
SET(TARGET_NO_IMPORT_LIB)

if(WIN32)
    set(_lib_prefix "")
else()
    set(_lib_prefix "lib")
endif()
SET(SGI_LIBRARY_NAME_DEBUG "${_lib_prefix}${LIB_NAME}${CMAKE_DEBUG_POSTFIX}${CMAKE_SHARED_MODULE_SUFFIX}")
SET(SGI_LIBRARY_NAME_RELEASE "${_lib_prefix}${LIB_NAME}${CMAKE_RELEASE_POSTFIX}${CMAKE_SHARED_MODULE_SUFFIX}")
SET(SGI_LIBRARY_NAME_RELWITHDEBINFO "${_lib_prefix}${LIB_NAME}${CMAKE_RELWITHDEBINFO_POSTFIX}${CMAKE_SHARED_MODULE_SUFFIX}")
SET(SGI_LIBRARY_NAME_MINSIZEREL "${_lib_prefix}${LIB_NAME}${CMAKE_MINSIZEREL_POSTFIX}${CMAKE_SHARED_MODULE_SUFFIX}")

SET(SGI_LIBRARY_POSTFIX_DEBUG "${CMAKE_DEBUG_POSTFIX}")
SET(SGI_LIBRARY_POSTFIX_RELEASE "${CMAKE_RELEASE_POSTFIX}")
SET(SGI_LIBRARY_POSTFIX_RELWITHDEBINFO "${CMAKE_RELWITHDEBINFO_POSTFIX}")
SET(SGI_LIBRARY_POSTFIX_MINSIZEREL "${CMAKE_MINSIZEREL_POSTFIX}")

SET(SGI_LIBRARY_SHARED_MODULE_SUFFIX "${CMAKE_SHARED_MODULE_SUFFIX}")

fast_configure_file(${CMAKE_CURRENT_SOURCE_DIR}/../../Export.in ${SGI_INCLUDE_DIR}/sgi/Export)

SET(TARGET_H
	# precompiled header
	stdafx.h
	SGIPlugin.h
	entrypoint.h
	sgi_internal.h
	dxt.h
	swscale.h
	colorconversion.h
)

LIST(APPEND TARGET_H
    ${SGI_INCLUDE_DIR}/sgi/Export
    ${SGI_INCLUDE_DIR}/sgi/AutoLoadOsg
    ${SGI_INCLUDE_DIR}/sgi/AutoLoadQt
    ${SGI_INCLUDE_DIR}/sgi/ContextMenu
    ${SGI_INCLUDE_DIR}/sgi/ContextMenuQt
    ${SGI_INCLUDE_DIR}/sgi/GenerateItem
    ${SGI_INCLUDE_DIR}/sgi/ImagePreviewDialog
    ${SGI_INCLUDE_DIR}/sgi/LibraryInfo
    ${SGI_INCLUDE_DIR}/sgi/ObjectInfo
    ${SGI_INCLUDE_DIR}/sgi/ObjectLoggerDialog
    ${SGI_INCLUDE_DIR}/sgi/ReferencedPicker
    ${SGI_INCLUDE_DIR}/sgi/SceneGraphDialog
    ${SGI_INCLUDE_DIR}/sgi/SGIItemInternal
    ${SGI_INCLUDE_DIR}/sgi/Shutdown
    ${SGI_INCLUDE_DIR}/sgi/WritePrettyHTML

    ${SGI_INCLUDE_DIR}/sgi/helpers/html
	${SGI_INCLUDE_DIR}/sgi/helpers/osg
    ${SGI_INCLUDE_DIR}/sgi/helpers/osg_helper_nodes
    ${SGI_INCLUDE_DIR}/sgi/helpers/osg_statistics
    ${SGI_INCLUDE_DIR}/sgi/helpers/qt
    ${SGI_INCLUDE_DIR}/sgi/helpers/qt_widgets
    ${SGI_INCLUDE_DIR}/sgi/helpers/qt_widgetwindow
    ${SGI_INCLUDE_DIR}/sgi/helpers/rtti
    ${SGI_INCLUDE_DIR}/sgi/helpers/singleton
    ${SGI_INCLUDE_DIR}/sgi/helpers/string

	${SGI_INCLUDE_DIR}/sgi/details/type_list
	${SGI_INCLUDE_DIR}/sgi/details/functionImplBase

    ${SGI_INCLUDE_DIR}/sgi/plugins/fallback_support.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/log4cplus_support.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/osg_support.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/osgearth_support.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/qt_support.h

    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIItemInfo

    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemBase.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemFallback.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemLog4cplus.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemOsg.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemOsgEarth.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemQt.h

    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIItemBase.h
	${SGI_INCLUDE_DIR}/sgi/plugins/SGIImage.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIPluginImpl.h
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIPluginInterface.h

    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIDataItemBase.h

    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostItemGenerator
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGIHostSupport

    ${SGI_INCLUDE_DIR}/sgi/plugins/ContextMenu
    ${SGI_INCLUDE_DIR}/sgi/plugins/SceneGraphDialog
    ${SGI_INCLUDE_DIR}/sgi/plugins/ObjectLoggerDialog
    ${SGI_INCLUDE_DIR}/sgi/plugins/ImagePreviewDialog

	${SGI_INCLUDE_DIR}/sgi/plugins/Matrix
	${SGI_INCLUDE_DIR}/sgi/plugins/Quat
	${SGI_INCLUDE_DIR}/sgi/plugins/Vector

    ${SGI_INCLUDE_DIR}/sgi/plugins/SettingsDialogImpl
    ${SGI_INCLUDE_DIR}/sgi/plugins/SGISettingsDialogImpl
    ${SGI_INCLUDE_DIR}/sgi/plugins/WritePrettyHTMLImpl

	)

SET(TARGET_UI
	ObjectLoggerDialog.ui
	QTextDialog.ui
	DoubleInputDialog.ui
	QuatInputDialog.ui
	MatrixInputDialog.ui
    ImagePreviewDialog.ui
    )

SET(TARGET_MOC_H
	SceneGraphDialog.h
	ContextMenu.h
	ObjectLoggerDialog.h
	QtProxy.h
	QTextDialog.h
	DoubleInputDialog.h
	QuatInputDialog.h
	MatrixInputDialog.h
	ImagePreviewDialog.h
	ImageGLWidget.h
	ImageQtWidget.h
	ImageScrollArea.h
)

# CHECK-IT:
# add your source files here
SET(TARGET_SRC
	stdafx.cpp
	SceneGraphDialog.cpp
	ContextMenu.cpp
	ObjectLoggerDialog.cpp
	SGIPlugin.cpp
	entrypoint.cpp
	sgi_internal.cpp
	QtProxy.cpp
	QTextDialog.cpp
	DoubleInputDialog.cpp
	QuatInputDialog.cpp
	MatrixInputDialog.cpp
	ImagePreviewDialog.cpp
	ImageGLWidget.cpp
	ImageQtWidget.cpp
	ImageScrollArea.cpp
	dxt.cpp
	swscale.cpp
	colorconversion.cpp
)
set(_imagewidget_dir .)
set(TARGET_GLSL
    ImageGLWidget.vert.glsl
    ImageGLWidget.frag.glsl
    )

set(SHADERS_CPP "${CMAKE_CURRENT_BINARY_DIR}/AutoGenShaders.cpp")

SGI_CONFIGURE_SHADERS(
    ${_imagewidget_dir}/Shaders.cpp.in
    ${SHADERS_CPP}
    ${TARGET_GLSL} )

list(APPEND TARGET_SRC
    ${_imagewidget_dir}/ImageGLWidget.cpp
    )
list(APPEND TARGET_SRC_NO_PCH
    ${SHADERS_CPP}
)

SET(TARGET_LIBRARIES_VARS
    SGI_REF_LIBRARY
    SGI_PLUGIN_IMPL_LIBRARY
    SGI_QT_HELPER_LIBRARY
	OPENTHREADS_LIBRARY
)
LIST(APPEND TARGET_LIBRARIES_VARS
    QT_QTCORE_LIBRARY
    QT_QTGUI_LIBRARY
    )
IF ( Qt5Widgets_FOUND )
    # Add the include directories for the Qt 5 Widgets module to
    # the compile lines.
    include_directories(${Qt5Widgets_INCLUDE_DIRS})
    LIST(APPEND TARGET_LIBRARIES_VARS QT_QTWIDGETS_LIBRARY )
ENDIF()
if(NOT WIN32)
    LIST(APPEND TARGET_LIBRARIES_VARS
        dl
        )
endif()

if(FAST_SGI_CMAKE_SYSTEM)
    file(RELATIVE_PATH _qt_plugin_dir ${FAST_WORK_BIN_DIR} ${FAST_WORK_PLUGINS_DIR})
    add_definitions(-DSGI_QT_PLUGIN_SGI_DIR="/${_qt_plugin_dir}/sgi")
else()
    VAR_CONFIG(_postfix FAST_POSTFIX)
    add_definitions(-DSGI_QT_PLUGIN_SGI_DIR="/../plugins${_postfix}/sgi")
endif()

FAST_SHARED_LIBRARY(${LIB_NAME} NO_MOC_INCLUDE)

if(SGI_SWSCALE_USE_LIBRARY_POSTFIX)
    set(_swscale "${SGI_SWSCALE_LIBRARYNAME}$<$<CONFIG:Debug>:${CMAKE_DEBUG_POSTFIX}>$<$<CONFIG:Release>:${CMAKE_RELEASE_POSTFIX}>$<$<CONFIG:RelWithDebInfo>:${CMAKE_RELWITHDEBINFO_POSTFIX}>$<$<CONFIG:MinSizeRel>:${CMAKE_MINSIZEREL_POSTFIX}>")
else()
    set(_swscale "${SGI_SWSCALE_LIBRARYNAME}")
endif()

target_compile_definitions(${TARGET_DEFAULT_PREFIX}${LIB_NAME} PRIVATE
    SGI_LIBRARY
	SGI_SWSCALE_LIBRARYNAME="${_swscale}"
    SGI_PLUGIN_EXTENSION="${CMAKE_SHARED_MODULE_SUFFIX}"
    SGI_LIBRARY_POSTFIX="$<$<CONFIG:Debug>:${CMAKE_DEBUG_POSTFIX}>$<$<CONFIG:Release>:${CMAKE_RELEASE_POSTFIX}>$<$<CONFIG:RelWithDebInfo>:${CMAKE_RELWITHDEBINFO_POSTFIX}>$<$<CONFIG:MinSizeRel>:${CMAKE_MINSIZEREL_POSTFIX}>"
    )
