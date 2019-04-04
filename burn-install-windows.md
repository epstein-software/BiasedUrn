
## BiasedUrn: Microsoft Windows installation

### The precompiled Windows downloads:

For convenience, we are providing already modified and compiled windows-ready versions here, where we have set <tt>MAXCOLORS=10000</tt> Anyone who wishes to compile their own can proceed to subsequent sections of this page.

*   both 32- and 64-bit versions compiled for R-3.0.1:  
    [BiasedUrn_1.05.zip](BiasedUrn_1.05.zip)
*   32-bit compiled for R-2.15.* :  
    [BiasedUrn_32bit_1.04.zip](BiasedUrn_1.04.zip)
*   64-bit compiled for R-2.15.* :  
    [BiasedUrn_64bit_1.04.zip](BiasedUrn64_1.04.zip)

Upon downloading one of these zip files, the BiasedUrn code can be installed using the <tt>Packages</tt> menu option in the R GUI, as shown in Figure 2.

<figure>![R GUI menu for local package install](http://genetics.emory.edu/labs/epstein/software/BiasedUrn/R-console-packages-local.png)

<figcaption>Figure 2\. The menu option for installing packages from a local zip file.</figcaption>

</figure>

* * *

### How to build and install your own BiasedUrn package

Microsoft operating systems do not provide basic developer tools for compiling source code. This basic set of tools includes the GNU Compiler Collection (gcc), a Fortran compiler, a TeX distribution, among other tools. A convenient collection of resources for building R packages from source is provided by [Rtools](http://cran.r-project.org/bin/windows/Rtools/). The official guid to installation and administration of R and R packages is the _[R Administration and Installation](http://cran.r-project.org/doc/manuals/R-admin.html)_ manual. In particular, please read the [Windows Toolset](http://cran.r-project.org/doc/manuals/R-admin.html#The-Windows-toolset) appendix for further guidance.  
Once a set of working developer tools is installed, the instructions for compiling the BiasedUrn package are similar to those described in the [Linux section](burn-install-linux.html) of this document; However, there are subtle differences between Windows and Linux compilation and we therefore present details of the necessary shell commands for Windows below

#### Setting a few environment variables

**<tt>$RHOME</tt>**  
To avoid tedious typing of long directory names, it is convenient to define the directory where R is installed as a system variable. For the machine used in this example, we are using version <tt>R-2.15.0</tt> found under the <tt>C:/PROGRA~1/R</tt> directory, where <tt>PROGRA~1</tt> is the space-free short name for <tt>Program Files</tt>. Thus, we have defined

<pre>RHOME=C:\PROGRA~1\R\R-2.15.0
</pre>

The Microsoft website provides information about how to accomplish this for [Windows XP](http://support.microsoft.com/kb/310519). Check [this site](http://www.windows7hacker.com/index.php/2010/05/how-to-addedit-environment-variables-in-windows-7/) for how to do this in Windows 7.  
Hereafter refering to $RHOME is a shortcut to directory where R is installed.  

**<tt>$CYGWIN</tt>**  
Sometimes a Rtools cygwin terminal will produce warning messages like this:

<pre>cygwin warning:
  MS-DOS style path detected: C:\PROGRA~1\R\R-2.15.0/bin/R.exe
  Preferred POSIX equivalent is: /cygdrive/c/PROGRA~1/R/R-2.15.0/bin/R.exe
  CYGWIN environment variable option "nodosfilewarning" turns off this warning.
  Consult the user's guide for more details about POSIX paths:
    http://cygwin.com/cygwin-ug-net/using.html#using-pathnames
</pre>

To turn off such warnings, define a new environment variable

<pre>CYGWIN=nodosfilewarning
</pre>

These environment variables will not be in effect until a new terminal is initiated.

#### modify

The modification that needs to be performed is in the <tt>Makevars</tt> file within the package <tt>src</tt> directory. Open this file with any text editor then change the value of <tt>MAXCOLORS</tt> from 32 to the desired value; here we set <tt>MAXCOLORS=10000</tt> After performing this edit and saving the changes, the content of this file should look like this:

<pre># Makevars for BiasedUrn
# The value of MAXCOLORS may be modified
PKG_CPPFLAGS= -DR_BUILD=1 -DMAXCOLORS=10000
</pre>

#### check

First we run the check command to ensure the package can be compiled with the existing set of tools:

<pre># $RHOME/bin/R.exe CMD check BiasedUrn
* using log directory 'C:/Documents and Settings/jdoe/My Documents/projects/R/BiasedUrn.Rcheck'
* using R version 2.15.0 (2012-03-30)
* using platform: i386-pc-mingw32 (32-bit)
* using session charset: ISO8859-1
* checking for file 'BiasedUrn/DESCRIPTION' ... OK
...
* checking PDF version of manual ... OK
</pre>

#### build and install

If the check succeeds, then we build and install the modified package:

<pre># $RHOME/bin/R.exe CMD build BiasedUrn
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

# $RHOME/bin/R.exe CMD INSTALL --build BiasedUrn
* installing to library 'C:/Program Files/R/R-2.15.0/library'
* installing *source* package 'BiasedUrn' ...
file 'src/Makevars' has the wrong MD5 checksum
** libs
make: Nothing to be done for `all'.
installing to C:/Program Files/R/R-2.15.0/library/BiasedUrn/libs/i386
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
* MD5 sums
packaged installation of 'BiasedUrn' as BiasedUrn_1.04.zip

* DONE (BiasedUrn)
</pre>

If the terminal used to run the install command is initiated with Administrator priveleges, then the package can be installed in the main R tree; otherwise, it must be installed to a local account. The command line option <tt>--library</tt> will facilitate package installation into a local directory without administrator priveleges. In this case, one should create a directory dedicated to R packages, e.g., here use our terminal to create the directory <tt>$HOME/R/library</tt>:

<pre># mkdir $HOME/R
# mkdir $HOME/R/library
</pre>

where <tt>$HOME</tt> is the system variable set to the user's home directory.  

Finally, we perform the installation under this local directory:

<pre># $RHOME/bin/R.exe CMD INSTALL BiasedUrn --library=$HOME/R/library/
</pre>

[Epstein software](http://genetics.emory.edu/labs/epstein/software/index.html) | [Human Genetics](http://genetics.emory.edu/) | [School of Medicine](http://www.med.emory.edu/) | [Emory University](http://www.emory.edu/)
