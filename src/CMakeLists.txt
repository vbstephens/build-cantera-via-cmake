#################### EXECUTABLE ##########################

# -------- executable targets --------
add_executable(cantera-via-cmake-example)

# -------- target properties --------
target_compile_features(cantera-via-cmake-example PUBLIC cxx_std_11)

# -------- src files --------
target_include_directories(cantera-via-cmake-example PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_sources(cantera-via-cmake-example PRIVATE test.cc)

# -------- dependencies --------
get_target_property(cantera_INCLUDE_DIR cantera-ext INTERFACE_INCLUDE_DIRECTORIES)  # tell CMake where to find cantera headers
list(APPEND sundials_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include/cantera/ext)
list(APPEND yaml-cpp_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include/cantera/ext)

target_include_directories(cantera-via-cmake-example PRIVATE ${Boost_INCLUDE_DIR} ${yaml-cpp_INCLUDE_DIR} ${sundials_INCLUDE_DIR} ${cantera_INCLUDE_DIR})

target_link_libraries(cantera-via-cmake-example PUBLIC cantera-ext)

############# INSTALLATION ################

include(GNUInstallDirs)

#---- allow odt to be used in other targets ----
target_include_directories(cantera-via-cmake-example
        INTERFACE
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
        "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
        )

install(TARGETS cantera-via-cmake-example
        RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY  DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE  DESTINATION ${CMAKE_INSTALL_LIBDIR}
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
        )