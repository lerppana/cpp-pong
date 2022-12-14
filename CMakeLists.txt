cmake_minimum_required(VERSION 3.21.2)

project(pong CXX)

find_package(engine CONFIG REQUIRED)

include(engine_create)

set(PROJECT_FILE "${CMAKE_CURRENT_LIST_DIR}/pong.project")
engine_create_plugin(${PROJECT_NAME}
        PROJECT_FILE "${PROJECT_FILE}"

        SOURCE_FILES
            src/scenes/game.cpp
            src/scenes/load.cpp
            src/scenes/menu.cpp
            src/systems/ball_particle_system.cpp
            src/plugin.cpp

        INCLUDE_FILES
            src/scenes/game.hpp
            src/scenes/load.hpp
            src/scenes/menu.hpp
            src/systems/ball_particle_system.hpp
            src/tags.hpp
)

engine_create_launcher(
        SOURCE_DIR "${VCPKG_INSTALLED_DIR}/${VCPKG_TARGET_TRIPLET}/include/engine/launcher"
        PROJECT_FILE "${PROJECT_FILE}"
)

target_precompile_headers(${PROJECT_NAME} PUBLIC src/engine.hxx)

engine_install_plugin(${PROJECT_NAME})