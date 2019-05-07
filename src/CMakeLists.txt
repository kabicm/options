##############################
#    Command-line options    #
##############################
if (NOT TARGET options)
    set(sources options.cpp)
    add_library(options SHARED ${sources})
endif()
