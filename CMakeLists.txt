cmake_minimum_required (VERSION 3.11)
project(hd44780_analyzer)

# custom CMake Modules are located in the cmake directory.
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

include(ExternalAnalyzerSDK)

set(SOURCES 
src/HD44780Analyzer.cpp
src/HD44780Analyzer.h
src/HD44780AnalyzerResults.cpp
src/HD44780AnalyzerResults.h
src/HD44780AnalyzerSettings.cpp
src/HD44780AnalyzerSettings.h
src/HD44780SimulationDataGenerator.cpp
src/HD44780SimulationDataGenerator.h
)

add_library(hd44780_analyzer SHARED ${SOURCES})
target_link_libraries(hd44780_analyzer PRIVATE Saleae::AnalyzerSDK)

if(MSVC)
    install(TARGETS hd44780_analyzer RUNTIME DESTINATION ".")
else()
    install(TARGETS hd44780_analyzer LIBRARY DESTINATION ".")
endif()

set_post_build_destination(hd44780_analyzer)
