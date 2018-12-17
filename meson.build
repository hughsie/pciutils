project('pciutils', 'c',
  version : '3.6.2',
  license : 'GPL-2.0+',
  meson_version : '>=0.47.0',
  default_options : ['warning_level=2', 'c_std=c99'],
)

# libtool versioning
lt_current = '3'
lt_revision = '0'
lt_age = '0'
lt_version = '@0@.@1@.@2@'.format(lt_current, lt_age, lt_revision)

# get suported warning flags
warning_flags = [
  '-Wall',
  '-W',
  '-Wno-parentheses',
  '-Wstrict-prototypes',
  '-Wmissing-prototypes',
]

conf = configuration_data()

cc = meson.get_compiler('c')
add_project_arguments(cc.get_supported_arguments(warning_flags), language : 'c')
add_project_arguments('-D_DEFAULT_SOURCE', language : 'c')

prefix = get_option('prefix')
sbindir = join_paths(prefix, get_option('sbindir'))
libdir = join_paths(prefix, get_option('libdir'))
mandir = join_paths(prefix, get_option('mandir'))

libzlib = dependency('zlib')

idsdir = get_option('idsdir')

conf.set('PCI_OS_LINUX', '1') # FIXME
conf.set_quoted('PCILIB_VERSION', meson.project_version())
conf.set_quoted('PCI_PATH_IDS_DIR', idsdir)
conf.set_quoted('PCI_PATH_SYS_BUS_PCI', get_option('sysbuspci'))
conf.set_quoted('PCI_IDS', get_option('pciids'))
conf.set_quoted('PCI_PATH_PROC_BUS_PCI', get_option('procbuspci'))
configh = configure_file(
  output : 'config.h',
  configuration : conf
)

subdir('lib')

executable(
  'setpci',
  sources : [
    'setpci.c',
    'common.c',
  ],
  include_directories : [
    include_directories('lib'),
  ],
  dependencies : [
  ],
  link_with : [
    pci,
  ],
  install : true,
  install_dir : sbindir
)

executable(
  'lspci',
  sources : [
    'lspci.c',
    'ls-vpd.c',
    'ls-caps.c',
    'ls-caps-vendor.c',
    'ls-ecaps.c',
    'ls-kernel.c',
    'ls-tree.c',
    'ls-map.c',
    'common.c',
  ],
  include_directories : [
    include_directories('lib'),
  ],
  dependencies : [
  ],
  link_with : [
    pci,
  ],
  install : true,
  install_dir : sbindir
)
