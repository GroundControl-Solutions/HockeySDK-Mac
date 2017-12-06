cmake_minimum_required(VERSION 3.2)
project(HockeySDK)

set(HOCKEYSDK_VERSION 3.2.1)

set(HOCKEYSDK_SOURCE_FILES
    Classes/BITHockeyManager.h
    Classes/BITHockeyManager.m
    Classes/BITHockeyManagerDelegate.h
    Classes/BetaDistribution/BITSystemProfile.h
    Classes/BetaDistribution/BITSystemProfile.m
    Classes/BetaDistribution/BITSystemProfilePrivate.h
    Classes/CrashReporting/BITCrashCXXExceptionHandler.h
    Classes/CrashReporting/BITCrashCXXExceptionHandler.mm
    Classes/CrashReporting/BITCrashDetails.h
    Classes/CrashReporting/BITCrashDetails.m
    Classes/CrashReporting/BITCrashDetailsPrivate.h
    Classes/CrashReporting/BITCrashExceptionApplication.h
    Classes/CrashReporting/BITCrashExceptionApplication.m
    Classes/CrashReporting/BITCrashManager.h
    Classes/CrashReporting/BITCrashManager.m
    Classes/CrashReporting/BITCrashManagerDelegate.h
    Classes/CrashReporting/BITCrashManagerPrivate.h
    Classes/CrashReporting/BITCrashMetaData.h
    Classes/CrashReporting/BITCrashMetaData.m
    Classes/CrashReporting/BITCrashReportTextFormatter.h
    Classes/CrashReporting/BITCrashReportTextFormatter.m
    Classes/CrashReporting/BITCrashReportUI.h
    Classes/CrashReporting/BITCrashReportUI.m
    Classes/CrashReporting/BITCrashReportUI.xib
    Classes/CrashReporting/BITHockeyAttachment.h
    Classes/CrashReporting/BITHockeyAttachment.m
    Classes/Feedback/BITActivityIndicatorButton.h
    Classes/Feedback/BITActivityIndicatorButton.m
    Classes/Feedback/BITFeedbackManager.h
    Classes/Feedback/BITFeedbackManager.m
    Classes/Feedback/BITFeedbackManagerPrivate.h
    Classes/Feedback/BITFeedbackMessage.h
    Classes/Feedback/BITFeedbackMessage.m
    Classes/Feedback/BITFeedbackMessageAttachment.h
    Classes/Feedback/BITFeedbackMessageAttachment.m
    Classes/Feedback/BITFeedbackMessageCellView.h
    Classes/Feedback/BITFeedbackMessageCellView.m
    Classes/Feedback/BITFeedbackMessageCellViewDelegate.h
    Classes/Feedback/BITFeedbackMessageDateValueTransformer.h
    Classes/Feedback/BITFeedbackMessageDateValueTransformer.m
    Classes/Feedback/BITFeedbackWindowController.h
    Classes/Feedback/BITFeedbackWindowController.m
    Classes/Feedback/BITFeedbackWindowController.xib
    Classes/Helper/BITHockeyAppClient.h
    Classes/Helper/BITHockeyAppClient.m
    Classes/Helper/BITHockeyBaseManager.m
    Classes/Helper/BITHockeyBaseManagerPrivate.h
    Classes/Helper/BITHockeyHelper.h
    Classes/Helper/BITHockeyHelper.m
    Classes/Helper/BITHTTPOperation.h
    Classes/Helper/BITHTTPOperation.m
    Classes/Helper/BITKeychainItem.h
    Classes/Helper/BITKeychainItem.m
    Classes/Helper/BITSDKColoredView.h
    Classes/Helper/BITSDKColoredView.m
    Classes/Helper/BITSDKTextFieldCell.h
    Classes/Helper/BITSDKTextFieldCell.m
    Classes/Helper/BITSDKTextView.h
    Classes/Helper/BITSDKTextView.m
    Classes/Helper/BITSDKTextViewDelegate.h
    Classes/Helper/HockeySDKNullability.h
    Classes/Helper/HockeySDKPrivate.h
    Classes/Helper/HockeySDKPrivate.m
    Vendor/CrashReporter/Headers/CrashReporter.h
    Vendor/CrashReporter/Headers/PLCrashFeatureConfig.h
    Vendor/CrashReporter/Headers/PLCrashMacros.h
    Vendor/CrashReporter/Headers/PLCrashNamespace.h
    Vendor/CrashReporter/Headers/PLCrashReport.h
    Vendor/CrashReporter/Headers/PLCrashReportApplicationInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportBinaryImageInfo.h
    Vendor/CrashReporter/Headers/PLCrashReporter.h
    Vendor/CrashReporter/Headers/PLCrashReporterConfig.h
    Vendor/CrashReporter/Headers/PLCrashReportExceptionInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportFormatter.h
    Vendor/CrashReporter/Headers/PLCrashReportMachExceptionInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportMachineInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportProcessInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportProcessorInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportRegisterInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportSignalInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportStackFrameInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportSymbolInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportSystemInfo.h
    Vendor/CrashReporter/Headers/PLCrashReportTextFormatter.h
    Vendor/CrashReporter/Headers/PLCrashReportThreadInfo.h
    )

add_library(HockeySDK ${HOCKEYSDK_SOURCE_FILES})

target_include_directories(HockeySDK PUBLIC
                           ${CMAKE_CURRENT_SOURCE_DIR}
                           HockeySDK/
                           Classes/
                           Classes/CrashReporting/
                           Classes/BetaDistribution/
                           Classes/Feedback/
                           Classes/Helper/
                           Vendor/CrashReporter/Headers/
                           )
target_compile_definitions(HockeySDK PRIVATE -DBITHOCKEY_VERSION=@"${HOCKEYSDK_VERSION}")

find_library(QUICKLOOK QuickLook)
find_library(QUARTZ Quartz)
find_library(COCOA Cocoa)

target_link_libraries(HockeySDK PRIVATE
                      ${CMAKE_CURRENT_SOURCE_DIR}/Vendor/CrashReporter/libCrashReporter-MacOSX-Static.a
                      ${QUICKLOOK}
                      ${QUARTZ}
                      ${COCOA}
                      ${Foundation}
                      ${IOKit}
                      ${Security}
                      )

file(MAKE_DIRECTORY HockeySDK)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Resources/HockeySDK.h ${CMAKE_CURRENT_SOURCE_DIR}/HockeySDK/HockeySDK.h COPYONLY)