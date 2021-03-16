# build-llvm-project

llvm project build shell script for macOS

```zsh
#!/usr/bin/env zsh

set -e

cd llvm-project

if [ -d build ]; then
  rm -rf build
fi

install_dir=/tmp/llvm

cmake -S llvm -B build -G Ninja \
    -DCMAKE_INSTALL_PREFIX=${install_dir} \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_OSX_DEPLOYMENT_TARGET=10.12 \
    -DLLVM_ENABLE_PROJECTS='clang;clang-tools-extra;libcxx;libcxxabi;libunwind;lldb;compiler-rt;lld;polly'

if [ -d ${install_dir} ]; then
  rm -rf ${install_dir}
fi

cmake --build build --target install
```
