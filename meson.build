project(
  'libeuler',
  'c',
  default_options: ['c_std=c11'],
  version: '0.1.0',
  license: 'MIT')

cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required : false)

conf_data = configuration_data()
conf_data.set('VERSION', meson.project_version())
conf_data.set('VERSION_MAJ', meson.project_version().split('.')[0])
conf_data.set('VERSION_MIN', meson.project_version().split('.')[1])
conf_data.set('VERSION_REV', meson.project_version().split('.')[2])

include_dir = include_directories('include')

all_files = [
  'collatz',
  'math',
  'modular_arithmetic',
  'prime',
  'sieve',
  'vec8',
  'vec16',
  'vec32',
  'vec64',
  'vecp',
]

sources = []
foreach f : all_files
  sources += 'src/@0@.c'.format(f)
endforeach

# main library
libeuler = library(
  'euler',
  sources,
  install: true,
  include_directories: include_dir,
  dependencies: [m_dep])

# dependency
libeuler_dep = declare_dependency(
  include_directories: include_dir,
    link_with: libeuler)

tests = []
foreach f : all_files
  tests += 'test/@0@_test.c'.format(f)
endforeach

# tests
generate_all = find_program('test/all.rb')
all_tests = custom_target(
  'all.c',
  input: tests,
  output: 'all.c',
  command: [generate_all, '@OUTPUT@', '@INPUT@'])
tests = executable(
  'tests',
  tests,
  all_tests,
  link_with: libeuler,
  include_directories: include_dir)
test('tests', tests)

# headers
install_headers(
  'include/euler.h')

headers = []
foreach f : all_files
  headers += 'include/euler/@0@.h'.format(f)
endforeach

install_headers(
  headers,
  subdir: 'euler')

# pkgconfig file
pkg = import('pkgconfig')
pkg.generate(
  libeuler,
  description: 'data structures useful for solving project euler problems, in C.')
