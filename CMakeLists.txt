cmake_minimum_required(VERSION 3.8)
cmake_policy(SET CMP0112 NEW) # Required by copy_folder_to_output()

project(SimpleGlimac)

# Set the folder where the executables are created
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin/${CMAKE_BUILD_TYPE})

# Include glimac
add_subdirectory(glimac)

# Create a target for each TP
function(setup_tp TP_NUMBER)
    set(TARGET_NAME ${TP_NUMBER}_exe)
    add_executable(${TARGET_NAME})
    target_compile_features(${TARGET_NAME} PRIVATE cxx_std_11)

    # Enable many good warnings
    if (MSVC)
        target_compile_options(${TARGET_NAME} PRIVATE /WX /W3)
    else()
        target_compile_options(${TARGET_NAME} PRIVATE -Werror -W -Wall -Wextra -Wpedantic -pedantic-errors)
    endif()
    
    # Add all the source and header files
    target_include_directories(${TARGET_NAME} PRIVATE ${TP_NUMBER})
    file(GLOB_RECURSE MY_SOURCES CONFIGURE_DEPENDS ${TP_NUMBER}/*)
    target_sources(${TARGET_NAME} PRIVATE ${MY_SOURCES})

    # Add glimac as a dependency
    target_link_libraries(${TARGET_NAME} glimac)

    # Copy the assets and the shaders to the output folder (where the executable is created)
    function(copy_folder_to_output DIR)
        string(SHA1 TARGET_HASH ${DIR})                                  # Create a unique name for our custom target. We can't use ${DIR} directly because it could contain invalid characters like spaces
        set(CUSTOM_TARGET_NAME CopyToOutput_${TP_NUMBER}_${TARGET_HASH}) #
        add_custom_target(${CUSTOM_TARGET_NAME}
            COMMENT "Copying \"${DIR}\""
            COMMAND ${CMAKE_COMMAND} -E copy_directory
                ${CMAKE_SOURCE_DIR}/${DIR}
                $<TARGET_FILE_DIR:${TARGET_NAME}>/${DIR}
        )
        add_dependencies(${TARGET_NAME} ${CUSTOM_TARGET_NAME}) # Mark our custom target as a dependency of our TP, so that whenever the TP is launched our custom target is triggered and files are copied
    endfunction()
    copy_folder_to_output(assets)
    copy_folder_to_output(${TP_NUMBER}/shaders)
endfunction(setup_tp)

setup_tp(TP1)
setup_tp(TP2)
setup_tp(TP3)
setup_tp(TP4)
setup_tp(TP5)
setup_tp(TP6)
setup_tp(TP7)
setup_tp(TP8)
setup_tp(TP9)