The Tools
=========
This section describes the tools that you should find in the tools directory, what they are for, and brief details of what they do.

.. note:: The following code examples assume that the ``tools`` sub-directory has been added to your PATH.

The tools are unlikely to be of much use to anyone - they are designed for the initial conversion of the old, rough, HTML into something that Pandoc can convert to ReStructuredText.

buildTools.sh
-------------
This script calls the Linux C++ compiler, g++, to compile all the various c++ source files into a binary. It is executed as follows::

    buildTools.sh

Windows users will need to convert this to something resembling a batch file - if one doesn't already exist, but given the plethora of different C++ compilers available for Windows, it's unlikely that one will exist. (Update: I lied, see `buildTools.cmd` and adapt it for your particular C++ compiler - it defaults to Borland C++ 10.1)


fixHeadings
-----------
This C++ file removes some random characters from each command's main section heading. These get created when the document is converted from HTML to RST - by dint of some weird and wonderful HTML in the original file!

This utility also converts numerous HTML headings into bold text as they did not need to be headings as such.
  
This utility gets automatically run by the HTML2rst.sh shell script.

It can, however, be executed on it's own as follows::

    fixHeadings < KeywordsX.clean.rst > output_file.rst
  
  
fixLinks
--------
This C++ utility converts existing links to other commands in the generated RST files so that they point to ``KeywordsX.clean.html#xxx`` rather than to ``KeywordsX.html#xxx``. 

The fix also includes the lower-casing of the command name and the replacing of some unusable characters with hyphens - to match what Sphinx generates. 

Any '$' or '%' in the link names or anchors - the bit after the '#' - get dropped.


fixLinkComments
---------------
During testing, fixLinks output the original link text, which it was converting, as a comment line in the RST file. It was found that those commenst caused erros in other utilities further down the chain, so they had to be removed. 

As there were numerous comments, this utility was quickly written to find and destroy them. It is executed manually, on demand, by the following::

    fixLinkComments < KeywordsX.clean.rst > output_file.rst

It should no lonegr be required but lives on in source code form!


fixSyntax
---------
This utility tries it's best to convert the Syntax: and Location: lines for each command, into a nice looking table. It gets it right pretty much *most* of the time, but occasionally, we still need to do some manual editing.
  
This utility gets automatically run by the HTML2rst.sh shell script.


preHTMLTidy
-----------
This one simply corrects any invalid '<br href="...">...</a>' tags, which are simply and utterly wrong, into the correct form which is '<a href="...">...</a>'. It can be executed by itself but is normally called from within the HTMLTidy.sh script::

    preHTMLTidy < KeywordsX.html > output_file.html
    

Process.sh
----------
This script simply calls the following two to do the work for a single html file. Once completed, and if no errors were reported, the various source files, error texts etc are moved to their appropriate directory.


HTMLTidy.sh
-----------
This script takes care of all the HTML handling to get a clean (cleanish?) HTML file to convert to RST. It calls out to preHTMLTidy first, then runs the HTML Tidy utility to attempt to clean up the HTML. 

If there are any errors reported, the utility will stop. 

If there are any warnings, these are listed, but in this case, the utility carries on.

Sed is then called to strip out a list of headings that have line breaks in them, either before - "<BR><Hn>" or after "<Hn><BR>" as these are just plain wrong! The edit also strips out any heading that is immediately followed by a line feed - "<Hn>\n".

The output from all this is a clean HTML file named ``KeywordsX.clean.html``. It shouldn't need to be, but can be called on it's own, as follows::

    HTMLtidy.sh KeywordsX.html
    
This will produce the following files in the current directory:

- KeywordsX.html.tmp - a temporary work file.
- KeywordsX.clean.html - a ReStructuredText source file ready for manual tidying up and future processing.    
- KeywordsX.errors.txt - a file holding all the errors and warnings from the (most recent) run of the HTML Tidy utility.


HTML2rst.sh
-----------
This script takes the clean HTML file produced by HTMLTidy.sh, and converts it to an RST file named ``KeywordsX.clean.rst``. 

It does this by running sed to strip out Rich's table of contents which is present at the head of each and every file in the original online manual - this is no longer needed.

Pandoc is then called to convert this truncated HTML file to RST.

Once the RST file is created, the utilities fixSyntax, fixHeadings and fixLinks are executed to do the needful.

It shouldn't *need* to be, but it *can* be called on it's own, as follows::

    HTML2rst.sh KeywordsX.clean.html
    
This will produce the following files in the current directory:

- KeywordsX.clean.rst.tmp - a temporary work file.
- KeywordsX.clean.rst - a ReStructuredText source file ready for manual tidying up and future processing.   

