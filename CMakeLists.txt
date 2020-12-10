cmake_minimum_required(VERSION 3.9)

project(PRO)

set(CMAKE_CXX_STANDARD 17)            
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_INCLUDE_CURRENT_DIR YES)
set(CMAKE_AUTOMOC ON)

#find_package(Leptonica CONFIG REQUIRED)

find_package(SFML REQUIRED COMPONENTS system window graphics audio)

find_package(Qt5Gui CONFIG REQUIRED)

find_package(Qt5Widgets CONFIG REQUIRED)

#find_package(Tesseract CONFIG REQUIRED)

find_library(Tesseract libtesseract
    PATHS
    /usr/lib
    /usr/local/lib
    /usr/bin/tesseract
    /usr/lib/x86_64-linux-gnu
    /usr/lib/x86_64-linux-gnu/
    /usr/bin/install
    /usr/local/Cellar/tesseract/lib
    /usr/share/tesseract)


add_executable(main
${CMAKE_CURRENT_SOURCE_DIR}/source/main.cpp
${CMAKE_CURRENT_SOURCE_DIR}/source/ui.cpp
${CMAKE_CURRENT_SOURCE_DIR}/source/drawer.cpp)


target_include_directories(main
PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

include_directories(${Tesseract_INCLUDE_DIRS})
include_directories(${Leptonica_INCLUDE_DIRS})
include_directories(${Qt5Gui_INCLUDE_DIRS})
include_directories(${Qt5Widgets_INCLUDE_DIRS})
include_directories(sfml-system sfml-window sfml-graphics sfml-audio)


#set_target_properties(main PROPERTIES AUTOMOC TRUE)

target_link_libraries(main PRIVATE ${Leptonica_LIBRARIES})

#target_link_libraries(main PRIVATE libtesseract)

target_link_libraries(main PRIVATE sfml-system sfml-window sfml-graphics sfml-audio)

target_link_libraries(main PRIVATE ${Qt5Gui_LIBRARIES})

target_link_libraries(main PRIVATE ${Qt5Widgets_LIBRARIES})

##target_link_libraries(main PRIVATE llept PRIVATE libtesseract PRIVATE )


