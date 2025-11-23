ida_add_plugin(pdb
    SOURCES
        # Main compilation unit (unity build)
        # pdb.cpp includes: common.cpp, tilbuild.cpp, sip.cpp, msdia.cpp
        # msdia.cpp includes: pdblocal.cpp
        pdb.cpp

        # Compiled separately (per makefile O1=old)
        old.cpp

        # Headers (CMake needs them listed for IDE support)
        cvadd.h
        cvconst.h
        dbghelp.h
        dia2.h
        msdia.hpp
        oldpdb.h
        pdb.hpp
        pdbaccess.hpp
        pdblocal.hpp
        pdbremote.hpp
        sip.hpp
        tilbuild.hpp
        varser.hpp

        # Unity build includes (not compiled separately - included by pdb.cpp/msdia.cpp)
        common.cpp
        misc.cpp
        sip.cpp
        tilbuild.cpp
        msdia.cpp
        pdblocal.cpp
        pdbremote.cpp
        merge.cpp
)

# Mark #included files as HEADER_FILE_ONLY
set_source_files_properties(
    common.cpp
    misc.cpp
    sip.cpp
    tilbuild.cpp
    msdia.cpp
    pdblocal.cpp
    pdbremote.cpp
    merge.cpp
    PROPERTIES HEADER_FILE_ONLY TRUE
)

# Link DIA SDK (set by parent CMakeLists.txt)
target_include_directories(pdb PRIVATE ${DIA_SDK_INCLUDE_DIR})
target_link_libraries(pdb PRIVATE ${DIA_SDK_LIBRARY})

# Windows system libraries needed for DIA SDK
target_link_libraries(pdb PRIVATE ole32 oleaut32)
