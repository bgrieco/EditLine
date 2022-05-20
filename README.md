# Editline
A fork from https://www.thrysoee.dk/editline/ modified to be built with CMake

The source comes from libedit-20210910-3.1.tar.gz

I added a .1 patch to the release number so that is differentiated from the original

## Copyright
Since the original Editline library was published under the BSD License, it allows me to redistribute and alter the code granted I provide the original Copyright

## Disclaimer
This library was originally designed to be built using GNU Autoconf.
I modified it to use CMake instead.
The original files and modifications may be tracked through the commits to this repository

## Building
Building should be straightforward for those with CMake experience.
Once downloaded:

```
cmake .
```

will generate the required files, and 
```
make
```

will build the project

There is no install command yet. The idea is to add this directory with a cmake

```
add_subdirectory( ... path to .../Editline )
```
and the build system should be able to figure things out for itself.

## Known Problems
- The GNU autoconf system would have scanned all files and generated a config.h with the required specifications. This doesn't happen with CMake. 
Instead:
  - this configuration uses a config.h generated in Mac OS X. 
  - To circumvene this problem, some files were altered from the original (check the commits).
- It does not work with windows. Check the WinEditLine project instead. (link will be updated)

## Updates and Releases
Even though I ported EditLine to work with CMake, I have no intent in supporting it or updating it so that it matches the original version.
I am not a CMake fan and I consider my knowledge of the tool to be somewhat in the **Beginners** level
That said, **I will try to help you** as much as I can, and requests may be created as issues.

21-May-2022

Bruno Grieco
