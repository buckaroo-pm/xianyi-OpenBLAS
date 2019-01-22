load('//:buckaroo_macros.bzl', 'buckaroo_deps')
load('//:subdir_glob.bzl', 'subdir_glob')
load('//:extract.bzl', 'extract')

genrule(
  name = 'make',
  out = 'out',
  srcs = glob([
    '*_check',
    '*.h',
    '*.in',
    '*.c',
    '*.S',
    'Makefile*',
    'driver/**/*',
    'exports/**/*',
    'interface/**/*',
    'kernel/**/*',
    'lapack/**/*',
  ]),
  cmd = ' && '.join([
    'mkdir -p $OUT',
    'cd $SRCDIR',
    'make',
    'make install PREFIX=$OUT',
  ]),
)

prebuilt_cxx_library(
  name = 'openblas',
  header_namespace = '',
  exported_headers = {
    'cblas.h': extract(':make', 'include/cblas.h'),
    'f77blas.h': extract(':make', 'include/f77blas.h'),
    'openblas_config.h': extract(':make', 'include/openblas_config.h'),
  },
  static_lib = extract(':make', 'lib/libopenblas.a'),
  shared_lib = extract(':make', 'lib/libopenblas.so'),
  visibility = [
    'PUBLIC',
  ],
)
