
# TensorFlow windows builds with AVX/AVX2 extensions

Checkout the [releases](https://github.com/faisalthaheem/tensorflow-windows/releases) section for the python wheels.

TF Version|Python Version|Instruction set|GPU Enabled|Link
-------|----|----|----|-----------
1.8.0|3.5.3|AVX2|| [tensorflow-1.8.0-cp35-cp35m-win_amd64.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.8.0/tensorflow-1.8.0-cp35-cp35m-win_amd64.whl)
1.7.1|3.5.3|AVX2|| [tensorflow-1.7.1-cp35-cp35m-win_amd64.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.7.1/tensorflow-1.7.1-cp35-cp35m-win_amd64.whl)
1.7.0|3.5.3|AVX2|| [tensorflow-1.7.0-cp35-cp35m-win_amd64.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.7.0/tensorflow-1.7.0-cp35-cp35m-win_amd64.whl)
1.7.0|3.5.3|AVX2|Yes| [tensorflow_gpu-1.7.0-cp35-cp35m-win_amd64-avx2-cuda9.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.7.0/tensorflow_gpu-1.7.0-cp35-cp35m-win_amd64-avx2-cuda9.whl)
1.6.0|3.5.3|AVX2|| [tensorflow-1.6.0-cp35-cp35m-win_amd64-avx2.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.6.0/tensorflow-1.6.0-cp35-cp35m-win_amd64-avx2.whl)
1.5.1|3.5.3|AVX2|| [tensorflow-1.5.1-cp35-cp35m-win_amd64-avx2.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.5.1/tensorflow-1.5.1-cp35-cp35m-win_amd64-avx2.whl)
1.4.0|3.5.3|AVX2|| [tensorflow-1.4.0-cp35-cp35m-win_amd64.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.4/tensorflow-1.4.0-cp35-cp35m-win_amd64.whl)
1.4.0|3.5.3|AVX|| [tensorflow-1.4.0-cp35-cp35m-win_amd64-avx.whl](https://github.com/faisalthaheem/tensorflow-windows/releases/download/1.4/tensorflow-1.4.0-cp35-cp35m-win_amd64-avx.whl)


# Build Environment

Environment|Version
-------|----
OS|Windows 10 x64
Visual Sutdio|2017 Community Edition for CPU only builds & 2015 Community Edition for CUDA enabled builds
CMAKE|3.9.0
SWIG|swigwin-3.0.12
Python|3.5.3

Followed official guide at 
[https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/cmake/README.md](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/cmake/README.md)

# Build Commands

CMAKE Configuration Command for AVX/AVX2 non CUDA Builds using VS 2017

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

Or when using CUDA, use the following command to build using toolchain 140 with VS 2015

    cmake.exe .. ^
    -A x64 ^
    -G "Visual Studio 14 2015" -T v140 ^
    -DSWIG_EXECUTABLE="C:/tools/swigwin-3.0.12/swig.exe" ^
    -DPYTHON_EXECUTABLE="C:/Program Files/Python35/python.exe" ^
    -DCMAKE_BUILD_TYPE=Release ^
    -DPYTHON_LIBRARIES="C:/Program Files/Python35/libs/python35.lib" ^
    -Dtensorflow_BUILD_PYTHON_TESTS=OFF ^
    -Dtensorflow_BUILD_CC_TESTS=OFF ^
    -Dtensorflow_TF_NIGHTLY=OFF ^
    -Dtensorflow_WIN_CPU_SIMD_OPTIONS=/arch:AVX2 ^
    -Dtensorflow_ENABLE_GPU=ON ^
    -DCUDNN_HOME="C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0"

Build with following command using "**Developer Command Prompt for VS 2017**" or "**Developer Command Prompt for VS 2015**"

    msbuild.exe /p:Configuration=Release /maxcpucount:1 /verbosity:minimal tf_python_build_pip_package.vcxproj

Make sure 64bit build tools are used, rename "**Hostx64**" to "**Hostx86**" at following default install location for VS 2017

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.11.25503\bin

and for VS 2015 rename "**amd64**" to "**x86_amd64**" at the following default install location
    
    C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin
