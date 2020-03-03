find_program(BIN2CODE_NODE_EXECUTABLE NAMES node nodejs HINTS /opt/local/bin)
if (NOT DEFINED BIN2CODE_NODE_EXECUTABLE)
    message(FATAL_ERROR "Node.js executable required but not found")
endif()

set(BIN2CODE_EXECUTABLE ${BIN2CODE_NODE_EXECUTABLE} ${CMAKE_CURRENT_LIST_DIR}/bin2code.js CACHE INTERNAL "")

function(bin2code file_path output_path)
    add_custom_command(
        OUTPUT ${output_path}
        COMMAND ${BIN2CODE_EXECUTABLE} ${file_path} ${output_path}
        DEPENDS ${file_path}
    )
endfunction(bin2code)
