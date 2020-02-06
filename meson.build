project( 'zstd', 'c', default_options : [ 'c_std=gnu99' ], version : '1.4.4' )

includes = include_directories(
    'lib',
    'lib/common',
    'lib/compress',
    'lib/decompress',
    'lib/dictBuilder'
)

headers = [
    'lib/zstd.h',
    'lib/dictBuilder/zdict.h',
    'lib/common/zstd_errors.h'
]

sources = [
    'lib/common/entropy_common.c',
    'lib/common/fse_decompress.c',
    'lib/common/threading.c',
    'lib/common/pool.c',
    'lib/common/zstd_common.c',
    'lib/common/error_private.c',
    'lib/common/xxhash.c',
    'lib/compress/hist.c',
    'lib/compress/fse_compress.c',
    'lib/compress/huf_compress.c',
    'lib/compress/zstd_compress.c',
    'lib/compress/zstd_compress_literals.c',
    'lib/compress/zstd_compress_sequences.c',
    'lib/compress/zstdmt_compress.c',
    'lib/compress/zstd_fast.c',
    'lib/compress/zstd_double_fast.c',
    'lib/compress/zstd_lazy.c',
    'lib/compress/zstd_opt.c',
    'lib/compress/zstd_ldm.c',
    'lib/decompress/huf_decompress.c',
    'lib/decompress/zstd_decompress.c',
    'lib/decompress/zstd_decompress_block.c',
    'lib/decompress/zstd_ddict.c',
    'lib/dictBuilder/cover.c',
    'lib/dictBuilder/fastcover.c',
    'lib/dictBuilder/divsufsort.c',
    'lib/dictBuilder/zdict.c'
]

dependencies = [ dependency( 'threads' ) ]

c_args = [ '-DZSTD_MULTITHREAD' ]
dep_args = []

if host_machine.system() == 'windows'
    c_args += '-DZSTD_DLL_EXPORT=1'
    dep_args += '-DZSTD_DLL_IMPORT=1'
    sources += import( 'windows' ).compile_resources( 'build/VS2010/libzstd-dll/libzstd-dll.rc', include_directories : includes )
endif

zstd_lib = library( 'zstd', name_prefix : 'lib', include_directories : includes, sources : sources, c_args : c_args, dependencies : dependencies, gnu_symbol_visibility : 'hidden', install : true )
zstd_lic = files( 'LICENSE' )
zstd_dep = declare_dependency( include_directories : include_directories( 'lib', 'lib/dictBuilder', 'lib/common' ), compile_args : dep_args, link_with : zstd_lib )
install_headers( headers )
