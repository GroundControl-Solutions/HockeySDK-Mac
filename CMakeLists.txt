cmake_minimum_required(VERSION 3.2)
project(HockeySDK)

include(ExternalProject)

find_library(HockeySDKFramework HockeySDK PATHS "${CMAKE_CURRENT_SOURCE_DIR}/Latest/Support/build/Release" NO_DEFAULT_PATH)

add_custom_target(HockeyCommand
	COMMAND xcodebuild -project "${CMAKE_CURRENT_SOURCE_DIR}/Latest/Support/HockeySDK.xcodeproj" -target HockeySDK VERBATIM
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

add_custom_target(HockeyHeaders
	COMMAND cmake -E create_symlink "${CMAKE_CURRENT_SOURCE_DIR}/Latest/Product/HockeySDK.framework/Headers" "${CMAKE_CURRENT_BINARY_DIR}/HockeySDK" VERBATIM
)

add_library(HockeySDK INTERFACE)
target_include_directories(HockeySDK INTERFACE "${CMAKE_CURRENT_BINARY_DIR}")
target_link_libraries(HockeySDK INTERFACE ${HockeySDKFramework})
add_dependencies(HockeySDK HockeyCommand HockeyHeaders)
