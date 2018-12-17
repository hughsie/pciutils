install_headers([
    'header.h',
    'pci.h',
    'types.h',
    configh,
  ],
  subdir : 'pci',
)

pci = shared_library(
  'pci',
  sources : [
    'access.c',
    'caps.c',
    'dump.c',
    'filter.c',
    'generic.c',
    'i386-ports.c',
    'init.c',
    'names.c',
    'names-cache.c',
    'names-hash.c',
    'names-hwdb.c',
    'names-net.c',
    'names-parse.c',
    'params.c',
    'proc.c',
    'sysfs.c',
  ],
  soversion : lt_current,
  version : lt_version,
  dependencies : [
    libzlib,
  ],
  include_directories : [
    include_directories('..'),
  ],
  install : true
)

pkgg = import('pkgconfig')
pkgg.generate(
  libraries : pci,
  variables : [
    'idsdir=' + idsdir,
  ],
  version : meson.project_version(),
  name : 'libpci',
  filebase : 'libpci',
  description : 'libpci',
)
