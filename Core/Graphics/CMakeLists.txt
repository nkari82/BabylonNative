set(SOURCES
    "Include/Babylon/Graphics.h"
    "Source/${BABYLON_NATIVE_PLATFORM}/GraphicsPlatform.h"
    "Source/BgfxCallback.cpp"
    "Source/BgfxCallback.h"
    "Source/Graphics.cpp"
    "Source/GraphicsImpl.cpp"
    "Source/GraphicsImpl.h")

add_library(Graphics ${SOURCES})
warnings_as_errors(Graphics)

target_include_directories(Graphics
    PUBLIC "Include"
    PRIVATE "Source/${BABYLON_NATIVE_PLATFORM}")

target_link_to_dependencies(Graphics
    PUBLIC JsRuntime
    PRIVATE JsRuntimeInternal
    PRIVATE bgfx
    PRIVATE bimg
    PRIVATE bx)

target_compile_definitions(Graphics
    PRIVATE NOMINMAX)

set_property(TARGET Graphics PROPERTY FOLDER Core)
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SOURCES})

add_library(GraphicsInternal INTERFACE)
target_include_directories(GraphicsInternal
    INTERFACE "Source"
    INTERFACE "Source/${BABYLON_NATIVE_PLATFORM}")
target_link_to_dependencies(GraphicsInternal
    INTERFACE Graphics
    INTERFACE JsRuntimeInternal
    INTERFACE arcana
    INTERFACE bgfx
    INTERFACE bimg
    INTERFACE bx)
