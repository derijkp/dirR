dirR
==== 
scripts to create a directory based, standalone/portable version of R with a number of packages
       Copyright Peter De Rijk (VIB/University of Antwerp)

dirR is a tool to create portable, self-contained binary version of R
that can be "installed" by just copying (or unpacking) a
directory anywhere on the host system, without interfering with the
system it is installed on, providing easy deployment with great
reproducibility on a wide range of systems:

* wide portability: binaries are compiled for wide compatibility (using
Holy Build Box): They will work on that centos7 cluster you still have
going somewhere (due to compatibility problems or similar) as well as on
the latest ubuntu.
* High reproducibility: You are using the same binaries with exactly the
same versions on all installs (It is typically hard to get exactly the
same package versions in different R installs, and even if the same
versions are instelled, there are sometimes differences in results)
* no depency hell: the correct versions of all dependencies (binaries
libraries, external tools) areincluded into one self-contained application
directory directory.
* Easy isolated install: just unpack a directory that comes with all
dependencies, does not interfere with the rest of the system, has no need
to set up environments, make permanent modifications to system
environment, ..
* multiple versions possible: easily use different versions next to each other
or even together by directly calling the binary in the directory of choice
* no root install/use: Can be run from anywhere in the filing system (no
root needed). The application directory can be included in the PATH, but a
softlink to the application executable in a directory in the PATH will
also work (dirR will find application directory based on the link)

Installing dirR
---------------
In a directory of choice, e.g. ~/bin, do
```
wget https://genomecomb.bioinf.be/download/extra/dirR-4.2.1-3-linux-x86_64.tar.gz
tar xvzf dirR-4.2.1-3-linux-x86_64.tar.gz
```

Using dirR
----------
You can use it directly from the directory, like
```
./dirR-4.2.1-linux-x86_64/R
```
or
* Put dirR-4.2.1-linux-x86_64 in your PATH
* Make a softlink (using any name you want) to dirR-4.2.1-linux-x86_64/R anywhere in PATH

Building dirR
-------------
dirR does not support the direct use of install.packages() from the dirR version.
If you want to use a different set of packages, you have to rebuild using an adaptation
of the build script build_dirR4.sh. 

The build process happens using docker in holy build box
(https://github.com/phusion/holy-build-box), which provides a stable and
compatible build environment (based on a centos7 container)

Make sure you can use docker, and then use the following command to build:
```
./build_dirR4.sh
```
By default this will build in the directory ~/build/bin-x86_64
with the result in ~/build/bin-x86_64/dirR-4.2.1-linux-x86_64

Adapting the build script
-------------------------
You can (copy,) change and run the build script to e.g. add or remove
packages, but as a build takes quite long, it can be useful to
interactively debug/test a build script using the following commmand:
```
./start_hbb3.sh
```
This starts up the centos7 based container with the development
environment providing shell access to it. You can copy-paste or source code
there to check what errors are given and correct them (without needed to
start over from the beginning)
In the docker build environment the dirR source can be accessed in /io, while
the build directory is accessed in /build

How to contact me
-----------------
I will do my best to reply as fast as I can to any problems, etc.
However, unfortunately the development of dirR is not my only task,
which is why my response might not be always as fast as you would
like.

Peter De Rijk
VIB - UAntwerp Center for Molecular Neurology
Universiteitsplein 1
B-2610 Antwerp

E-mail: Peter.DeRijk@gmail.com

Legalities
----------
dirR is Copyright Peter De Rijk, VIB/University of Antwerp, 2024

following terms apply to all files associated with the software unless
explicitly disclaimed in individual files.

The author hereby grant permission to use, copy, modify, distribute, and
license this software and its documentation for any purpose, provided that
existing copyright notices are retained in all copies and that this notice
is included verbatim in any distributions. No written agreement, license, or
royalty fee is required for any of the authorized uses. Modifications to
this software may be copyrighted by their authors and need not follow the
licensing terms described here, provided that the new terms are clearly
indicated on the first page of each file where they apply.

IN NO EVENT SHALL THE AUTHORS OR DISTRIBUTORS BE LIABLE TO ANY PARTY FOR
DIRECT, INDIRECT, SPECIAL, INCIDENTAL, OR CONSEQUENTIAL DAMAGES ARISING OUT
OF THE USE OF THIS SOFTWARE, ITS DOCUMENTATION, OR ANY DERIVATIVES THEREOF,
EVEN IF THE AUTHORS HAVE BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

THE AUTHORS AND DISTRIBUTORS SPECIFICALLY DISCLAIM ANY WARRANTIES,
INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT. THIS SOFTWARE IS
PROVIDED ON AN "AS IS" BASIS, AND THE AUTHORS AND DISTRIBUTORS HAVE NO
OBLIGATION TO PROVIDE MAINTENANCE, SUPPORT, UPDATES, ENHANCEMENTS, OR
MODIFICATIONS.
