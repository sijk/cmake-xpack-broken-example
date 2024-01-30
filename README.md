`cmake-xpack` has broken argument parsing on Windows. I have provided two
examples that I've come across. I suspect that this is because of the patches
xpack applies to cmake to run processes inside `cmd`, which alters the way
arguments are parsed. Whatever the reason, cmake-xpack is broken on Windows and
there is no workaround.

I suggest testing with the following builds, since it's a direct comparison
between the latest xpack-cmake and the corresponding upstream version.
- https://github.com/xpack-dev-tools/cmake-xpack/releases/download/v3.26.5-1/xpack-cmake-3.26.5-1-win32-x64.zip
- https://github.com/Kitware/CMake/releases/download/v3.26.5/cmake-3.26.5-windows-x86_64.zip


# Example 1

    cd example1
    cmake .
    cmake --build .

If you run this with upstream cmake it works fine. If you run it with
cmake-xpack you get an error about `fatal: ambiguous argument 'HEAD0'`
because the xpack build of cmake parses `HEAD^0` as `HEAD0`.

# Example 2

    cd example2
    cmake . -DPython_EXECUTABLE=C:/Python/python.exe

You'll need to provide a valid path to a python interpreter as that last
argument, of course. If you run this with upstream cmake it works fine. If you
run it with cmake-xpack you get an error about `list GET given empty list`
because FindPython runs a command internally to inspect the python interpreter,
and the arguments to that command get passed incorrectly by the xpack build of
cmake.

