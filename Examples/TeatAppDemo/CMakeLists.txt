add_executable(TeatAppDemo
  TeatAppDemo.swift)
add_custom_command(TARGET TeatAppDemo POST_BUILD
  COMMAND
    mt -nologo -manifest ${CMAKE_CURRENT_SOURCE_DIR}/TeatAppDemo.exe.manifest -outputresource:$<TARGET_FILE:TeatAppDemo>
  COMMAND
    ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/Info.plist $<TARGET_FILE_DIR:TeatAppDemo>
  COMMAND
    ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/Assets/CoffeeCup.jpg $<TARGET_FILE_DIR:TeatAppDemo>)
# FIXME(SR-12683) `@main` requires `-parse-as-library`
target_compile_options(TeatAppDemo PRIVATE
  -parse-as-library)
target_link_libraries(TeatAppDemo PRIVATE
  SwiftWin32)