include_directories(${INCLUDE_DIRS})
ament_add_gtest(${PROJECT_NAME}_test main.cpp)
ament_add_gtest(${PROJECT_NAME}_test_image_encodings test_image_encodings.cpp)
