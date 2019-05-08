##############################
#    Command-line options    #
##############################
set(sources options.cpp)
add_library(options ${sources})
target_include_directories(options PUBLIC ${PROJECT_SOURCE_DIR}/src)
