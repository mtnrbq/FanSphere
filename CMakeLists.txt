#  Copyright (c) Microsoft Corporation. All rights reserved.
#  Licensed under the MIT License.

cmake_minimum_required (VERSION 3.10)

project (FanSphere C)

azsphere_configure_tools(TOOLS_REVISION "21.10")
azsphere_configure_api(TARGET_API_SET "11")

add_subdirectory("AzureSphereDevX" out)

set(Source
    "main.c"
)
source_group("Source" FILES ${Source})

set(ALL_FILES
    ${Source}
)

# Create executable
add_executable(${PROJECT_NAME} ${ALL_FILES})

target_compile_definitions(${PROJECT_NAME} PUBLIC AZURE_IOT_HUB_CONFIGURED)
target_link_libraries (${PROJECT_NAME} applibs pthread gcc_s c azure_sphere_devx)

target_include_directories(${PROJECT_NAME} PUBLIC Azure-Sphere-DevX/include . )

target_compile_options(${PROJECT_NAME} PRIVATE -Wno-unknown-pragmas)

azsphere_target_add_image_package(${PROJECT_NAME})
