# Portions of this come from KiCad's CMakeLists.txt
# set the project name
project('wxWabbitemu', ['c', 'cpp'],
	version: '0.1.0',
	license: 'GPL2+',
	default_options : ['default_library=static'])

# find wx + include it
# Turn on wxWidgets compatibility mode for some classes
add_global_arguments('-DWX_COMPATIBILITY', language: ['c', 'cpp'])

# wxWabbitemu specific defines
add_global_arguments('-DHIGH_SHADE_GIF', '-DVERBOSE', '-D_LINUX', '-DWXVER', language: ['c', 'cpp'])

# Enable Unicode, as needed
compiler = meson.get_compiler('cpp')

if ['gcc', 'clang'].contains(compiler.get_id())
  if compiler.version().version_compare('>=4.8.0')
    add_global_arguments('-D_UNICODE', language: ['c', 'cpp'])
  endif
endif

# now hunt for wxWidgets
# (adv is used for "advanced" widgets, such as the wizard)
wxWidgets_dep = dependency('wxWidgets', required: true, modules: ['adv', 'net', 'core', 'base'], static: false)

# includes
includes = include_directories(
	'core',
	'debugger',
	'gui',
	'hardware',
	'interface',
	'utilities'
)

# add the executable
wxWabbitemu_exe = executable('wxWabbitemu',
	# Core
	'core/core.c',
	'core/alu.c',
	'core/control.c',
	'core/device.c',
	'core/indexcb.c',
	
	# Calc Interfacing
	'interface/calc.c',
	'interface/state.c',
	
	# Utilities/Libraries
	'utilities/exportvar.c',
	'utilities/fileutilities.c',
	'utilities/gif.c',
	'utilities/gifhandle.c',
	'utilities/label.c',
	'utilities/savestate.c',
	'utilities/sendfile.c', 
	'utilities/var.c',
	
	# Hardware Emulation
	'hardware/81hw.c',
	'hardware/83hw.c',
	'hardware/83phw.c',
	'hardware/83psehw.c',
	'hardware/86hw.c',
	'hardware/keys.c',
	'hardware/lcd.c',
	'hardware/link.c',
	
	# wxWidgets GUI
	'gui/gui.cpp',                   # This requires ../gui/gui.h
	'gui/guiapp.cpp',                # This requires ../gui/guiapp.h
	'gui/guiskinwindow.cpp',         # This requires ../gui/guiskinwindow.h
	'gui/guilcd.cpp',                # This requires ../gui/guilcd.h
	'gui/guivartree.cpp',            # This requires ../gui/guivartree.h
	'gui/droptarget.cpp',            # This requires ../gui/droptarget.h
	'gui/wizard/wizardstart.cpp',    # This requires ../gui/wizard/wizardstart.h
	'gui/wizard/wizardcalctype.cpp', # This requires ../gui/wizard/wizardcalctype.h
	'gui/wizard/wizardos.cpp',       # This requires ../gui/wizard/wizardos.h
	'gui/wizard/romwizard.cpp',      # This requires ../gui/wizard/romwizard.h
	'debugger/guidebug.cpp',         # This requires ../debugger/guidebug.h
	
	# Debugger and debugger GUI
	'debugger/disassemblyview.cpp',  # This requires ../debugger/disassemblyview.h
	'debugger/disassemble.c',
	'debugger/panes/regpane.cpp',    # This requires ../debugger/panes/regpane.h
	'debugger/panes/flagspane.cpp',  # This requires ../debugger/panes/flagspane.h
	'debugger/panes/cpupane.cpp',    # This requires ../debugger/panes/cpupane.h
	
	dependencies: wxWidgets_dep,
	
	# mixing of C and C++ necessitates builds in c++
	c_args: ['-x', 'c++'],
	
	include_directories: includes,
	install: true
)

