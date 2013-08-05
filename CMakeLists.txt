cmake_minimum_required(VERSION 2.6)
project(gnucap)

# Set project version information.
set(VERSION "2013-04-23")

# Set configuration options.
option(DOCS "Build and install documentation" OFF)
option(READLINE "Support command-line editing" ON)
option(TEST "Enable regression testing" OFF)

# Set standard installation paths.
include(GNUInstallDirs)

# Use Git and the current repository to determine revision information.
find_package(Git)

if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git/HEAD")
    execute_process(COMMAND "git" "rev-parse" "HEAD"
        OUTPUT_VARIABLE GIT_COMMIT)
    string(STRIP "${GIT_COMMIT}" GIT_COMMIT)
    execute_process(COMMAND "git" "describe"
        OUTPUT_VARIABLE GIT_TAG ERROR_QUIET)
    string(STRIP "${GIT_TAG}" GIT_TAG)
    execute_process(COMMAND "git" "rev-parse" "--abbrev-ref" "HEAD"
        OUTPUT_VARIABLE GIT_BRANCH)
    string(STRIP "${GIT_BRANCH}" GIT_BRANCH)
endif()

# Enable regression testing (if enabled).
if(TEST)
    enable_testing()
endif()

# Check for command-line editing libraries (readline and termcap).
include(CheckLibraryExists)

if(READLINE)
    check_library_exists(readline readline "" HAVE_LIBREADLINE)
    check_library_exists(termcap tgetent "" HAVE_LIBTERMCAP)
    set(READLINE_LIBS "readline")
endif()

# Check for dynamic library support (dlopen).
include(cmake/FindDL.cmake)

if(DL_FOUND)
    set(HAVE_DLFCN_H true)
    set(HAVE_LIBDL true)
endif()

# TODO: Check for local modelgen if cross-compiling.

# Write configuration to header file.
configure_file(
    "${PROJECT_SOURCE_DIR}/cmake/config.h.in"
    "${PROJECT_BINARY_DIR}/config.h"
    )

# Tell the compiler where to find the header files.
include_directories(${PROJECT_BINARY_DIR})
include_directories(include)

# Build in subdirectories.
add_subdirectory(apps)
add_subdirectory(lib)
add_subdirectory(main)
add_subdirectory(modelgen)

# Build an installation package.
include(InstallRequiredSystemLibraries)
set(CPACK_GENERATOR "TGZ")
set(CPACK_PACKAGE_VERSION "${VERSION}")
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/COPYING")
include(CPack)
