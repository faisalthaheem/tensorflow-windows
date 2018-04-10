
# TensorFlow windows builds with AVX/AVX2 extensions

Checkout the [releases](https://github.com/faisalthaheem/tensorflow-windows/releases) section for the python wheels.

tensorflow version|Python Version|Instruction set|Link
-------|----|----|-----------
1.7.0|3.5.3|AVX2| [tensorflow-1.7.0-cp35-cp35m-win_amd64.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.7.0/tensorflow-1.7.0-cp35-cp35m-win_amd64.whl)
1.6.0|3.5.3|AVX2| [tensorflow-1.6.0-cp35-cp35m-win_amd64-avx2.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.6.0/tensorflow-1.6.0-cp35-cp35m-win_amd64-avx2.whl)
1.5.1|3.5.3|AVX2| [tensorflow-1.5.1-cp35-cp35m-win_amd64-avx2.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.5.1/tensorflow-1.5.1-cp35-cp35m-win_amd64-avx2.whl)
1.4.0|3.5.3|AVX2| [tensorflow-1.4.0-cp35-cp35m-win_amd64.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.4/tensorflow-1.4.0-cp35-cp35m-win_amd64.whl)
1.4.0|3.5.3|AVX| [tensorflow-1.4.0-cp35-cp35m-win_amd64-avx.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.4/tensorflow-1.4.0-cp35-cp35m-win_amd64-avx.whl)


# Build Environment

Environment|Version
-------|----
OS|Windows 10 x64
Visual Sutdio|2017 Community Edition
CMAKE|3.9.0
SWIG|swigwin-3.0.12
Python|3.5.3

Followed official guide at 
[https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/cmake/README.md](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/cmake/README.md)

# Build Commands

CMAKE Configuration Command

    cmake.exe .. ^
    -A x64 ^
    -G "Visual Studio 15 2017" ^
    -DSWIG_EXECUTABLE="c:/swigwin-3.0.12/swig.exe" ^
    -DPYTHON_EXECUTABLE="c:/py/35/python.exe" ^
    -DCMAKE_BUILD_TYPE=Release ^
    -DPYTHON_LIBRARIES="c:/py/35/libs/python35.lib" ^
    -Dtensorflow_BUILD_PYTHON_TESTS=OFF ^
    -Dtensorflow_BUILD_CC_TESTS=OFF ^
    -Dtensorflow_TF_NIGHTLY=OFF ^
    -Dtensorflow_WIN_CPU_SIMD_OPTIONS=/arch:AVX2

Build with following command using "**Developer Command Prompt for VS 2017**"

    msbuild.exe /p:Configuration=Release /maxcpucount:1 /verbosity:minimal tf_python_build_pip_package.vcxproj

Make sure 64bit build tools are used, rename "**Hostx64**" to "**Hostx86**" at location

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.11.25503\bin
