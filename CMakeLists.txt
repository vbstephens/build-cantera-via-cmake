################### PREAMBLE ###############################

cmake_minimum_required(VERSION 3.15)

project(cantera-via-cmake VERSION 0.1.0
        LANGUAGES CXX)

################### PROJECT SETUP ##########################

include(FetchContent)
include(ExternalProject)
include(GNUInstallDirs)

# ---- set C++ language standard ----
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED YES)
set(CMAKE_CXX_EXTENSIONS NO)

# ---- module path ----
list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)      # tells find_package() where to look for Find[pkg].cmake files

# ---- installation location ----
set(CMAKE_INSTALL_PREFIX "${PROJECT_SOURCE_DIR}")

# ---- build options ----
option(PREFIX_SYSTEM_CANTERA    "Use system-wide Cantera installation"  OFF)

################### DEPENDENCIES #####################

add_subdirectory(ext)

################### MAIN PROJECT TARGETS #####################

add_subdirectory(src)