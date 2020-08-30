cmake_minimum_required(VERSION 3.0.0)
project(openvino_api VERSION 0.1.0)


set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --std=c++11")

# set(OPENCV_PATH "/home/mike/workspace/utils/opencv440openvino/")

# set(LIBS
#     ${OPENCV_PATH}/lib/libopencv_core.so
#     ${OPENCV_PATH}/lib/libopencv_imgproc.so
#     ${OPENCV_PATH}/lib/libopencv_imgcodecs.so
#     ${OPENCV_PATH}/lib/libopencv_highgui.so
#     ${OPENCV_PATH}/lib/libopencv_video.so
#     ${OPENCV_PATH}/lib/libopencv_videoio.so
#     ${OPENCV_PATH}/lib/libopencv_dnn.so
# )

set(SOURCES
    src/main.cpp
)
# include_directories(BEFORE ${OPENCV_PATH}/include)

#message(STATUS ${InferenceEngine_DIR})
#message(STATUS ${NGRAPH_DIR})
#message(STATUS $ENV{ngraph_DIR})

#set(ngraph_DIR $ENV{ngraph_DIR})

 find_package(ngraph REQUIRED)
 find_package(InferenceEngine REQUIRED)
 find_package(OpenCV REQUIRED)

add_executable(${PROJECT_NAME} ${SOURCES})

target_link_libraries(${PROJECT_NAME} PRIVATE 
    ${InferenceEngine_LIBRARIES} 
    ${OpenCV_LIBS} 
    ${NGRAPH_LIBRARIES}
)

message(STATUS ${InferenceEngine_LIBRARIES})
message(STATUS ${OpenCV_LIBS})
message(STATUS ${NGRAPH_LIBRARIES})



target_include_directories(${PROJECT_NAME} BEFORE PUBLIC 
 $ENV{INTEL_OPENVINO_DIR}/inference_engine/include
 ${CMAKE_SOURCE_DIR}/include/common)


# message(STATUS ${OPENCV_PATH})
# message(STATUS ${INCLUDE_DIRECTORIES})
 
# target_link_libraries ( ${PROJECT_NAME} PRIVATE ${LIBS})

# add_custom_target ( dist ALL
#   COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_LIST_DIR}/init.ini ${CMAKE_CURRENT_BINARY_DIR}
#   COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_LIST_DIR}/test.ini ${CMAKE_CURRENT_BINARY_DIR}
# )
