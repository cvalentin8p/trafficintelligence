Information for installation and development is provided by default for Linux (in particular the Ubuntu distribution, and more generally any Debian-based distribution). 

# Installation
## OpenCV Library
**Very important**, the code has been updated to OpenCV 3.x and works with OpenCV 4.x, and can be compiled simply with the repository version of the OpenCV libraries, at least on Ubuntu. It is sufficient to install the `libopencv-dev` package. 

Otherwise, one needs to compile OpenCV from source. The installation instructions are provided on this [page](http://docs.opencv.org/master/df/d65/tutorial_table_of_content_introduction.html) on the OpenCV website. On Ubuntu, the C/C++ GNU compiler is provided in the `build-essential` package. It is important to get the development version of all the required libraries (`-dev` packages). Depending on your version of Ubuntu, the ffmpeg packages `libavformat-dev`, `libavcodec-dev`, `libswscale-dev` may be sufficient for OpenCV. Look for any compilation error or mention in the output of `cmake .` related to ffmpeg (other useful packages is `libavutil-dev`, while `libavresample-dev` seems to have been replaced by `libswscale-dev`). If issues persist after installing all ffmpeg-related packages, one solution is to install ffmpeg from source: do not install all the other libraries, unless you want some specific codec support, eg x264. Video codecs should be available in the `ubuntu-restricted-extras`. 

For Python, one needs the `python3-dev` to compile the Python bindings as well (and numpy somewhere). 

You should compile the code in a different directory than the base source directory, e.g. in a sub-directory (`build` or `release`). Once the compilation is configured using CMake (check optimization options, whether or not to get the compiled samples and to install them), you should verify the output of `cmake .` to know what package may be missing. The command line steps are the following (once you are in the main OpenCV source directory):

```sh
$ mkdir release
$ cd release
$ ccmake .. (interactive)
OR $ cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..
$ make
$ sudo make install
```

On Windows, the [MinGW tools](http://tdm-gcc.tdragon.net/) are recommended. 

## Mercurial
The code is now self-hosted since Bitbucket abandoned Mercurial. Clone the repository with the following command:

```
$ hg clone https://hg.reactionary.software/repo/traffic-intelligence/ <destination directory>
```

Note that using Mercurial will make it easier to update your code and enable you to contribute more easily to the project. For more information, see [PolyWikiTI](http://www.polymtl.ca/wikitransport/index.php?title=Mercurial).

## Library for Trajectory Management 
The library was initially developed in 2010 by [Piotr Bilinski](http://www.piotr-bilinski.com/) and provides I/O functions (saving to a SQLite database) and several trajectory distances implemented. It was previously hosted on [Bitbucket](https://bitbucket.org/trajectories/trajectorymanagementandanalysis) and is now included in the Traffic Intelligence repository for simplicity.

It relies on [SQLite](https://www.sqlite.org) which can be installed both easily from the Ubuntu repository (do not forget the dev packages). It relies on [CppUnit](http://apps.sourceforge.net/mediawiki/cppunit/) for unit testing, but this can be skipped if only compiling the library. Once Traffic Intelligence downloaded or cloned, go to the `trajectorymanagement` directory and compile the library using the following commands (if not using cppunit, simply provide empty values for the library location):

```sh
$ ccmake .
$ make TrajectoryManagementAndAnalysis
```

## Traffic Intelligence Feature Tracker
If you got OpenCV to compile (or installed from the repository) and have mercurial installed, you need to install some extra libraries: some libraries of the [Boost project](https://www.boost.org) and the Trajectory Management project (see above). The project relies on the following Boost libraries: Foreach, Graph, Program Options, Smart Ptr and optionally Test. Program Options, Test, File System and System have to be compiled (or their compiled libraries need to be downloaded from the Ubuntu repository), the others being header only.

```sh
$ sudo apt install libboost-dev libboost-program-options-dev libboost-graph-dev libboost-filesystem-dev libboost-system-dev
```

The C++ code of feature-based tracker will now be compiled in the cloned Traffic Intelligence directory. The make utility is used to automatically build the executable programs from the source code. Makefiles are files that specify how to derive the target program from each of its dependencies. The explanation of this tool is beyond the scope of this document (See the [Wikipedia page](http://en.wikipedia.org/wiki/Make_(software))). A Makefile is provided to compile the Traffic Intelligence project only on Linux for now (the specific one for C++ is in the `c` sub-directory). When typing `make` in a directory, where the Makefile is, it will automatically use it. Otherwise, the Makefile to use can be specified with the `-f` option. The simplest thing is to compile the C++ executables by going in the `c` sub-directory and type `make [target]` where `target` can be `feature-based-tracking`. The executables are put in the `bin` sub-directory. Other targets are: 

* `tests`: this compiles tests into an executable `tests` and runs it.
* `doc`: this generates the code documentation using the Doxygen tool (install the [Doxygen](https://www.doxygen.org) tool with `sudo apt install doxygen` and it is equivalent to type `doxygen` in the main directory).
* `dist`: _TODO_ this compiles the executable, generates the user manual and bundles an archive for the program distribution. 
* `clean`: this cleans the compiled code (the object files and the executables). 

In addition, there are options when compiling the code

* `DEBUG` (default 0): set to 1 to compile with debug symbols for debugging under [GDB](https://www.gnu.org/software/gdb/).
* `OPENCV` (default 1): this controls the compilation with or without OpenCV dependencies (not everything will obviously be therefore available).

On Linux, completion for Makefile targets is automatic. You may have to change some paths in the Makefile, in particular the `TRAJECTORYMANAGEMENT_DIR` variable to point where the library for Trajectory Management has been copied or cloned (it should point to the directory that contains the src directory that contains `Trajectory.h` and should work by default now it is in the same repository). The `OPENCV_HOME` should be changed to `OPENCV_HOME=/usr` if OpenCV was installed from the repository. 

A tip for faster compilation is to call make with the option `-j [N]` where `N` is the number of threads. It should match the number of processors (or cores for multi-core processors) on your computer. This may slowdown your computer significantly. 

# User Manual
The interface is based on the command line. All options are described by using the help option (`-h` or `--help`).
