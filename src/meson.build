psl_make_dafsa = find_program('psl-make-dafsa')

suffixes_dafsa_h = custom_target('suffixes_dafsa.h',
  input : psl_file,
  output : 'suffixes_dafsa.h',
  command : [python, psl_make_dafsa, '--output-format=cxx+', '@INPUT@', '@OUTPUT@'])

sources = [
  'lookup_string_in_fixed_set.c',
  'psl.c',
]

cargs = [
  '-DHAVE_CONFIG_H',
  '-DBUILDING_PSL',
  '-DPSL_DISTFILE="@0@"'.format(psl_distfile),
]

libpsl = library('psl', sources, suffixes_dafsa_h,
  include_directories : [configinc, includedir],
  c_args : cargs,
  dependencies : [libidn2_dep, libidn_dep, libicu_dep, libunistring],
)

pkgconfig.generate(libpsl,
  name : 'libpsl',
  description : 'Public Suffix List C library')

libpsl_dep = declare_dependency(link_with : libpsl,
  include_directories : includedir)
