# Learn OpenGL

This is a Meson-based project to be used with [Learn OpenGL](https://learnopengl.com).

## Getting started

### Prerequisites

- (Windows only) MSVC C++ Build Tools
- C/C++ compiler
- GNU/LLVM linker and binutils
- Python
- Ninja
- Meson

> [!NOTE]
> Works on Windows.

To use Clang and other LLVM tools (`llvm-ar` and `llvm-strip`):

```shell
meson setup --native-file clang.ini build
```

Else, if you want to use the GNU ones:

```shell
meson setup --native-file gcc.ini build
```

> [!NOTE]
> When naming the build directory, `build` is recommended over `builddir` as `build` is usually the name assumed by clangd and some other tools. Otherwise, you'll have to manually tell the location of the compilation database to clangd. Have a look at <https://clangd.llvm.org/config#compilationdatabase>.

## Building

Simply run:

```shell
meson compile -C build
```

You can find the executable (`main` or `main.exe`) under `build` directory.
