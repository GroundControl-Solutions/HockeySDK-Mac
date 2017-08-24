cmake_minimum_required(VERSION 3.2)
project(HockeySDK)

include(ExternalProject)

find_library(HockeySDKFramework HockeySDK PATHS "${CMAKE_CURRENT_SOURCE_DIR}/Latest/Support/build/Release" NO_DEFAULT_PATH)

add_custom_target(HockeyCommand
	COMMAND xcodebuild -project "${CMAKE_CURRENT_SOURCE_DIR}/Latest/Support/HockeySDK.xcodeproj" -target HockeySDK VERBATIM
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

add_library(HockeySDK INTERFACE)
target_include_directories(HockeySDK INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/Latest/Support/build/Release/HockeySDK.framework/Headers/")
target_link_libraries(HockeySDK INTERFACE ${HockeySDKFramework})