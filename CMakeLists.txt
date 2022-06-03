project(cmake-git-version-tracking)

# Define the two required variables before including
# the source code for watching a git repository.
set(PRE_CONFIGURE_FILE "git.cc.in")
set(POST_CONFIGURE_FILE "${CMAKE_CURRENT_BINARY_DIR}/git.cc")
include(git_watcher.cmake)

set(HEADERS
    include/cmake-git-version-tracking/git.h
)

# Create a library out of the compiled post-configure file.
add_library(${PROJECT_NAME} STATIC ${POST_CONFIGURE_FILE} ${HEADERS})
add_dependencies(${PROJECT_NAME} check_git)

target_include_directories(${PROJECT_NAME}
    PUBLIC include
    PRIVATE .                 # "dot" is redundant, because local headers are always available in C/C++.
)

