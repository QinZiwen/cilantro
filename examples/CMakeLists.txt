if(Pangolin_FOUND)
    file(GLOB example_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../examples/*.cpp)
    foreach(example_file ${example_files})
        get_filename_component(example_name ${example_file} NAME_WE)
        add_executable(${example_name} ${example_file})
        target_link_libraries(${example_name} ${PROJECT_NAME} ${Pangolin_LIBRARIES})
        if (ENABLE_NATIVE_BUILD_OPTIMIZATIONS)
            target_compile_options(${example_name} PUBLIC -O3 -march=native -mtune=native)
        else()
            target_compile_options(${example_name} PUBLIC -O3)
        endif()
    endforeach(example_file ${example_files})
endif()
