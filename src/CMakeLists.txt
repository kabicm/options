##############################
#    Command-line options    #
##############################
if (NOT TARGET options)
    set(sources options.cpp)
    add_library(options SHARED ${sources})
    target_include_directories(options PUBLIC ${PROJECT_SOURCE_DIR}/src)
endif()
