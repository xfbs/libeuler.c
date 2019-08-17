project(
  'libeuler',
  'c',
  default_options: ['c_std=c11'],
  version: '0.1.0',
  license: 'MIT')

conf_data = configuration_data()
conf_data.set('VERSION', meson.project_version())
conf_data.set('VERSION_MAJ', meson.project_version().split('.')[0])
conf_data.set('VERSION_MIN', meson.project_version().split('.')[1])
conf_data.set('VERSION_REV', meson.project_version().split('.')[2])

include_dir = include_directories('include')

sources = [
  'src/collatz.c',
  'src/math.c',
  'src/modular_arithmetic.c',
  'src/prime.c',
  'src/sieve.c',
  'src/vec8.c',
  'src/vec16.c',
  'src/vec32.c',
  'src/vec64.c',
  'src/vecp.c',
]

# main library
libpassgen = library(
  'euler',
  sources,
  install: true,
  include_directories: include_dir)

# headers
install_headers(
  'include/euler.h')
install_headers(
  'include/euler/collatz.h',
  'include/euler/math.h',
  'include/euler/modular_arithmetic.h',
  'include/euler/prime.h',
  'include/euler/sieve.h',
  'include/euler/vec8.h',
  'include/euler/vec16.h',
  'include/euler/vec32.h',
  'include/euler/vec64.h',
  'include/euler/vecp.h',
  subdir: 'euler')

# pkgconfig file
pkg = import('pkgconfig')
pkg.generate(
  libpassgen,
  description: 'data structures useful for solving project euler problems, in C.')
