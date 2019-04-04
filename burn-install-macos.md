
## BiasedUrn: Mac OS installation

The majority of Mac OS machines do not provide basic developer tools, e.g., the GNU Compiler Collection (gcc), a Fortran compiler, a TeX distribution, etc., to compile R source code. To identify and obtain these developer tools, please refer to the section entitled "Building R from sources" in the [R for Mac OS X FAQ](http://cran.r-project.org/bin/macosx/RMacOSX-FAQ.html).  

Please note that different Mac OS versions might require different sets of developer tools. Also, note that the same developer tools used to compile R from source are also required to compile R library packages. Once the appropriate set of developer tools are installed, instructions for modifying, compiling, and installing the modified BiasedUrn package are identical to those described in the [Linux section of this document](#linux).

### modify

We will use shell commands within a terminal to edit, recompile, and install the package. First, change directories to that which contains the BiasedUrn package source code. Here, we assume this directory is called <tt>Downloads</tt> and is found under our home directory (i.e. <tt>~/Downloads/</tt>).

<pre>John-Does-MacBook-Pro:~ jdoe$ cd ~/Downloads
</pre>

Next, use the <tt>tar</tt> command to extract the BiasedUrn source code.

<pre>John-Does-MacBook-Pro:Downloads jdoe$ tar -zxf BiasedUrn_1.04.tar.gz 
</pre>

The default contents of the <tt>Makevars</tt> file within the package <tt>src</tt> directory is displayed here:

<pre>John-Does-MacBook-Pro:Downloads jdoe$ cat BiasedUrn/src/Makevars
# Makevars for BiasedUrn
# The value of MAXCOLORS may be modified
PKG_CPPFLAGS= -DR_BUILD=1 -DMAXCOLORS=32
</pre>

Using any text editor, change the value of <tt>MAXCOLORS</tt> from 32 to 10000\. After performing this edit and saving the changes, the file should look like this:

<pre>John-Does-MacBook-Pro:Downloads jdoe$ cat BiasedUrn/src/Makevars
# Makevars for BiasedUrn
# The value of MAXCOLORS may be modified
PKG_CPPFLAGS= -DR_BUILD=1 -DMAXCOLORS=10000
</pre>

### check

Before building the package, one should execute the `R check` script to resolve any problems that may arise from compiling the package, e.g., missing developer tools. The command line execution of this step along with example output is shown here:

<pre>John-Does-MacBook-Pro:Downloads jdoe$ R CMD check BiasedUrn
* using log directory '/Users/jdoe/Downloads/BiasedUrn.Rcheck'
* using R version 2.15.0 (2012-03-30)
* using platform: x86_64-apple-darwin9.8.0 (64-bit)
* using session charset: UTF-8
...
* checking running R code from vignettes ... OK
* checking re-building of vignette PDFs ... OK
* checking PDF version of manual ... OK
</pre>

The full output generated from the <tt>check</tt> command can be found in the log file <tt>BiasedUrn.Rcheck/00check.log</tt>.

### build

Next we use the build command to compile the modified package and create an installable package file. This step will overwrite the original source file <tt>BiasedUrn_1.04.tar.gz</tt> with the installable modified package file.

<pre>John-Does-MacBook-Pro:Downloads jdoe$ R CMD build BiasedUrn
* checking for file 'BiasedUrn/DESCRIPTION' ... OK
* preparing 'BiasedUrn':
* checking DESCRIPTION meta-information ... OK
* cleaning src
* installing the package to re-build vignettes
* creating vignettes ... OK
* cleaning src
* checking for LF line-endings in source and make files
* checking for empty or unneeded directories
* building 'BiasedUrn_1.04.tar.gz'
</pre>

The final step is to install this modified package. If you have root privileges, a global install can be performed; otherwise, installation to a local directory tree can be performed. Next we describe these two cases.

### global install with root privileges

If you have root or sudo privileges and wish to make the new package available system-wide, then perform this action as superuser. Here we demonstrate this using the <tt>sudo</tt> command. Similarly, one could also perform this action from a root shell.

<pre>John-Does-MacBook-Pro:Downloads jdoe$ sudo R CMD INSTALL BiasedUrn

WARNING: Improper use of the sudo command could lead to data loss
or the deletion of important system files. Please double-check your
typing when using sudo. Type "man sudo" for more information.

To proceed, enter your password, or type Ctrl-C to abort.

Password:
* installing to library '/Library/Frameworks/R.framework/Versions/2.15/Resources/library'
* installing *source* package 'BiasedUrn' ...
file 'src/Makevars' has the wrong MD5 checksum
** libs
*** arch - i386
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c fnchyppr.cpp -o fnchyppr.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc1.cpp -o stoc1.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc3.cpp -o stoc3.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stocR.cpp -o stocR.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn1.cpp -o urn1.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn2.cpp -o urn2.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c wnchyppr.cpp -o wnchyppr.o
g++ -arch i386 -dynamiclib -Wl,-headerpad_max_install_names -undefined dynamic_lookup -single_module -multiply_defined suppress -L/usr/local/lib -o BiasedUrn.so fnchyppr.o stoc1.o stoc3.o stocR.o urn1.o urn2.o wnchyppr.o -F/Library/Frameworks/R.framework/.. -framework R -Wl,-framework -Wl,CoreFoundation
installing to /Library/Frameworks/R.framework/Versions/2.15/Resources/library/BiasedUrn/libs/i386
*** arch - x86_64
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c fnchyppr.cpp -o fnchyppr.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc1.cpp -o stoc1.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc3.cpp -o stoc3.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stocR.cpp -o stocR.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn1.cpp -o urn1.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn2.cpp -o urn2.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c wnchyppr.cpp -o wnchyppr.o
g++ -arch x86_64 -dynamiclib -Wl,-headerpad_max_install_names -undefined dynamic_lookup -single_module -multiply_defined suppress -L/usr/local/lib -o BiasedUrn.so fnchyppr.o stoc1.o stoc3.o stocR.o urn1.o urn2.o wnchyppr.o -F/Library/Frameworks/R.framework/.. -framework R -Wl,-framework -Wl,CoreFoundation
installing to /Library/Frameworks/R.framework/Versions/2.15/Resources/library/BiasedUrn/libs/x86_64
** R
** demo
** inst
** preparing package for lazy loading
** help
*** installing help indices
** building package indices
** installing vignettes
   'UrnTheory.Rtex' 
** testing if installed package can be loaded
*** arch - i386
*** arch - x86_64

* DONE (BiasedUrn)
</pre>

### install to local account

In the event one does not have root privileges, a local version of the package can be installed and used from the user account. Ensure that you have a directory set for local package installations; here we have created the directory <tt>~/R/library/</tt> for this purpose. In the output from this command you should see a line indicating installation to this local directory:

<pre>John-Does-MacBook-Pro:Downloads jdoe$ R CMD INSTALL BiasedUrn --library=~/R/library/
* installing *source* package 'BiasedUrn' ...
file 'src/Makevars' has the wrong MD5 checksum
** libs
*** arch - i386
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c fnchyppr.cpp -o fnchyppr.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc1.cpp -o stoc1.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc3.cpp -o stoc3.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stocR.cpp -o stocR.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn1.cpp -o urn1.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn2.cpp -o urn2.o
g++ -arch i386 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/i386 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c wnchyppr.cpp -o wnchyppr.o
g++ -arch i386 -dynamiclib -Wl,-headerpad_max_install_names -undefined dynamic_lookup -single_module -multiply_defined suppress -L/usr/local/lib -o BiasedUrn.so fnchyppr.o stoc1.o stoc3.o stocR.o urn1.o urn2.o wnchyppr.o -F/Library/Frameworks/R.framework/.. -framework R -Wl,-framework -Wl,CoreFoundation
installing to /Users/jdoe/R/library/BiasedUrn/libs/i386
*** arch - x86_64
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c fnchyppr.cpp -o fnchyppr.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc1.cpp -o stoc1.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stoc3.cpp -o stoc3.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c stocR.cpp -o stocR.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn1.cpp -o urn1.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c urn2.cpp -o urn2.o
g++ -arch x86_64 -I/Library/Frameworks/R.framework/Resources/include -I/Library/Frameworks/R.framework/Resources/include/x86_64 -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fPIC  -g -O2  -c wnchyppr.cpp -o wnchyppr.o
g++ -arch x86_64 -dynamiclib -Wl,-headerpad_max_install_names -undefined dynamic_lookup -single_module -multiply_defined suppress -L/usr/local/lib -o BiasedUrn.so fnchyppr.o stoc1.o stoc3.o stocR.o urn1.o urn2.o wnchyppr.o -F/Library/Frameworks/R.framework/.. -framework R -Wl,-framework -Wl,CoreFoundation
installing to /Users/jdoe/R/library/BiasedUrn/libs/x86_64
** R
** demo
** inst
** preparing package for lazy loading
** help
*** installing help indices
** building package indices
** installing vignettes
   'UrnTheory.Rtex'
** testing if installed package can be loaded
*** arch - i386
*** arch - x86_64

* DONE (BiasedUrn)
</pre>

Subsequent to either of these methods, the package should be ready to use.

[Epstein software](http://genetics.emory.edu/labs/epstein/software/index.html) | [Human Genetics](http://genetics.emory.edu/) | [School of Medicine](http://www.med.emory.edu/) | [Emory University](http://www.emory.edu/)
