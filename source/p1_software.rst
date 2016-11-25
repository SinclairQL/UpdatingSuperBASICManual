Software Required
=================

I did all my stuff on Linux, well most of it, I did install everything on a Windows 7 box, just to see if it was any good. Surprisingly enough it was, but then again, that's the value of Open Source stuff. It *usually* works!

To fix things, you only need the following software:

- A decent text editor. *Not* a word processor like Word or Open/Libre Office. On Windows I would advise ``Notepad++``. On Linux, I use the default text editor in Linux Mint 18 which is ``xed`` but any decent one will do. It helps if it has or understands ReStructuredText highlighting, but this isn't essential.

- Git. You need git to be able to ``pull`` and ``push`` changes from and to the repository. You can download the entire repository as a zip file, but any changes you make can't then be pushed back.

So far so not too exciting, however, if you intend to add any new details to the manual, or it you want to build a local copy to test your changes, you will need more:

- Python - because Sphinx-doc needs Python to work.
- Sphinx-doc - which takes the ReStructuredText that we create and converts it into other formats.

That's the main software list covered in brief, there are some optional software that you might find useful too:

- Pandoc - this is literally the Swiss Army Knife of document conversion. I use it at work to convert ReStructuredText into Word's docx format because I'm sick and tired of Word deciding that my desired formatting is not what it thinks I should have, or that two consecutive bullet points should have totally different bullets or indents or bullet sizes! Word drives me absolutely nuts!

- A C++ Compiler. Useful if you ever have the need to build any of the utilities in the Tools folder.


How and Where to Get the Software
=================================

The Editor
----------

Head on over to https://notepad-plus-plus.org/ and download the latest version. Install it andthat's all there is to it. This is probably one of the finest text editors I've used on any operating system and I cannot recommend it highly enough.


Git
---

Git is needed to allow the SuperBASIC-Manaul repository to be updated. The download details, for Windows users, can be found at https://git-for-windows.github.io/. If you are on Linux then your software repository will have an up to date versions which you should install using the appropriate package manager.

Mac users simply need to head on over to https://git-scm.com/download/mac where you will get all the details you need.


Sphinx-Doc
----------

Overall, the biggie of the conversion process is a tool called Sphinx, or Sphinx-doc to avoid searching Google for statues of lion beasts from Ancient Egypt! ;-)

Head over to http://www.sphinx-doc.org/en/stable/install.html where you will find details of installing just about everything you need for Windows, Linux and Macs to run the Sphinx documentation builder.

Sphinx needs Python and it needs a version of Python that is 2.7 or higher (at the time of writing.)


Python
------

Windows and Mac users should go to https://www.python.org/downloads/, the main download site for Python. Look for a link to the Python download for your Operating System. Linux users, just install Python from your software repository in the usual manner.

Version 2.7 is suitable, but 3.x is probably better in the long run if you plan on doing more Python work on Windows.

Run the installer and install the package somewhere suitable. Make sure you update your path to suit, or nothing will work!


Pip
---

Once Python is installed, install pip::

    python get-pip.py

Simple stuff. pip is the Python Installer Program and is useful in installing Python utilities. We need it to install Sphinx.    


Sphinx
------

Once Pip is installed, install Sphinx::

    pip install sphinx

Once this is complete, make sure it worked by running the command::

    sphinx-build --version

Which will show you that your PATH etc are set up well enough to build things. You should see something like::

    Sphinx (sphinx-build) 1.4.6

    
Sphinx RTD Theme
----------------

Sphinx used to come with a Read The Docs theme installed automatically, but more recent versions don't include it for some unknown reason. Not to worry, if you try to build docs using that theme, you will be prompted to install it as follows::

    pip install sphinx_rtd_theme
    

Optional Software
=================

The software above is all you need to be able to run the *building* of the docs, however, the following might prove useful in other work you might want to do later.

    
Pandoc
------

Pandoc is used to convert the cleaned up HTML into ReStructuredText format. This can also convert numerous input formats into many different output formats, it is the *Swiss Army Knife* of document conversions. 

Head on over to http://pandoc.org/installing.html where you will find instructions and downloads for installing Pandoc.

Pandoc is a command-line tool to convert between different document formats. It can read in the following formats:

- Commonmark, docbook, docx, epub, haddock, html, json, latex, markdown, markdown_github, markdown_mmd, markdown_phpextra, markdown_strict, mediawiki, native, odt, opml, org, rst, t2t, textile & twiki.

And it can convert those to any of the following:

- Asciidoc, beamer, commonmark, context, docbook, docbook5, docx, dokuwiki, dzslides, epub, epub3, fb2, haddock, html, html5, icml, json, latex, man, markdown, markdown_github, markdown_mmd, markdown_phpextra, markdown_strict, mediawiki, native, odt, opendocument, opml, org, plain, revealjs, rst, rtf, s5, slideous, slidy, tei, texinfo, textile & zimwiki.

As I mentioned, I use it at work with something resembling the following command::

    pandoc -f rst -t docx --toc --toc-depth 3 --reference-docx pandoc_reference.docx -o RMANRestore.docx RMANRestore.rst
    
That reads my ``RMANRestore.rst`` text file, references the file ``pandoc_reference.docx`` to determine the formatting of the various styles I need, and writes out ``RMANRestore.docx`` as a properly formatted Word document.
    

A C++ Compiler
--------------

On Linux, just about everything uses the G++ compiler. That's definitely what I use, however, Windows is the proverbial nightmare. Visual Studio Express Edition is freely available for download and use, but it's no longer proper C++ as Microsoft went over to their "java-like" .net nonsense years ago. Even their C++ compiler cannot compile proper standard C++ code - does that sound familiar? Microsoft and standards not matching up? 

The best ever compiler on Windows was always Borland C++ and many years ago, they gave away the 5.5 version to anyone who wanted it. I used it happily for years on Windows. Sadly, Borland sold out to Embarcadero, but the 5.5 version is still available and still free.

*However*, Embarcadero recently started giving away version 10 of the compiler which is right up to date. You can get it at https://www.embarcadero.com/free-tools then follow the links to the C++ compiler.

You will need to create an account, but this only causes a few special offers in your inbox, some of them useful!

If anyone is interested, this is what Embarcadero have to say about their free tool:

    *This free download of the C++ Compiler for C++Builder includes C++11 language support, the Dinkumware STL (Standard Template Library) framework, and the complete Embarcadero C/C++ Runtime Library (RTL). In this free version, you’ll also find a number of C/C++ command line tools—such as the high performance linker and resource compiler.*

    
All Done!
---------    
That's (about) it! Nothing too excessive now, was it? Too much software perhaps? Well, nobody said that it was going to be easy. But remember, once all this is installed, you have a very good and useful document production system whihc can be used for many things, not just updating the SuperBASIC Manual.
