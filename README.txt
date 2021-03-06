######################################

All files distributed with LGL fall under the terms of 
the GNU General Public License, and are copyright (c) 2002, 2003 Alex Adai.

LGL on the web at:  http://www.opte.org/lgl/

Much thanks to the Marcotte lab for testing.

######################################
# Table of contents

  0 Before compiling!
  I Setup and Installation
 II Other files that come with LGL
III Expanding LGL
IV  What's new for 2.0


######################################
# 0

Firstly, LGL will probably only compile with the GNU compilers. It was tested 
on FreeBSD 9.x and CentOS, but it should compile OK on other Linux 
distributions. For other operating systems you are on your own. Good Luck :-)

You must have the following Perl modules in your @INC path to run LGL:

ParseConfigFile.pm
LGLFormatHandler.pm

These files are in the ./perls directory.  You don't have to know anything 
about these modules, and you won't have to use them directly but lgl.pl will 
call them.

######################################
# I

To compile LGL change to the same directory as setup.pl and type:

prompt$ ./setup.pl -i

This will compile 2D and 3D versions of LGL and put the resulting binaries 
in the ./bin directory. Afterwards you can move them whereever you want.


NOTE:  setup.pl has been updated to locate boost, however you may need
       to direct gcc on where to find the includes if the automated 
       detection does not work:

       env CPLUS_INCLUDE_PATH=/usr/local/include ./setup.pl -i

After all is compiled and done you can run LGL by the driver script lgl.pl as:

prompt$ ./bin/lgl.pl edges_file

but you have to modify the 'tmpdir' variable in lgl.pl. That directory will 
hold all the files that LGL outputs, and it must be changed for EACH run.  
However, The best way to run LGL is to have setup.pl generate a sample 
config file for lgl.pl by running it as

prompt$ ./setup.pl -c conf_file_name

That file (after modification of course) can just be given to lgl.pl for 
execution as follows:

prompt$ ./bin/lgl.pl -c conf_file_name

The config file itself is documented further, and explains each of the 
variables to be used.  It also provides defaults, so the minimum that MUST 
be changed are the variables:

tmpdir
inputfile

where tmpdir is the output directory of the LGL run and inputfile is the edge 
file. inputfile must be a file parsable by LGLFormatHandler.pm This can be 
just a simple 2 column space delimited file with one edge per line 
(the 2 vertex ids represent the two columns).

One last change is to ./bin/lgl.pl. A Perl variable $LGLDIR must be set to 
the root bin directory of all the lgl executables (This might be 
/where/lgl/was/unpacked/bin ). This var is empty by default, and the 
program won't run until it is set correctly.

######################################
# II

A list of important files in the perls dir:

genVrml.pl - This generates the VRML code from 3D layout results. Run 
genVrml.pl with no args to get the usage.

colorEdgesBasedOnLevel.pl - This generates a simple color file to be 
given to lglview, that will color your edges based on the level in the 
heirarchy in layout.

Other files might be included as well, but they are not necessary for LGL. 
Their documentation will be added here in the near future, or they may not 
be carried in the future.

Other Files:


LGLView.jar - A JAVA 2D viewer for looking at the output of lgl.pl. The output of the layout programs is just a set of coordinates.  For looking at 2D 
coordinates use lglview.jar See the web page http://www.opte.org/lgl for 
usage and other info.

ImageMaker.jar - A JAVA 2D image output tool.  For more detail visit http://www.opte.org/lgl/

Looking at the huge PNG (100k x 100k pixels) java.awt.image.Raster: The 
maximum width x height has to be less than Integer.MAX_VALUE (2147483647) so 
the maximum square image is 46340 x 46340. Note also that such images will 
need a lot of RAM since Java's BufferedImage's pixels are hold in memory. 

An example of a larger output would be: 

java  -Xms1G -Xmx5G -jar ImageMaker.jar 29200 29200 <files...>


LGLView.jar - The full package that combines LGLView and ImageMaker.


Java - Directory and source code of all JAVA programs.  See README in the JAVA dir.

######################################
# III

The most obvious way to expand LGL is to add support for your type of edge file to LGLFormatHandler.pm.  Just add a method to read in your file type, update 
the 'loadFromFile' method to recognize your file suffix, and that should be it.

Let me know of any source code contributions that would make LGL more suitable 
and usable so I can add the code in!

######################################
# IV

LGL-2.0 is the first new release of LGL in years.  It's the first release by 
the new LGL team at the Opte Project.  LGL was the baby of Alex Adia and 
he's been too busy to update things, now we're involved in bringing the 
code up-to-date. 

2.0 changes include:  

   * The code has been ported to boost-1.55

   * Now compiles on modern operating systems

   * LGLView.jar has been updated to work with Java 1.6

   * ImageMaker.jar has been released with the ability to do large resolution.
     do 46340 x 46340 pixel output.

   * UI fixes for lglview.jar

   * The original code uses Jama, the old classes were included with the 
     software package, we've now changed that to use the JAR from Jama RI.


######################################


Cheers the LGL team!
lgl@opte.org


