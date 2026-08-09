# Copyright (C) 2026 CharOfString <root@charofstring.cc>
#
# This program is free software: you can redistribute it and/or modify it under
# the terms of the GNU General Public License as published by the Free Software
# Foundation, version 3.
#
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
# FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License along with
# this program. If not, see <https://www.gnu.org/licenses/>.

cmake_minimum_required(VERSION 3.21)

project(gxwm_neolk VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.5
  REQUIRED COMPONENTS
    Quick
    ShaderTools
)

qt_standard_project_setup(REQUIRES 6.5)

foreach(cur IN ITEMS
  qml/LiquidGlass.qml
  qml/LiquidGlassButton.qml
  qml/Main.qml
  qml/TintArea.qml
)
get_filename_component(qml_alias "${cur}" NAME)
set_source_files_properties("${cur}" PROPERTIES QT_RESOURCE_ALIAS "${qml_alias}")
endforeach()

qt_add_executable(gxwm_neolk
  src/main.cc
)

qt_add_qml_module(gxwm_neolk
  URI NeoLK
  VERSION 1.0
  QML_FILES
    qml/MainWindow.qml
)

target_link_libraries(gxwm_neolk PRIVATE
  Qt6::Quick
)

include(GNUInstallDirs)

install(TARGETS gxwm_neolk
  BUNDLE DESTINATION .
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
