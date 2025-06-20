
inc_dir = include_directories('../utilities', incdir_numpy)
openmp = dependency('openmp', required: false)
if openmp.found()
  if host_machine.system() == 'windows'
    # On Windows, the mingw compiler does not support OpenMP ATOMIC operations
    openmp_deps = dependencies + [openmp]
  else
    openmp_deps = dependencies + [openmp]
  endif

else
  openmp_deps = dependencies
endif


util_srcs = ['../utilities/quad_tree.c',
                 '../utilities/sparse_dok.c',
                 '../utilities/sparse_csr.c']

# Compile the Cython-generated C code and additional C code
py3.extension_module('fitsmooth_ext',
  sources: ['fitsmooth_ext.pyx'] + util_srcs,
  include_directories: inc_dir,
  c_args : ['-O3', '-march=native', '-fopenmp', '-g'],
  dependencies: openmp_deps,
  subdir: 'anuga/fit_interpolate',
  install: true,
)

python_sources = [
  'benchmark_least_squares.py',
  'fit.py',
  'general_fit_interpolate.py',
  '__init__.py',
  'interpolate2d.py',
  'interpolate.py',
  'profile_long_benchmark.py',
  'run_long_benchmark.py',
  'ticket178_benchmark.py',
]

py3.install_sources(
  python_sources,
  subdir: 'anuga/fit_interpolate'
)

subdir('tests')
