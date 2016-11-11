Step by Step Guide to the Migration
===================================

Clone the git Repository
------------------------
In a shell (DOS) session, yes, we use the command line a lot here, I cloned my repository where all the latest up to date (master) and working sources can be found. 

::

    cd SourceCode
    git clone https://github.com/NormanDunbar/SuperBASIC-Manual.git

This command created a directory named SuperBASIC-Manual and within it, the following sub-directories were created:

- clean - this is where the cleaned up html files are saved. If you have fixed all the errors and warnings them the files here are genuine HTML5 compliant.
- errors - where the errors and warnings from HTMLTidy are sent.
- html - this is where the old, dirty, html files are saved. These may be used in future to run a diff to see what, if anything, has been changed and may need updating in the RST [#]_ (ReStructuredText) files. 
- sphinx - where the make files live. These help you build the various documentation formats.
- sphinx/source - where the numerous RST files live. These are the files I edited. This will be where any corrections of updates will be done too.
- tools - where the various tools, and their source code live. See `the tools page <tools.html>`__ for details.

Some build specific directories are created on demand too, once the appropriate build command is called. These are, or will be:

- sphinx/build/buildtrees - nothing to see here, move along! A working area used by the sphinx software. Don't edit anything here please! It's basically a cache so that only changed files are recompiled into HTML or Latex etc.
- sphinx/build/html - where the HTML generated documentation is/will be found.
- sphinx/build/latex - where the LATEX and LATEXPDF generated documentation is/will be found.
- sphinx/build/linkcheck - where the linkcheck command puts its output.


These latter directories will not appear until after the first build (of the appropriate format).


Checkout the working branch
---------------------------
Currently I have only checked out the *master* branch. We *do not* work on this branch, unless we are merging changes from the *working* branch.

The master branch is only for the fully edited and corrected files. These are used by "Read the Docs" to build HTML, PDF and EPUB versions of the SuperBASIC Manual, every time there is a git push to the master branch. 

*All work is done on the working branch.* The working branch also causes a rebuild of the html, pdf and epub versions, but only of the working docs. These are *not* considered suitable for general consumption - that's what the master branch is for - but it gives the author/convertor an idea of how it will look when completed.

Remember, **We do not break the build!** and **The master branch always builds!**

::

    git checkout working
    git branch
    
You should see::

    master
   *working
    
The asterisk before the branch name shows you the current branch. We can see from the above that we are indeed on the correct, ``working`` branch.    


Build the Tools
---------------
The various tools I've created don't have their binary versions included in the repository, for obvious reasons. The source code is either a Bash shell script (*.sh) or a C++ source file (*.cpp).

For Linux users there's a buildTools.sh script to compile everything. For Windows users, try buildTools.cmd but you will need to adjust the default compiler used to match your system. I'm on Linux, so I'm happy!

The script will compile the following:

- fixHeadings.cpp
- fixLinks.cpp
- fixLinkComments.cpp
- fixSyntax.cpp
- preHTMLTidy.cpp
- And any more I later add of course!

There are a number of shell scripts,. Linux format, to call the various tools above. These will most likely need converting to Windows batch files, or PowerShell scripts - if you are that masochistic! You are on your own here, especially as I can't find a decent replacement for the ``sed`` editor, which is used in the various scripts.


Fetch an HTML File
------------------

::

    wget http://www.rwapsoftware.co.uk/SBASIC_reference_manual_online/KeywordsX.html

This creates a file named KeywordsX.html in the current directory. Alternatively:

- Open the page in your Internet browser. The following assumes Chrome.
- Right-click
- View page source
- Right-click
- Save as ...
- Then save the source with the same filename that you originally opened - ``KeywordsX.html``, for example.

.. warning:: Do not select the 'save as' option when you first right-clicked on the page in the browser. That option is entirely different and downloads any or all supporting css files, images etc.

Run Process.sh 
--------------

For Linux users, ie me, this file does the lot. Well, unless HTML Tidy exits with an error of course, but if it's just warnings, it will continue.

This script does a lot of work:

- runs preHTMLTidy.
- runs HTMLTidy.sh to, hopefully, produce a clean html file. 
- runs a sed script to do some basic tidying up to line breaks in wrong places.
- runs HTML2rst.sh to convert the clean html to ReStructuredText in KeywordsX.clean.rst.
- Processes the Syntax and Location sections to build a nice looking table format.
- Changes various headings that shouldn't be actual headings, into bold - warnings, notes etc.
- Moves the KeywordsX.html file to the html directory.
- Moves the KeywordsX.clean.html to the clean directory.
- Moves the errors & warnings file from HTMLTidy.sh, KeywordsX.errors.txt, to the errors directory.
- Moves the generated KeywordsX.clean.rst to the sphinx/source directory, ready for editing.


Windows users could try having a look at the following to get an idea of what they will need to do ...


Run PreTidy
-----------
Assuming we are working with KeywordsX.html, then::

    copy KeywordsX.html to KeywordsX.html.tmp
    tools/preTidy <KeywordsX.html.tmp >KeywordsX.html

This sorts out the faulty <br href="some url"> tags into correct <a href="some url"> tags prior to the proper run of html tidy.


Test HTMLTidy.sh
----------------

Run a test tidy of filename.html::

    HTMLTidy.sh filename.html

This will display any errors first. If there are any, edit filename.html to correct them, them repeat the run of HTMLTidy.sh until it only shows warnings. 

Warnings should be checked, but you can ignore stuff that says  that there are unescaped '&'s or '<' and '>' etc. If you see warnings about "unknown entity dir1" or similar, the you are probably looking at something like::

    dir1$=datad$&dir1$

where the '&', which will be flagged as unescaped, is causing the variable dir1$ to be considered as an HTML entity, similar to &quot; or &lt; or &amp; etc.

These can also be ignored. The problem(s) are caused by the original html file setting program listings as italic body text rather than wrapped in <pre> </pre> tags.    

.. note:: A lot of the code examples don't have spaces in the lines, unless absolutely necessary - it makes for interesting reading!

Things like 'escaping linefeed in <a> tag" should be fixed. You will find something like::

    <a href="some url">
    anchor text here</a>

which should be all on one line, not on two::

    <a href="some url">anchor text here</a>

Once happy that the warnings etc can be ignored, move on.


Edit the Source
---------------

This is where the fun begins. All - or as much as possible - of the automatic tidying has been done. The rest is up to me/you/us!


Paragraphs
~~~~~~~~~~

Start typing at the left margin. Don't stop typing at the end of a line - but if you do, don't worry, the line feed will be ignored, and replaced with a space as the various lines making up the paragraph are merged.

Leave a blank line between paragraphs, otherwise it all runs into one.


Syntax/Location Table
~~~~~~~~~~~~~~~~~~~~~

Making sure that the synatx/location table is correctly formatted. The code generates a single line for each, but where there are "or" options in either Syntax or Location, these need to be on separate lines with a double pipe (||) to force a newline in the table. 

If a command only has a single form, then a table like this will suffice::

    +----------+------------------------------------+
    | Syntax   | Command(a,b)                       |
    +----------+------------------------------------+
    | Location | QL ROM, TOOKIT II, SOMEWHERE ELSE  |
    +----------+------------------------------------+

The above will render into the following:    

+----------+------------------------------------+
| Syntax   | Command(a,b)                       |
+----------+------------------------------------+
| Location | QL ROM, TOOKIT II, SOMEWHERE ELSE  |
+----------+------------------------------------+

    
However, if there are alternate forms, the table needs to look like this::

    +----------+------------------------------------+
    | Syntax   || Command(a,b) or                   |  
    |          || Alternative(a,b,c)                |
    +----------+------------------------------------+
    | Location || QL ROM, TOOKIT II, SOMEWHERE ELSE |
    +----------+------------------------------------+

which becomes the following after a build:

+----------+-------------------------------------+
| Syntax   || Command(a,b) or                    |
|          || Alternative(a,b,c)                 |
+----------+-------------------------------------+
| Location || QL ROM, TOOKIT II, SOMEWHERE ELSE  |
+----------+-------------------------------------+

Which gives a better layout in the generated HTML. You should note the doubling up of the pipe characters in both the syntax and location sections of the table.


Tables
~~~~~~

We use grid tables, where we design the table according to how we want it to look::

    +--------+--------+--------+
    | Cell 1 | Cell 2 | Cell 3 |
    +--------+--------+--------+
    | Cell 4 | Cell 5 | Cell 6 |
    +--------+--------+--------+


+--------+--------+--------+
| Cell 1 | Cell 2 | Cell 3 |
+--------+--------+--------+
| Cell 4 | Cell 5 | Cell 6 |
+--------+--------+--------+

We can add headings too::

    +--------+--------+--------+
    | Head 1 | Head 2 | Head 3 |
    +========+========+========+
    | Cell 1 | Cell 2 | Cell 3 |
    +--------+--------+--------+
    | Cell 4 | Cell 5 | Cell 6 |
    +--------+--------+--------+

+--------+--------+--------+
| Head 1 | Head 2 | Head 3 |
+========+========+========+
| Cell 1 | Cell 2 | Cell 3 |
+--------+--------+--------+
| Cell 4 | Cell 5 | Cell 6 |
+--------+--------+--------+

Cells can span along the row::

    +--------+--------+--------+
    | Head 1 | Head 2 | Head 3 |
    +========+========+========+
    | Cell 1 | Cell 2 and 3    |
    +--------+--------+--------+
    | Cell 4 | Cell 5 | Cell 6 |
    +--------+--------+--------+

+--------+--------+--------+
| Head 1 | Head 2 | Head 3 |
+========+========+========+
| Cell 1 | Cell 2 and 3    |
+--------+--------+--------+
| Cell 4 | Cell 5 | Cell 6 |
+--------+--------+--------+

And also, down the columns::

    +--------+--------+--------+
    | Head 1 | Head 2 | Head 3 |
    +========+========+========+
    | Cell 1 | Cell 2 | Cell 3 |
    |        +--------+--------+
    | Cell 4 | Cell 5 | Cell 6 |
    +--------+--------+--------+

+--------+--------+--------+
| Head 1 | Head 2 | Head 3 |
+========+========+========+
| Cell 1 | Cell 2 | Cell 3 |
|        +--------+--------+
| Cell 4 | Cell 5 | Cell 6 |
+--------+--------+--------+

Getting text on separate lines is interesting, and a bit of a hack. You've already seen it above for the Syntax/Location tables, but here we are again::

    +--------+-----------------+
    | Head 1 | Head 2          |
    +========+=================+
    | Cell 1 | Cell 2 - line 1 |
    |        | Cell 2 - line 2 |
    +--------+-----------------+
    | Cell 4 | Cell 5          |
    +--------+-----------------+


+--------+-----------------+
| Head 1 | Head 2          |
+========+=================+
| Cell 1 | Cell 2 - line 1 |
|        | Cell 2 - line 2 |
+--------+-----------------+
| Cell 4 | Cell 5          |
+--------+-----------------+

Looks good eh? No? Oh well, this works::

    +--------+------------------+
    | Head 1 || Head 2          |
    +========+==================+
    | Cell 1 || Cell 2 - line 1 |
    |        || Cell 2 - line 2 |
    +--------+------------------+
    | Cell 4 || Cell 5          |
    +--------+------------------+

+--------+------------------+
| Head 1 || Head 2          |
+========+==================+
| Cell 1 || Cell 2 - line 1 |
|        || Cell 2 - line 2 |
+--------+------------------+
| Cell 4 || Cell 5          |
+--------+------------------+

We have to "double pipe" all entries down the column(s) we want to have text on separate lines, unfortunately, plus the headings or we get strange indents.

Bullet Point Lists
~~~~~~~~~~~~~~~~~~

These start with a hyphen and a space. Then the text of the list item follows on the same line. Do not press enter until you wish to start a new paragraph, and if intended to be part of the list item, it should be indented to line up under the first character after the hyphen space.

::

    - This is a single line item in a list.
    - This is another.

      However, this is not a third, but a second paragraph of the second list item.
  
    - And here we go back again. Item 3.
    
- This is a single line item in a list.
- This is another.

  However, this is not a third, but a second paragraph of the second list item.
  
- And here we go back again. Item 3.

You can nest lists::

    - A top level item.

      - a nested item.
      - And another.
      
    - Another top  level item.

- A top level item.

  - a nested item.
  - And another.
  
- Another top  level item.

And so on.  


Enumerated Lists
~~~~~~~~~~~~~~~~

These are similar to the above, but start with a digit, or a hash dot  (#.)::

    #. Item 1.
    #. Item 2.
    #. Item 3.

      #. Nested Item 1
      #. Nested Item 2

    4. Item 4.  

#. Item 1.
#. Item 2.
#. Item 3.

  #. Nested Item 1
  #. Nested Item 2

4. Item 4.  

In the above, we had to start item 4 with the digit 4. There might be a way to get t his to work automagically, I'm still looking.

We can use Letters too::

    a. Item a.
    #. Item b.
    #. Item c.

a. Item a.
#. Item b.
#. Item c.

Or Roman Numbers, but how? This should, but doesn't work::

    I. Item I
    #. Item II.
    #. Item III.
    #. Item IV.
    #. Item V.

I. Item I
#. Item II.
#. Item III.
#. Item IV.
#. Item V.

As you can see the above doesn't work! It should allow i,ii,iii etc and I,II,III and so on, but this one doesn't seems to work.

Definition Lists
~~~~~~~~~~~~~~~~

This is how we do definition lists::

    A Term
        A definition goes here.
        
    B Term
        B definition goes here. You can have many paragraphs too.
        
        Like this one you are currently reading.
    
A Term
    A definition goes here.
    
B Term
    B definition goes here. You can have many paragraphs too.
    
    Like this one you are currently reading.

    
Program Listings
~~~~~~~~~~~~~~~~



In-line
"""""""

This is an example of an inline section of code, ``1000 A$ = 'This is Fun!'``. We use the following to make it so::

    This is an example of an inline section of code, ``1000 A$ = 'This is Fun!'``.

Single line
"""""""""""

A single line of code is defined thus::

    ::

        100 PRINT "Hello World!"
    
Which renders to the following::

    100 PRINT "Hello World!"

The double colon can go at the end of the preceeding line, followed by a blank, followed by the indented code, or, can be on a line of its own, followed by a blank then the indented code.    

Multiple lines
""""""""""""""

Multiple lines of code are defined thus::

    ::

        100 REPeat Silly
        110   PRINT "Hello World!"
        120 END REPeat Silly
    
Which renders to the following::

        100 REPeat Silly
        110   PRINT "Hello World!"
        120 END REPeat Silly

The double colon can go at the end of the preceeding line, followed by a blank, followed by the indented code, or, can be on a line of its own, followed by a blank then the indented code.  

Character Formatting
--------------------

Bold is a pair of asterisks wrapped around the text yo uwant to be bold. No spaces between the leading asterisks and the text, or the end of the text and the trailing asterisks.

::

    This will be **bold** text.
    
Which gives the following:    

This will be **bold** text.

Italic is a single asterisk:

::

    This will be *italic* text.
    
Which gives the following:    

This will be **italic** text.

You want both? Tough, they cannot be nested.

Escaping Special Characters
---------------------------

The asterisk (\*), the invisible space, the underscore (\_), the backslash (\\) (and more?) are special and have to be escaped using a back slash character (\\)::

    Astersik = \*
    Underscore = \_
    Backslash = \\
    Invisible\ space (did you see it?)
    
Whic gives the followig:

    Astersik = \*

    Underscore = \_

    Backslash = \\

    Invisible\ space (did you see it?)


I think that's enough to be going on with! Check out `this link <http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html>`__ for better information, but the above is fine for me.

Links
-----

Oh yes, links, I forgot! Links are wrapped in backticks (\`) and double underscores (\_\_) as per the following::

    `link text here <URL Here>`__
    

- External links
    For example::

        This is a link to my `GitHub repository <https://github.com/NormanDunbar/SuperBASIC-Manual.git>`__. Try it.
        
    This is a link to my `GitHub repository <https://github.com/NormanDunbar/SuperBASIC-Manual.git>`__. Try it.

- Chapter & Section Headings 
    Each chapter and section heading becomes it's own link. Replace spaces, underscores etc with a hyphen in the link's URL to get to that section and lower case the remaining letters. For example::

        This is a link to the section above on `Escaping stuff <#escaping-special-characters>`__.
        
    This is a link to the section above on `Escaping stuff <#escaping-special-characters>`__.

    However, if the section in in another document, then this is required::

        This is a link to the `Python <software.html#python>`__ section in the Software chapter.
        
    This is a link to the `Python <software.html#python>`__ section in the Software chapter.



.. :rubrick: Footnotes

.. [#] RST is what I'm calling the ReStructuredText files from now on. It saves typing, and I'm basically lazy!