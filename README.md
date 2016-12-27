# example-boost-poco
A simple example app using Boost and Poco C++ libraries, as an example to conan as a consumer.

This application uses Poco threads and Boost regex functionalities.

# How to install dependencies

We need both Boost and Poco libraries to compile our app.

We will use conan C/C++ package manager to install dependencies. The following command will use your default compiler, in the example it uses VS14-64 in Win.

First inspect the contents of ``conanfile.txt``, it defines the dependencies to be installed, and the ``cmake`` generator, because we will be using cmake in our example.

```bash
$ mkdir build && cd build
$ conan install ..
```

This will install all the dependencies, not only Boost and Poco, but also **transitive dependencies**, like ZLib or OpenSSL, which are required by Poco or Boost.

We can inspect what is installed in the conan local cache (so they don't have to be installed again, and can be used in other projects too):

```bash
$ conan search
# Also specific information of binaries installed for a certain package
$ conan search Poco/1.7.2@lasote/stable
```

The ``search`` shows information of everything that is installed in the local cache. If we want to inspect the dependency graph of our project:

```bash
$ conan info ..
```

Now inspect the 2 files that have been generated:

- conaninfo.txt shows the install information, the actual settings and options values that have been used
- conanbuildinfo.cmake contains some cmake variables and macros with useful values that we can use to build our app

If you have a look at ``CMakeLists.txt`` you will see how this generated file is included in your build script and used.

Lets build and run it:

```bash
$ cmake .. -G "Visual Studio 14 Win64"
$ cmake --build . --config Release
$ bin/timer
```

Now you can repeat the process, for example to create a 32bits app:

```bash
$ rm -rf *
$ conan install .. -s arch=X86
$ cmake .. -G "Visual Studio 14"
$ cmake --build . --config Release
$ bin/timer
```

Try what happens if you use a random ``arch`` value.

Also you can inspect your installed binaries:

```bash
$ conan search Poco/1.7.2@lasote/stable
```