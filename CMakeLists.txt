cmake_minimum_required(VERSION 2.6)

include(ReMake)

remake_project(
  starleth-diagnostics-ros-${ROS_DISTRIBUTION}
  VERSION 0.1
  RELEASE alpha
  SUMMARY "Diagnostics tools over ROS for the StarlETH robot."
  AUTHOR "Jerome Maye"
  CONTACT "jerome.maye@mavt.ethz.ch"
  HOME "http://github.com/jmaye/starleth-diagnostics-ros"
  LICENSE "GNU Lesser General Public License (LGPL)"
  PREFIX starleth-diagnostics-
  INSTALL /usr
  CONFIGURATION_DESTINATION /etc/starleth-diagnostics
  EXTRA_CXX_FLAGS -std=c++0x
)

remake_var_name(GIT_REVISION_VAR ${REMAKE_PROJECT_NAME} GIT_REVISION)

remake_ros_pack_deb()

if(${ROS_DISTRIBUTION} STREQUAL fuerte)
  remake_ros_distribute_deb(
    DISTRIBUTION lucid
    SECTION libs
    DEPENDS remake pkg-config
    UPLOAD ppa:jmaye/starleth
    PASS CMAKE_BUILD_TYPE ${GIT_REVISION_VAR}
    FORCE_CONSISTENCY
  )
endif()

remake_ros_distribute_deb(
  DISTRIBUTION precise
  SECTION libs
  DEPENDS remake pkg-config
  UPLOAD ppa:jmaye/starleth
  PASS CMAKE_BUILD_TYPE ${GIT_REVISION_VAR}
  FORCE_CONSISTENCY
)
