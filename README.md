# IPFS C++ HTTP API client library

[![Build CI Status](https://github.com/vasild/cpp-ipfs-http-client/actions/workflows/build_and_test.yml/badge.svg)](https://github.com/vasild/cpp-ipfs-http-client/actions/workflows/build_and_test.yml)
[![CodeQL](https://github.com/vasild/cpp-ipfs-http-client/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/vasild/cpp-ipfs-http-client/actions/workflows/codeql-analysis.yml)
[![codecov](https://codecov.io/gh/vasild/cpp-ipfs-http-client/branch/master/graph/badge.svg?token=4k5pulEnHE)](https://codecov.io/gh/vasild/cpp-ipfs-http-client)
[![Documentation](https://img.shields.io/badge/docs-doxygen-blue)](https://vasild.github.io/cpp-ipfs-http-client)
[![GitHub Issues](https://img.shields.io/github/issues/vasild/cpp-ipfs-http-client)](http://github.com/vasild/cpp-ipfs-http-client/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/vasild/cpp-ipfs-http-client)](https://github.com/vasild/cpp-ipfs-http-client/pulls)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/465/badge)](https://bestpractices.coreinfrastructure.org/projects/465)

![IPFS C++ HTTP Client Library](https://ipfs.io/ipfs/QmQJ68PFMDdAsgCZvA1UVzzn18asVcf7HVvCDgpjiSCAse)

Allows C++ applications to communicate with an [IPFS](https://ipfs.io) node.
It implements [IPFS API bindings](https://github.com/ipfs/interface-js-ipfs-core/blob/master/README.md#api) for C++.
See [the documentation](https://vasild.github.io/cpp-ipfs-http-client) and in partially the [Client Class](https://vasild.github.io/cpp-ipfs-http-client/classipfs_1_1Client.html).

See also [IPFS on GitHub](https://github.com/ipfs).

The C++ API is broken up into the following sections (Note: links below go to the `js-ipfs` project). The following calls are implemented in `cpp-ipfs-http-client`:

- [Bitswap](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/BITSWAP.md): *all methods are still to-do*
- [Block](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/BLOCK.md): get(), put(), stat()
- [Bootstrap](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/BOOTSTRAP.md): *all methods are still to-do*
- [Config](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/CONFIG.md): get(), set(), replace()
- [DAG](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/DAG.md): *all methods are still to-do*
- [DHT](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/DHT.md): findpeer(), findprovs()
- [Files](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/FILES.md): cat(), add(), ls()
- [Key](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/KEY.md): gen(), list(), rm()
- [Miscellaneous](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/MISCELLANEOUS.md): id(), version()
- [Name](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/NAME.md): *all methods are still to-do*
- [Object](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/OBJECT.md): new(), put(), get(), data(), links(), stat(), patch.addLink(), patch.rmLink(), patch.appendData(), patch.setData()
- [Pin](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/PIN.md): add(), ls(), rm()
- [PubSub](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/PUBSUB.md): *all methods are still to-do*
- [Refs](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/REFS.md): *all methods are still to-do*
- [Repo](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/REPO.md): stat()
- [Stats](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/STATS.md): bw(), repo() see Repo above
- [Swarm](https://github.com/ipfs/js-ipfs/blob/master/docs/core-api/SWARM.md): addrs(), connect(), disconnect(), peers()

As you can see, not all methods are yet implemented.

## TODO

- Implement the missing methods
- Contributors are welcome!

## Install

```sh
git clone https://github.com/vasild/cpp-ipfs-http-client.git
cd cpp-ipfs-http-client
cmake .
make -j 6
sudo make install
```

See the [documentation for details](https://vasild.github.io/cpp-ipfs-http-client).

## Dependencies

- [C++11 compiler](https://github.com/nlohmann/json#supported-compilers)
- [CMake](http://cmake.org)
- [libcurl](https://curl.haxx.se/libcurl)

## Build Test cases + Code Coverage

Test cases are build by default, but if you want to build with coverage:

```sh
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Debug -DCOVERAGE=ON -DBUILD_SHARED_LIBS=ON ..
# Run tests & Build the HTML report
make ctest_coverage_html -j 6

# Or run tests & create a Cobertura XML file
make ctest_coverage_xml -j 6
```

## Build Doxygen

Build Doxygen files locally. From the root directory of this project:

```sh
mkdir build
cd build
cmake -DDOC=ON ..
make doc
```

## Usage

```cpp
#include <iostream>
#include <sstream>

#include <ipfs/client.h>

int main(int, char**) {
  std::stringstream contents;

  ipfs::Client client("localhost", 5001);

  client.FilesGet("/ipfs/QmYwAPJzv5CZsnA625s3Xf2nemtYgPpHdWEz79ojWnPbdG/readme", &contents);

  std::cout << contents.str() << std::endl;

  return 0;
}
```

## Build via c++ compiler

```sh
c++ -std=c++11 -I/path/to/header -L/path/to/lib -lipfs-http-client myprog.cc -o myprog
```

## Build via CMake

An example using the CPP-IPFS project within *another* CMake project. For example via `git submodule` (but just `git clone` also works):

```sh
git submodule add https://github.com/vasild/cpp-ipfs-http-client.git lib/ipfs-http-client
```

Edit your `CMakeLists.txt` file to include CPP-IPFS-HTTP-client in the build:

```cmake
add_subdirectory (lib/ipfs-http-client)
```

Finally, add the CPP-IPFS static library to your target (in this example `${PROJECT_TARGET}` variable is used):

```cmake
target_include_directories(${PROJECT_TARGET} PRIVATE
    ${PROJECT_SOURCE_DIR}/lib/ipfs-http-client/include
)
target_link_libraries(${PROJECT_TARGET} PRIVATE ipfs-http-client)
```

## Contribute

Feel free to [open issues](https://github.com/vasild/cpp-ipfs-http-client/issues/new) and [pull requests](https://github.com/vasild/cpp-ipfs-http-client/compare).
Report vulnerabilities publicly, similar to other non-security issues.

The project adheres to the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html). Use [clang-format](http://clang.llvm.org/docs/ClangFormat.html) to properly format the code when you submit patches.

Write tests for new code. Changes should not cause the code coverage to go down (ideally up).

## License

The code is distributed under the [MIT License](http://opensource.org/licenses/MIT).
