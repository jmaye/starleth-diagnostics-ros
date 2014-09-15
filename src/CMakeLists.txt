remake_ros_package(
  starleth_diagnostics
  RUN_DEPENDS diagnostic_aggregator
  DESCRIPTION "Diagnostics tools for the StarlETH robot."
)
remake_ros_package_config_generate(PACKAGE starleth_diagnostics)
