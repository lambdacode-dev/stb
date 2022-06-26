cmake_minimum_required(VERSION 3.10)


project(stb)
add_library(stb INTERFACE)

target_include_directories(stb
                           INTERFACE
                           $<INSTALL_INTERFACE:include/stb>
                           )


install(TARGETS stb EXPORT stbTargets)

set(STB_HEADER_FILES stb_c_lexer.h stb_connected_components.h stb_divide.h stb_ds.h stb_dxt.h stb_easy_font.h stb_herringbone_wang_tile.h stb_hexwave.h stb_image.h stb_image_resize.h stb_image_write.h stb_include.h stb_leakcheck.h stb_rect_pack.h stb_sprintf.h stb_textedit.h stb_tilemap_editor.h stb_truetype.h stb_voxel_render.h)
install(FILES ${STB_HEADER_FILES} DESTINATION include/stb)

install(EXPORT stbTargets
  FILE stbTargets.cmake
  NAMESPACE stb::
  DESTINATION lib/cmake/stb
)

include(CMakePackageConfigHelpers)
# generate the config file that is includes the exports
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
  "${CMAKE_CURRENT_BINARY_DIR}/stbConfig.cmake"
  INSTALL_DESTINATION "lib/cmake/stb"
  NO_SET_AND_CHECK_MACRO
  NO_CHECK_REQUIRED_COMPONENTS_MACRO
  )

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/stbConfig.cmake
  DESTINATION lib/cmake/stb
  )

