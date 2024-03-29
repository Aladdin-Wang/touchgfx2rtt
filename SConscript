import os
import rtconfig
from building import *

cwd = GetCurrentDir()
libs = []
# add general drivers

src = Split('''
TouchGFX/target/generated/OSWrappers_RTT.cpp
TouchGFX/target/generated/STM32DMA.cpp
TouchGFX/target/STM32TouchController.cpp
TouchGFX/target/TouchGFXGPIO.cpp
TouchGFX/target/generated/TouchGFXConfiguration.cpp
TouchGFX/target/generated/TouchGFXGeneratedHAL.cpp
TouchGFX/target/TouchGFXHAL.cpp
TouchGFX/App/app_touchgfx.c
examples/touchgfx_main.c
''')

path  = [cwd + '/TouchGFX']
path  = [cwd + '/TouchGFX/App']
path += [cwd + '/TouchGFX/target']
path += [cwd + '/TouchGFX/target/generated']
path += [cwd + '/Middlewares/ST/touchgfx/framework/include']

if rtconfig.CPU =='cortex-m7' :
    if rtconfig.CROSS_TOOL == 'gcc':
        libpath = [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m7/gcc']
        libs += ['touchgfx-float-abi-hard']
        src += [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m7/gcc/libtouchgfx-float-abi-hard.a']
    elif rtconfig.CROSS_TOOL == 'keil':
        libpath = [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m7/Keil6.x']
        libs += ['touchgfx_core_wchar32.lib']
        src += [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m7/Keil/touchgfx_core_wchar32.lib']
    elif rtconfig.CROSS_TOOL == 'iar':
        libpath = [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m7/IAR8.x']
        libs += ['touchgfx_core.a']
        src += [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m7/IAR8.x/touchgfx_core.a']
elif rtconfig.CPU =='cortex-m4' :
    if rtconfig.CROSS_TOOL == 'gcc':
        libpath = [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m4f/gcc']
        libs += ['touchgfx-float-abi-hard']
        src += [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m4f/gcc/libtouchgfx-float-abi-hard.a']
    elif rtconfig.CROSS_TOOL == 'keil':
        libpath = [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m4f/Keil6.x']
        libs += ['touchgfx_core_wchar32.lib']
        src += [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m4f/Keil/touchgfx_core_wchar32.lib']
    elif rtconfig.CROSS_TOOL == 'iar':
        libpath = [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m4f/IAR8.x']
        libs += ['touchgfx_core.a']
        src += [cwd + '/Middlewares/ST/touchgfx/lib/core/cortex_m4f/IAR8.x/touchgfx_core.a']
        
group = DefineGroup('TouchGFX_app', src, depend = ['PKG_USING_TOUCHGFX2RTT'], CPPPATH = path, LIBS = libs, LIBPATH = libpath)

# add TouchGFX generated
genSrc = Glob('./TouchGFX/generated/fonts/src/*.cpp')
genSrc += Glob('./TouchGFX/generated/gui_generated/src/*/*.cpp')
genSrc += Glob('./TouchGFX/generated/images/src/*.cpp')
genSrc += Glob('./TouchGFX/generated/texts/src/*.cpp')

genPath = [cwd + '/TouchGFX/generated/fonts/include']
genPath += [cwd + '/TouchGFX/generated/gui_generated/include']
genPath += [cwd + '/TouchGFX/generated/images/include']
genPath += [cwd + '/TouchGFX/generated/texts/include']

group = group + DefineGroup('TouchGFX_generated', genSrc, depend = ['PKG_USING_TOUCHGFX2RTT'], CPPPATH = genPath)

# add TouchGFX resource
resSrc = Glob('./TouchGFX/generated/images/src/*/*.cpp')
resSrc += Glob('./TouchGFX/generated/images/src/*/*/*.cpp')
group = group + DefineGroup('TouchGFX_resource', resSrc, depend = ['PKG_USING_TOUCHGFX2RTT'])

# add TouchGFX gui
guiSrc = Glob('./TouchGFX/gui/src/*/*.cpp')
guiPath = [cwd + '/TouchGFX/gui/include']

group = group + DefineGroup('TouchGFX_gui', guiSrc, depend = ['PKG_USING_TOUCHGFX2RTT'], CPPPATH = guiPath)

Return('group')
