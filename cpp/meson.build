# project name: cpp, language: cpp, default_options...
project('cpp', 'cpp', default_options : ['cpp_std=c++17'])
add_global_arguments('-DSOME_TOKEN=value', language : 'cpp')

cc = meson.get_compiler('cpp')
# Using absolute path for now
lib_rust = cc.find_library('rust', dirs : ['/home/lee/Code/Projects/cpp-call-rust/rust/target/release'])
inc_rust = include_directories('/home/lee/Code/Projects/cpp-call-rust/rust/src')

executable('cpp', 'main.cpp', dependencies: [lib_rust], include_directories: [inc_rust])
# Using .hpp will cause build error, not sure why
