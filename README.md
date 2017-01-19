# bxprotobuftools

bxprotobuftools - Tools for *Protobuf* based serialization (C++ library)

The   ``bxprotobuftools``   library   (also   ``BxProtobuftools``   or
``Bayeux/Protobuftools``)  consists  in  a  set  of  C++  classes  and
utilities for serialization based on  the Google Protocol Buffers API.
It  aims to  be integrated  as a  companion module  of the  Bayeux C++
library (the foundation library  of the SuperNEMO physics experiment's
software).


This is a very preliminary work, not ready for production yet...
Some documentation and examples are still needed too.

bxjsontools  has been  initiated  in the  framework  of the  SuperNEMO
physics experiment software.

**Note for SuperNEMO users**:

Protobuf  based serialization  is used  by  the Vire  C++ library  for
communication between C++ and Java implemented services related to the
Control and Monitoring  System  (CMS)  of the SuperNEMO experiment.


## Dependencies and inspiration

bxprotobuftools depends on the Google Protocol Buffers library:
* the Google Protocol Buffers library version 3.0.0 (https://developers.google.com/protocol-buffers/)

  **Note:** bxprotobuftools provides its own ``FindProtobuf.cmake`` CMake script because
  the one provided by CMake 3.5 (``/usr/share/cmake-3.5/Modules/FindProtobuf.cmake``) does
  not suit our needs.

* the Boost C++ library 1.60 (http://www.boost.org/) (optional, activated by default and mandatory for SuperNEMO software)

It is inspired by a former related work:
* ``Bayeux/Jsontools`` (https://github.com/BxCppDev/bxjsontools)

Needed tools and software (tested on Ubuntu 16.04 LTS):
* You need CMake version >= 2.8 (former version may work)
* You need gcc version >= 4.8.4 (former version may work)
* Some parts of bxprotobuftools may depend on Boost 1.60 (former version may work). This can be inhibited at configuration (see 'CMake options' below).

## License:

See the ``LICENSE.txt`` file.


## Build and install:

The  following  instructions  illustrate  how  to  build  and  install
bxprotobuftools on  a Linux  system (Ubuntu 16.04  LTS). It  should be
easy to adapt for a MacOS X system.

CMake options:
* ``BXPROTOBUFTOOLS_WITH_BOOST`` (default: ``ON``) : interface with some part(s)
  of the Boost C++ library.
* ``BXPROTOBUFTOOLS_ENABLE_TESTING`` (default: ``ON``) : builds the test program(s).

### Download the source code from GitHub:
```sh
$ mkdir -p /tmp/${USER}/bxprotobuftools/_source.d/
$ cd /tmp/${USER}/bxprotobuftools/_source.d/
$ git clone https://github.com/fmauger/bxprotobuftools.git
```
### Build the library from a dedicated directory:

Make sure you have a proper installation of the Google Protocol Buffer
(C++)  library version  3.0.0 and  companion tools  (``protoc``).  You
must also have an installation of the Boost library.

**Note for SuperNEMO users:**

The SuperNEMO experiment data  processing and simulation software uses
Cadfaelbrew    (https://github.com/SuperNEMO-DBD/cadfaelbrew)    which
provides some core software tools  and libraries (C++ compiler, Boost,
GSL, ROOT libraries...).  Before to build and install BxProtobuftools,
you must switch to a brew shell before:

```sh
$ brew sh
```

We assume  here that you  want to install ``bxprotobuftools``  in your
home directory:

```sh
$ mkdir -p /tmp/${USER}/bxprotobuftools/_build.d/
$ cd  /tmp/${USER}/bxprotobuftools/_build.d/
$ cmake \
    -DCMAKE_INSTALL_PREFIX=${HOME}/sw/bxprotobuftools/install-0.1.0 \
    -DPROTOBUF_ROOT:PATH="installation/path/of/protobuf/version/3.0" \
    -DBoost_DIR="installation/of/Boost/version/1.60" \
    /tmp/${USER}/bxprotobuftools/_source.d/bxprotobuftools/
$ make
$ make test
$ make install
```

Note the use  of the ``PROTOBUF_ROOT`` and  ``Boost_DIR`` variables to
help CMake to find the Protobuf and Boost dependee libraries.


### Enjoy bxprotobuftools from its installation directory:
```sh
$ cd ${HOME}/sw/bxprotobuftools/install-0.1.0
$ LANG="C" tree .
.
|-- bin
|   `-- bxprotobuftools-query
|-- include
|   `-- bayeux
|       |-- proto
|       |   `-- protobuftools
|       |       |-- SimpleOptional.pb.h
|       |       |-- SimpleOptional.proto
|       |       |-- TimePeriod.pb.h
|       |       `-- TimePeriod.proto
|       `-- protobuftools
|           |-- base_type_converters.h
|           |-- bool_converter.h
|           |-- boost_converters.h
|           |-- boost_datetime_converters.h
|           |-- boost_optional_converter.h
|           |-- config.h
|           |-- core.h
|           |-- double_converter.h
|           |-- enum_converter.h
|           |-- exception.h
|           |-- float_converter.h
|           |-- i_protobufable.h
|           |-- int16_converter.h
|           |-- int32_converter.h
|           |-- int64_converter.h
|           |-- int8_converter.h
|           |-- io-inl.h
|           |-- io.h
|           |-- iofile-inl.h
|           |-- iofile.h
|           |-- logger.h
|           |-- logger_macros.h
|           |-- node-inl.h
|           |-- node.h
|           |-- protobuf_factory.h
|           |-- protobuf_utils.h
|           |-- protobufable_converter.h
|           |-- protobuftools.h
|           |-- protobuftools_stubs.h
|           |-- std_array_converter.h
|           |-- std_list_converter.h
|           |-- std_set_converter.h
|           |-- std_string_converter.h
|           |-- std_type_converters.h
|           |-- std_vector_converter.h
|           |-- uint16_converter.h
|           |-- uint32_converter.h
|           |-- uint64_converter.h
|           |-- uint8_converter.h
|           `-- version.h
|-- lib
|   |-- cmake
|   |   `-- BxProtobuftools-0.1.0
|   |       |-- BxProtobuftoolsConfig.cmake
|   |       |-- BxProtobuftoolsConfigVersion.cmake
|   |       |-- BxProtobuftoolsTargets-noconfig.cmake
|   |       `-- BxProtobuftoolsTargets.cmake
|   `-- libBayeux_protobuftools.so
`-- share
    `-- BxProtobuftools-0.1.0
        |-- LICENSE.txt
        `-- examples
            `-- ex01
                |-- BarMsg.proto
                |-- CMakeLists.txt
                |-- FooMsg.proto
                |-- README.md
                |-- bar.cc
                |-- bar.h
                |-- ex01.cxx
                |-- ex01.sh
                |-- foo.cc
                `-- foo.h
```

## Using bxprotobuftools:

* The ``bxprotobuftools-query`` utility allows you to fetch informations about your
  BxProtobuftools installation. You may add the following typical line in your
``~/.bashrc`` profile:
```sh
export PATH="${HOME}/sw/bxprotobuftools/install-0.1.0/bin:${PATH}"
```
  This will give you access to the ``bxprotobuftools-query`` command-line utility:
```sh
$ bxprotobuftools-query --help
```
* CMake  configuration  scripts (i.e. ``BxProtobuftoolsConfig.cmake`` and ``BxProtobuftoolsConfigVersion.cmake``) are provided for client
  software. The CMake ``find_package(BxProtobuftools REQUIRED CONFIG)`` command can be given
  the following variable to find the BxProtobuftools installation on your system:
```sh
$ cmake ... -DBxProtobuftools_DIR="$(bxprotobuftools-query --cmakedir)" ...
```
* There is  a simple example  ``ex01`` that illustrates a  very simple usecase.



## To do:

* Add ``converter`` template class for ``std::map`` container with simple layout.
* Add  ``converter`` template  class  for a  few  useful classes  from
   ``boost::date_time`` mapped using the ``google.protobuf.Timestamp``
   message.
* Add support for ``boost::variant`` template class mapped to some *oneof* fields (is it possible?).
