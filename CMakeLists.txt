cmake_minimum_required(VERSION 3.1.0)

project(emptyproject)

set(CMAKE_CONFIGURATION_TYPES "Release" CACHE STRING "" FORCE)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)
# Create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)

# Find the QtWidgets library
find_package(Qt5Widgets CONFIG REQUIRED)

# Find the Qt library
find_package(Qt5Core REQUIRED)
find_package(Qt5Network REQUIRED)
find_package(Qt5PrintSupport REQUIRED)

set(CMAKE_CXX_FLAGS_COVERAGE "${CMAKE_CXX_FLAGS_RELEASE} -fprofile-arcs -ftest-coverage")
set_target_properties(Qt5::Core PROPERTIES MAP_IMPORTED_CONFIG_COVERAGE "RELEASE")

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

link_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib)

# Populate a CMake variable with the sources
set(SRCS
    mainwindow.ui
    mainwindow.cpp
    main.cpp
)

# Tell CMake to create the helloworld executable
add_executable(${PROJECT_NAME} ${SRCS})

# Use the Widgets module from Qt 5
target_link_libraries(${PROJECT_NAME} Qt5::Widgets Qt5::Network Qt5::PrintSupport)
