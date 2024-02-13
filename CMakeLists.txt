cmake_minimum_required (VERSION 3.13)

project(QSPIAnalyzer)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(AnalyzerSDK_DIR SaleaeAnalyzerSDK)
find_package(AnalyzerSDK REQUIRED)

add_library(${PROJECT_NAME} SHARED
    src/QSpiAnalyzer.cpp
    src/QSpiAnalyzerResults.cpp
    src/QSpiAnalyzerSettings.cpp
    src/QSpiSimulationDataGenerator.cpp)

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 20)

target_compile_definitions(${PROJECT_NAME} PRIVATE LOGIC2 SALEAE)
target_link_libraries(${PROJECT_NAME} PRIVATE Saleae::AnalyzerSDK)

set(ANALYZER_DESTINATION "Analyzers")
install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION ${ANALYZER_DESTINATION}
                                LIBRARY DESTINATION ${ANALYZER_DESTINATION})

set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${ANALYZER_DESTINATION}
                                                 LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${ANALYZER_DESTINATION})
