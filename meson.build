project('hawktsdemux', 'c', version : '1.22.7.1', license : 'LGPL')
plugins_install_dir = join_paths(get_option('libdir'), 'gstreamer-1.0')
cc = meson.get_compiler('c')
gst_version = meson.project_version()
api_version = '1.0'
configinc = include_directories(['.', 'src'])

common_deps = []
gstcodecparsers_dep = dependency('gstreamer-codecparsers-1.0', version  : '>=1.22.7', required : true)
common_deps += gstcodecparsers_dep

gst_dep             = dependency('gstreamer-1.0', version : '>=1.22.7', required : true)
common_deps += gst_dep

gstbase_dep         = dependency('gstreamer-base-1.0', version : '>=1.22.7', required: true)
common_deps += gstbase_dep

gstmpegts_dep       = dependency('gstreamer-mpegts-1.0', version : '>=1.22.7', required: true)
common_deps += gstmpegts_dep

gsttag_dep          = dependency('gstreamer-tag-1.0', version : '>=1.22.7', required: true)
common_deps += gsttag_dep

gstpbutils_dep      = dependency('gstreamer-pbutils-1.0', version : '>=1.22.7', required: true)
common_deps += gstpbutils_dep

gstaudio_dep        = dependency('gstreamer-audio-1.0', version : '>=1.22.7', required: true)
common_deps += gstaudio_dep

m_dep = cc.find_library('m', required : true)
common_deps += m_dep

system_name = build_machine.system()
if system_name == 'linux'
  libunwind_dep       = dependency('libunwind', version : '>=1.3.1', required: true)
  common_deps += libunwind_dep

  orc04_dep           = dependency('orc-0.4', version : '>=0.4.34', required: true)
  common_deps += orc04_dep

  gmodule20_dep       = dependency('gmodule-2.0', version : '>=2.74.4', required: true)
  common_deps += gmodule20_dep

  glib20_dep          = dependency('glib-2.0', version : '>=2.74.4', required: true)
  common_deps += glib20_dep

  gobject20_dep       = dependency('gobject-2.0', version : '>=2.74.4', required: true)
  common_deps += gobject20_dep

  ffi_dep             = dependency('libffi', version : '>=3.2', required: true)
  common_deps += ffi_dep

  pcre2_dep           = dependency('libpcre2-8', version : '>=10.42', required: true)
  common_deps += pcre2_dep

  zlib_dep            = dependency('zlib', version : '>=1.2', required: true)
  common_deps += zlib_dep

elif system_name == 'darwin'
  message('macOS system')
elif system_name == 'windows'
  message('windows system')
else
  message('Unknown system')
endif

tsdemux_sources = files([
  'src/mpegtspacketizer.c',
  'src/mpegtsbase.c',
  'src/mpegtsparse.c',
  'src/tsdemux.c',
  'src/gsttsdemux.c',
  'src/pesparse.c',
])

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
                        dependencies : common_deps,
                        install : true,
                        install_dir : plugins_install_dir,
)
