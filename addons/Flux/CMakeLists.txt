# Base Io build system
# Written by Jeremy Tregunna <jeremy.tregunna@me.com>
#
# Builds the Flux addon

# Create the _build bundle hierarchy if needed.
make_build_bundle(_build)

# Generate the IoFluxInit.c file.
# Argument SHOULD ALWAYS be the exact name of the addon, case is
# important.
generate_ioinit(Flux)

# Output our dynamic library to the top-level _build hierarchy
set(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR}/_build/dll)

# Our library sources.
set(SRCS "${CMAKE_CURRENT_SOURCE_DIR}/source/IoFluxInit.c")

# Now build the shared library
add_library(IoFlux SHARED ${SRCS})
add_dependencies(IoFlux iovmall)
target_link_libraries(IoFlux iovmall)

# Install the addon to our global addons hierarchy.
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} DESTINATION lib/io/addons)
install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/_build DESTINATION lib/io/addons/Flux)
