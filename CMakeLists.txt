cmake_minimum_required(VERSION 3.2)
project(HockeySDK)

include(ExternalProject)

add_custom_target(HockeyCommand
        COMMAND xcodebuild -project ${CMAKE_CURRENT_SOURCE_DIR}/Latest/Support/HockeySDK.xcodeproj -target HockeySDK
        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        )

add_library(HockeySDK INTERFACE)
add_dependencies(HockeySDK HockeyCommand)
target_link_libraries(HockeySDK INTERFACE "-framework HockeySDK" "-F${CMAKE_CURRENT_SOURCE_DIR}/build/Release")
