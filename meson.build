project(
    'learnopengl',
    'c',
    'cpp',
    version: '0.1.0',
    meson_version: '>= 1.3.0',
    default_options: [
        'warning_level=3',
        'c_std=gnu11',
        'cpp_std=c++17',
        'buildtype=debug',
    ],
)

include_directories = include_directories('include')
src_files = files(
    'src/glad.c',
    'src/main.cpp',
)

cc = meson.get_compiler('c')

# subdir('src')

# Dependencies
m_dep = cc.find_library('m', required: false)
rt_dep = cc.find_library('rt', required: false)
glfw_dep = dependency('glfw3', default_options: ['default_library=static'])
glm_dep = dependency('glm')
opengl_dep = []

if host_machine.system() == 'windows'
    opengl_dep = cc.find_library('opengl32', required: true)
endif

deps = [
    glfw_dep,
    glm_dep,
    opengl_dep,
]

if m_dep.found()
    deps += m_dep
endif

if rt_dep.found()
    deps += rt_dep
endif

# Targets
executable(
    'main',
    sources: src_files,
    include_directories: include_directories,
    dependencies: deps,
)

run_clang_tidy = find_program('run-clang-tidy', 'run-clang-tidy.py', 'clang-tidy', required: false)

if run_clang_tidy.found()
    # 2. Define the custom run_target
    run_target(
        'lint',
        command: [
            run_clang_tidy,
            '-use-color',
            '-p', meson.project_build_root(), # Point to the compilation database
            '-checks=-*,bugprone-*', # Enable ONLY bugprone rules
            '-warnings-as-errors=bugprone-*', # Upgrade bugprone rules to hard compilation errors
            src_files,
        ],
    )
endif
