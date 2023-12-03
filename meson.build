project('hawktsdemux', 'c', version : '1.22.7.1', license : 'LGPL')
plugins_install_dir = join_paths(get_option('libdir'), 'gstreamer-1.0')
cc = meson.get_compiler('c')
gst_version = meson.project_version()
api_version = '1.0'
configinc = include_directories(['.', 'src'])

gstcodecparsers_dep = dependency('gstreamer-codecparsers-1.0', version  : '>=1.22.7', required : true)
gst_dep             = dependency('gstreamer-1.0', version : '>=1.22.7', required : true)
gstbase_dep         = dependency('gstreamer-base-1.0', version : '>=1.22.7', required: true)
gstmpegts_dep       = dependency('gstreamer-mpegts-1.0', version : '>=1.22.7', required: true)
gsttag_dep          = dependency('gstreamer-tag-1.0', version : '>=1.22.7', required: true)
gstpbutils_dep      = dependency('gstreamer-pbutils-1.0', version : '>=1.22.7', required: true)
gstaudio_dep        = dependency('gstreamer-audio-1.0', version : '>=1.22.7', required: true)
libunwind_dep       = dependency('libunwind', version : '>=1.3.1', required: true)
orc04_dep           = dependency('orc-0.4', version : '>=0.4.34', required: true)
gmodule20_dep       = dependency('gmodule-2.0', version : '>=2.74.4', required: true)
glib20_dep          = dependency('glib-2.0', version : '>=2.74.4', required: true)
gobject20_dep       = dependency('gobject-2.0', version : '>=2.74.4', required: true)
ffi_dep             = dependency('libffi', version : '>=3.2', required: true)
pcre2_dep           = dependency('libpcre2-8', version : '>=10.42', required: true)
zlib_dep            = dependency('zlib', version : '>=1.2', required: true)

libm = cc.find_library('m', required : true)

tsdemux_sources = [
  'src/mpegtspacketizer.c',
  'src/mpegtsbase.c',
  'src/mpegtsparse.c',
  'src/tsdemux.c',
  'src/gsttsdemux.c',
  'src/pesparse.c',
]

cdata = configuration_data()
cdata.set_quoted('GST_API_VERSION', api_version)
cdata.set_quoted('GETTEXT_PACKAGE', 'gstreamer-full-1.0')
cdata.set_quoted('PACKAGE_VERSION', meson.project_version())
cdata.set_quoted('GST_PACKAGE_ORIGIN', get_option('package-origin'))
cdata.set_quoted('GST_FULL_LICENSE', get_option('gstreamer-full-license'))
cdata.set_quoted('GST_PLUGIN_FULL_FEATURES_NAME', 'fullstaticfeatures')
cdata.set_quoted('VERSION', '1.22')
cdata.set_quoted('PACKAGE', 'gst-template-plugin')
cdata.set_quoted('GST_PACKAGE_NAME', 'GStreamer template Plug-ins')

configure_file(output : 'config.h', configuration : cdata)
configinc = include_directories('.')
gst_c_args = ['-DHAVE_CONFIG_H']

hawktsdemux = library('hawktsdemux',
                        tsdemux_sources,
                        c_args : ['-DGST_USE_UNSTABLE_API'] + gst_c_args,
                        include_directories : configinc,
                        dependencies : [gstcodecparsers_dep,
                                        gstmpegts_dep,
                                        gsttag_dep,
                                        gstpbutils_dep,
                                        gstaudio_dep,
                                        gstbase_dep,
                                        libunwind_dep,
                                        orc04_dep,
                                        gmodule20_dep,
                                        glib20_dep,
                                        gobject20_dep,
                                        ffi_dep,
                                        pcre2_dep,
                                        zlib_dep,
                                        libm],
                        install : true,
                        install_dir : plugins_install_dir,
)
