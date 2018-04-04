#����������С�汾Ϊ 2.8.11
cmake_minimum_required(VERSION 2.8.11)

#���ù�����
project(Chess)

#�����Զ�����moc�ļ�
set(CMAKE_AUTOMOC ON)

find_path(QT_DIR QT_DIR-NOTFOUND)

if(QT_DIR STREQUAL "QT_DIR-NOTFOUND")
    message(FATAL_ERROR "Can't find QT_DIR")
endif()


#������
#SET(CMAKE_MODULE_PATH ${QT_DIR}/lib/cmake/)

#����,�������find_package( Qt5Widgets NO_SYSTEM_ENVIRONMENT_PATH)
#set (CMAKE_PREFIX_PATH ${QT_DIR}/lib/cmake/)

#������
#set(CMAKE_FIND_ROOT_PATH ${QT_DIR}/lib/cmake)
#���������Qt���ļ�
#����,ֱ�Ӽ�PATHS, ������NO_SYSTEM_ENVIRONMENT_PATH
#find_package(Qt5Widgets PATHS ${QT_DIR}/lib/cmake/ NO_SYSTEM_ENVIRONMENT_PATH)
find_package(Qt5Widgets PATHS ${QT_DIR}/lib/cmake/ NO_SYSTEM_ENVIRONMENT_PATH)
find_package(Qt5Core PATHS ${QT_DIR}/lib/cmake/ NO_SYSTEM_ENVIRONMENT_PATH)
find_package(Qt5Gui PATHS ${QT_DIR}/lib/cmake/ NO_SYSTEM_ENVIRONMENT_PATH)
find_package(Qt5Network PATHS ${QT_DIR}/lib/cmake/ NO_SYSTEM_ENVIRONMENT_PATH)

#���ð�����ǰĿ¼
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(HEAD_FILES
	aimode.h
	board.h
	chessman.h
	compconfig.h
	dockctrlpanel.h
	mainwindow.h
	netclient.h
	rule.h
	selectdialog.h
	sets.h
	stacked.h
	stackedpage.h
)

set(SRC_FILES
	aimode.cpp
	board.cpp
	#chessman.cpp
	controlpanel.cpp
	dockctrlpanel.cpp
	main.cpp
	mainwindow.cpp
	netclient.cpp
	rule.cpp
	selectdialog.cpp
	sets.cpp
	stacked.cpp
	stackedpage.cpp
)

set(UI_FILES
	rule.ui
)

set(RCC_FILES
	board.qrc
	chessman.qrc
	chessman1.qrc
	chessman2.qrc
	icon.qrc
	#imgaes.qrc
	#one.qrc
)
#ͨ��.ui�ļ����ɶ�Ӧ���ļ�
qt5_wrap_ui(WRAP_UI ${UI_FILES})

#���ɵ�moc_xxx.cxx�ļ�
qt5_wrap_cpp(WRAP_CPP ${HEAD_FILES})

#������Դ
qt5_add_resources(ADD_RCCS ${RCC_FILES})

#��֯�ļ��ṹ
source_group("Header Files" FILES ${HEAD_FILES})
source_group("Source Files" FILES ${SRC_FILES})
source_group("Form Files" FILES ${UI_FILES}) 
source_group("Resource Files" FILES ${RCC_FILES})
source_group("Generated Files" FILES ${WRAP_UI} ${WRAP_CPP} ${ADD_RCCS})

MESSAGE(STATUS "This is PROJECT_SOURCE_DIR dir " ${PROJECT_SOURCE_DIR})
MESSAGE(STATUS "This is CMAKE_CURRENT_BINARY_DIR dir " ${CMAKE_CURRENT_BINARY_DIR})

message(STATUS "add  " ${ADD_RCCS})
message(STATUS "ui " ${WRAP_UI})
message(STATUS "cpp " ${WRAP_CPP})

include_directories(
	${PROJECT_SOURCE_DIR}
	${CMAKE_CURRENT_BINARY_DIR}
)
#add_executable����Ҫ���ļ�	
set(DPD_FILES
	${HEAD_FILES}
	${SRC_FILES}
	${WRAP_UI}
	#${WRAP_CPP}
	${ADD_RCCS}
)

#��������
add_executable(ChinessChess ${DPD_FILES})

#����Qt5������
target_link_libraries(ChinessChess
	Qt5::Widgets
	Qt5::Core
	Qt5::Gui
	Qt5::Network	
)
