add_custom_target(ragel
    WORKING_DIRECTORY ${PROJECT_BINARY_DIR}
    COMMAND ragel -G2 src/lib/uri/uri_parser.rl -o src/lib/uri/uri_parser.c)

if (CC_HAS_WNO_IMPLICIT_FALLTHROUGH)
    # Suppress noise warnings for autogenerated Ragel code
    set_source_files_properties(uri_parser.c PROPERTIES COMPILE_FLAGS
        -Wno-implicit-fallthrough)
endif()
add_library(uri STATIC uri.c uri_parser.c)
