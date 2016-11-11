Software Required
=================

I did all my stuff on Linux, well most of it, I did install everything on a Windows 7 box, just to see if it was any good. Surprisingly enough it was, but then again, that's the value of Open Source stuff. It *usually* works!

Overall, the biggie of the conversion process is a tool called Sphinx, or Sphinx-doc to avoid searching Google for statues of lion beasts from Ancient Egypt! ;-)

Head over to http://www.sphinx-doc.org/en/stable/install.html where you will find details of installing just about everything you need for Windows to run the Sphinx documentation builder.


Python
------
Most Windows users do not have Python, so we begin with the installation of Python itself. If you have already installed Python, please skip this section.

Go to https://www.python.org/, the main download site for Python. Look at the left sidebar and under “Quick Links”, click “Windows Installer” to download.

Version 2.7 is suitable, but 3.x is probably better in the long run if you plan on doing more Python work on Windows.

Run the installer and install the package somewhere suitable. Make sure you update your path to suit, or nothing will work!

The Sphinx link above has all the details, and indeed, some of the text I copied above came from there!


Pip
---
Once Python is installed, install pip::

    c:\> python get-pip.py

Simple stuff. pip is the Python Installer Program and is useful in installing Python utilities. We need it to install Sphinx.    


Sphinx
------
Once Pip is installed, install Sphinx::

    c:\> pip install sphinx

Once this is complete, make sure it worked by running the command::

    c:\> sphinx-build --version

Which will show you that your PATH etc are set up well enough to build things. You should see something like::

    Sphinx (sphinx-build) 1.4.6

Sphinx RTD Theme
----------------
Sphinx used to come with a Read The Docs theme installed automatically, but more recent versions don't include it for some unknown reason. Not to worry, if you try to build docs using that theme, you will be prompted to install it as follows::

    c:\> pip install sphinx_rtd_theme
    

Conversion Software
===================
The software above is all you need to be able to run the *building* of the docs, however, if like me, you are *converting* from the old HTML files, you need a few more bits and pieces.

    
Cmake
-----
https://cmake.org/download/ is where you can find the Cmake downloader for Windows. You will need it to compile HTML Tidy.

    
HTML Tidy
---------
HTML Tidy is used to clean up the rough HTML generated from the Text 87 sources and product something that has been validated for cleanliness and standards adherence. It is best to have a clean starting point before converting to other formats.

https://github.com/htacg/tidy-html5 is the URL to head on over to, and from there you can download the source code. It can be built from source using something called cmake, which you should also install.


Pandoc
------
Pandoc is used to convert the cleaned up HTML into ReStructuredText format. This can also convert numerous input formats into many different output formats, it is the *Swiss Army Knife* of document conversions. 

Head on over to http://pandoc.org/installing.html where you will find instructions and downloads for installing Pandoc.


Git
---
Git is needed to allow the SuperBASIC-Manaul repository to be updated. The download details can be found at https://git-for-windows.github.io/.


A C++ Compiler
--------------

On Linux, just about everything uses the G++ compiler. That's definitely what I use, however, Windows is the proverbial nightmare. Visual Studio Express Edition is freely available for download and use, but it's no longer proper C++ as Microsoft went over to their "java-like" .net nonsense years ago. Even their C++ compiler cannot compile proper standard C++ code - does that sound familiar? Microsoft and standards not matching up? 

The best ever compiler on Windows was always Borland C++ and many years ago, they gave away the 5.5 version to anyone who wanted it. I used it happily for years on Windows. Sadly, Borland sold out to Embarcadero, but the 5.5 version is still available.

Even better, Embarcadero recently started giving away version 10 of the compiler which is right up to date. You can get it at https://www.embarcadero.com/free-tools then follow the links to the C++ compiler.

You will need to create an account, but this only causes a few special offers in your inbox, some of them useful!

If anyone is interested, this is what Embarcadero have to say about their free tool:

    *This free download of the C++ Compiler for C++Builder includes C++11 language support, the Dinkumware STL (Standard Template Library) framework, and the complete Embarcadero C/C++ Runtime Library (RTL). In this free version, you’ll also find a number of C/C++ command line tools—such as the high performance linker and resource compiler.*

    
All Done!
---------    
That's (about) it! Nothing too excessive now, was it? Too much software perhaps? Well, nobody said that it was going to be easy. But remember, once all this is installed, you have a very good and useful document production system.
