https://blog.csdn.net/GGY1102/article/details/106199054
#find_package(OpenCV 3.0 QUIET)
#if(NOT OpenCV_FOUND)
#   find_package(OpenCV 2.4.3 QUIET)
#   if(NOT OpenCV_FOUND)
#      message(FATAL_ERROR "OpenCV > 2.4.3 not found.")
#   endif()
#endif()
set(OpenCV_DIR /usr/lib/cmake/opencv4)
set(OpenCV_INCLUDE_DIRS /usr/include/opencv4)
set(OpenCV_LIBS opencv_core opencv_imgproc opencv_highgui opencv_imgcodecs opencv_videoio)
include_directories(${OpenCV_INCLUDE_DIRS})

ORB_SLAM2改动

https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html
https://orbbec.github.io/OrbbecSDK_ROS2/zh/source/camera_devices/4_application_guide/launch_parameters.html
https://originbot.org/manual/package_develop.html
https://gazebosim.org/docs/all/migration_from_ignition/
https://fishros.com/d2lros2foxy/#/chapt7/7.4%E6%9C%BA%E5%99%A8%E4%BA%BA%E8%BF%90%E5%8A%A8%E5%AD%A6%E4%BB%8B%E7%BB%8D
https://book.guyuehome.com/ROS2/2.%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5/2.1_%E5%B7%A5%E4%BD%9C%E7%A9%BA%E9%97%B4/
https://x2-aimdk.agibot.com/zh-cn/latest/quick_start/code_sample.html#id2
