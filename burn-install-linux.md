## BiasedUrn: Linux installation

Other than the R software itself, most [Linux distributions](http://distrowatch.com/) (e.g. Ubuntu, CentOS, Debian, Slackware among other) include the developer tools required to compile R library packages. The instructions below should work for the majority of Linux distributions.

### modify

We will use shell commands within a Linux terminal to edit, recompile, and install the package. First, change directories to that which contains the BiasedUrn package source code. Here, we assume this directory is called <tt>Downloads</tt> and is found under our home directory (i.e. <tt>~/Downloads/</tt>).

<pre>jdoe@somewhere ~ $ cd ~/Downloads
</pre>

Next, use the <tt>tar</tt> command to extract the BiasedUrn source code.

<pre>jdoe@somewhere ~/Downloads $ tar -zxf BiasedUrn_1.04.tar.gz 
</pre>

The default contents of the <tt>Makevars</tt> file within the package <tt>src</tt> directory is displayed here:

<pre>jdoe@somewhere ~/Downloads $ cat BiasedUrn/src/Makevars
# Makevars for BiasedUrn
# The value of MAXCOLORS may be modified
PKG_CPPFLAGS= -DR_BUILD=1 -DMAXCOLORS=32
</pre>

Using any text editor, change the value of <tt>MAXCOLORS</tt> from 32 to 10000\. After performing this edit and saving the changes, the file should look like this:

<pre>jdoe@somewhere ~/Downloads $ cat BiasedUrn/src/Makevars
# Makevars for BiasedUrn
# The value of MAXCOLORS may be modified
PKG_CPPFLAGS= -DR_BUILD=1 -DMAXCOLORS=10000
</pre>

### check

Before building the package, one should execute the `R check` script to resolve any problems that may arise from compiling the package, e.g., missing developer tools. The command line execution of this step along with example output is shown here:

<pre>jdoe@somewhere ~/Downloads $ R CMD check BiasedUrn
* using log directory '/home/jdoe/Downloads/BiasedUrn.Rcheck'
* using R version 2.15.0 (2012-03-30)
* using platform: i686-pc-linux-gnu (32-bit)
* using session charset: ASCII
* checking for file 'BiasedUrn/DESCRIPTION' ... OK
* checking extension type ... Package
* this is package 'BiasedUrn' version '1.04'
* checking package namespace information ... OK
...
* checking re-building of vignette PDFs ... OK
* checking PDF version of manual ... OK
</pre>

The full output generated from the <tt>check</tt> command can be found in the log file <tt>BiasedUrn.Rcheck/00check.log</tt>.

### build

Next we use the build command to compile the modified package and create an installable package file. This step will overwrite the original source file <tt>BiasedUrn_1.04.tar.gz</tt> with the installable modified package file.

<pre>jdoe@somewhere ~/Downloads $ R CMD build BiasedUrn
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

<pre>jdoe@somewhere ~/Downloads $ sudo R CMD INSTALL BiasedUrn_1.04.tar.gz 
Password: 
* installing to library '/usr/local/lib/R/library'
* installing *source* package 'BiasedUrn' ...
** libs
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c fnchyppr.cpp -o fnchyppr.o
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c stoc1.cpp -o stoc1.o
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c stoc3.cpp -o stoc3.o
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c stocR.cpp -o stocR.o
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c urn1.cpp -o urn1.o
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c urn2.cpp -o urn2.o
g++ -I/usr/local/lib/R/include -DNDEBUG -DR_BUILD=1 -DMAXCOLORS=10000 -I/usr/local/include    -fpic  -g -O2  -c wnchyppr.cpp -o wnchyppr.o
g++ -shared -L/usr/local/lib -o BiasedUrn.so fnchyppr.o stoc1.o stoc3.o stocR.o urn1.o urn2.o wnchyppr.o
installing to /usr/local/lib/R/library/BiasedUrn/libs
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

* DONE (BiasedUrn)
</pre>

### install to local account

In the event one does not have root privileges, a local version of the package can be installed and used from the user account. Ensure that you have a directory set for local package installations; here we have created the directory <tt>~/R/library/</tt> for this purpose. In the output from this command you should see a line indicating installation to this local directory:

<pre>jdoe@somewhere ~/Downloads $ R CMD INSTALL BiasedUrn_1.04.tar.gz --library=~/R/library/
...
* installing *source* package 'BiasedUrn' ...
...
installing to /home/jdoe/R/library/BiasedUrn/libs
...
</pre>

The package should now be ready to use.

[Epstein software](http://genetics.emory.edu/labs/epstein/software/index.html) | [Human Genetics](http://genetics.emory.edu/) | [School of Medicine](http://www.med.emory.edu/) | [Emory University](http://www.emory.edu/)
