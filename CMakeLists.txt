cmake_minimum_required(VERSION 3.10)
project(mh3u-se-gui VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5 REQUIRED COMPONENTS Core Widgets Gui)

# Find all source files
file(GLOB_RECURSE ALL_SOURCES "app/*.cpp")
list(FILTER ALL_SOURCES EXCLUDE REGEX "app/MH3U Save Editor/MH3U Save Editor/main.cpp")
file(GLOB_RECURSE ALL_HEADERS "app/*.hpp" "app/*.h")

# Create an app bundle (MACOSX_BUNDLE)
add_executable(${PROJECT_NAME} MACOSX_BUNDLE ${ALL_SOURCES} ${ALL_HEADERS})

target_link_libraries(${PROJECT_NAME} Qt5::Core Qt5::Widgets Qt5::Gui)

target_include_directories(${PROJECT_NAME} PRIVATE
    "app/MH3U Save Editor GUI/MH3U Save Editor GUI"
    "app/MH3U Save Editor/MH3U Save Editor"
)

# On macOS, copy the data folder into the bundle's Resources
if(APPLE)
    set_target_properties(${PROJECT_NAME} PROPERTIES
        MACOSX_BUNDLE_BUNDLE_NAME "MH3U Save Editor"
        MACOSX_BUNDLE_BUNDLE_VERSION "1.0"
        MACOSX_BUNDLE_SHORT_VERSION_STRING "1.0"
    )
    add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${CMAKE_CURRENT_SOURCE_DIR}/data"
        "$<TARGET_FILE_DIR:${PROJECT_NAME}>/../Resources/data"
    COMMENT "Copying data folder to app bundle Resources"
)
endif()
