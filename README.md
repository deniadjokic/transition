Instructions
============

This is the main page for the instructions. It contains links to other pages within 
this repository that have additional information.

Installation
------------

There are three options for installation and instructions for each.

- [Virtual 
  Machine](https://github.com/katyhuff/transition/blob/master/vm_readme.md) (any platform)
- [Natively on 
  MacOSX](https://github.com/katyhuff/transition/blob/master/mac_readme.md) (macosx)
- [Natively on Linux](https://github.com/cyclus/cyclus/blob/develop/README.rst) 
  (after dependencies, same installation as macosx)


Checking
--------

Did the installation work? You can check in the terminal by running the tests. 
The tests are all in the bin directory. You can run each of them in turn. 
Execute the following lines one at a time: 

    cd ~/cyclus/install/bin
    ./CommodConverter_unit_tests
    ./StubInst_unit_tests         
    ./cyclus_unit_tests
    ./MktDrivenInst_unit_tests    
    ./StubRegion_unit_tests       
    ./SeparationMatrix_unit_tests 
    ./cycamore_unit_tests         
    ./StreamBlender_unit_tests    


Running
-------

In the cyclus/install/bin directory, you will also find the cyclus executable. 
Most simply, if you have an input file that you'd like to run, you can run the 
cyclus executable from the install/bin directory thus :

    ./cyclus input.xml

If the input file is in another directory, just give it the path:

    ./cyclus ~/cyclus/transition/input/example.xml

If you want to run cyclus from a different directory, you can do that too:

    ~/cyclus/install/bin/cyclus ~/cyclus/transition/input/example.xml



Analysis
--------

After you run cyclus, a cyclus.sqlite file will appear in the directory where 
you ran cyclus.

You can open that file using an sqlite browser such as
[sqliteman](http://sqliteman.com/) or 
[sqlitebrowser](http://sqlitebrowser.org/). Both of these are installed on the 
virtual machine.

To further analyze that file, there is a set of postprocessing scripts called 
[cyan](https://github.com/rwcarlsen/cyan). They were written in Go by Robert 
Carlsen. They go a long way toward extracting the output in an appropriate 
manner for comparison with FCO. If you have followed the installation 
instructions above or if you are working in the virtual machine, those scripts 
will be located in the ~/postprocessing directory.

To prepare the database for postprocessing (do this once) :

    cd ~/postprocessing/bin
    cp ~/cyclus/install/bin/cyclus.sqlite .
    cycpost cyclus.sqlite

To output a png graph of the flow of all material between agents from time=2 to 
time=7 :

    metric -db cyclus.sqlite flowgraph -t1=2 -t2=7 > flow.dot
    dot -Tpng -o flow.png flow.dot


For additional useful behaviors, try the -h flag for help with cyan, or see the 
[cyan](https://github.com/rwcarlsen/cyan) documentation.

Updating
--------

Since this is a work in progress, note that the code will change over time. You 
want to have the most up to date code, so I have included an update script for 
this purpose. When you want to update the repositories and reinstall cyclus, 
run update.sh. Please make sure the $TOP_DIR path is correct for your setup. If 
you have followed the instructions above exactly, or if you are on the virtual 
machine, it will be. 

If you do run this update script, it may be worth just reading over the output. 
Were there any fatal errors? If so, please email me the output and we'll make 
sure to get you on track.

