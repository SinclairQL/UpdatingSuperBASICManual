=================
ReStructured Text
=================

ReStructuredText (which apparently always has to be written like 'reStructuredText`!) is a plain text markup language. It is supposed to be readable even without conversion to other formats, unlike DocBook XML, etc, but it's not as simple to read as something like Markdown, for example. However, it's quite a powerful system.

Check out `this cheatsheet <http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html>`__ for better information on using RST [#FN1]_ in Sphinx (which is what we are doing after all).

For a full description of the RST "language", try any of the following links:

- `Docutils main page <http://docutils.sourceforge.net/rst.html>`__
- `Quick introduction <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`__
- `Deep stuff <http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html>`__
- `Sphinx primer <http://www.sphinx-doc.org/en/1.5.1/rest.html>`__

And, the ever faithful, `Wikipedia <https://en.wikipedia.org/wiki/ReStructuredText>`__\.

RST, can be converted into numerous other output formats using Sphinx (as we are for the SuperBASIC Manual) or by using a utility named ``pandoc`` we can even create Word and/or Libre Office documents - with user defined styles etc - as desired.


Comments
--------

You may find that it is useful to add a comment to the RST source code for the manual page you are editing/creating. This is done as follows::

    .. This is a comment. It is on a single line.
    
Comments have no effect on the generated output in HTML etc. If the comment needs to be longer than a single line, add additional lines and/or paragraphs (see below) as necessary.  

Section Headings
----------------

A section heading is simply the heading text, underlined by some combination of punctuation characters. Sphinx is quite good at determining the hierarchy, but it pays to be consistent. I use the following::

    =================
    Title of Document
    =================
    
    Heading 1
    =========
    
    Heading 2
    ---------
    
    Heading 3
    ~~~~~~~~~
    
    Heading 4
    """""""""
    
The document title is overlined as well as underlined.

You can go down another couple of levels, but it gets a bit messy. HTML only allows 6 levels of heading, so that's probably about as much as anyone should need. Unless you work in a legal establishment, of course, they do like to complicate things!

It is advisable to add *reference link destinations* above each section header, if you intend to set up links, from other source files, to any of the sections in "this" source file. For example, if another source file wishes to link to Heading 2 above, this file should give heading 2 a link destination, as follows::

    .. _Heading-two:
    
    Heading 2
    ---------

See :ref:`LinksToOtherRSTDocuments` below for full details.
    
    
Paragraphs
----------

Start typing at the left margin. Don't stop typing at the end of a line - but if you do, don't worry, the line feed will be ignored, and replaced with a space as the various lines making up the paragraph are merged.

Leave a blank line between paragraphs, otherwise it all runs into one.

If you happen to indent a paragraph with a leading tab, or spaces, then the following will happen:

    This paragraph is full of useless text and is indented using a TAB. Each line of the paragraph - thanks to the Notepad++ editor - will also align with the indent. 

    This paragraph, on the other hand, is indented using leading spaces, 4 to be precise, and subsequent lines also indent with 4 spaces - thanks again to Notepad++. You can see what the results are in both cases.

    
Character Formatting
--------------------

Bold formatting is facilitated by a pair of asterisks wrapped around the text you want to be bold. No spaces are allowed between the leading asterisks and the text, or the end of the text and the trailing asterisks.

::

    This will be **bold** text.
    
Which gives the following:    

This will be **bold** text.

Italic text uses a single asterisk:

::

    This will be *italic* text.
    
Which gives the following:    

This will be **italic** text.

You want both? Sorry, they cannot be nested. As this shows::

    **This is bold *this should be italic+bold, but isn't* - but this is still bold!**

**This is bold *this should be italic+bold, but isn't* - but this is still bold!**

Subscript and superscript need a slightly different format. You put the text to be raised or lowered in between backtick characters, not single quotes::    

    e=mc :sup:`2`
    
e=mc :sup:`2`  

This is fine if you want the space prior to the superscripted text, but if not, use the 'invisible space' character to prevent the space from appearing. That character is explained below. For example::

    e=mc\ :sup:`2`
    
e=mc\ :sup:`2`  

Which, to me, is much better looking *and* it won't accidentally get used as a word break in a paragraph!

Subscript is the same::

    Sulphuric Acid has the formula: H\ :sub:`2`\ SO\ :sub:`4`.
  
Sulphuric Acid has the formula: H\ :sub:`2`\ SO\ :sub:`4`.
  

Escaping Special Characters
---------------------------

The asterisk (\*), the backtick (\`), the invisible space, the underscore (\_), the backslash (\\) (and more?) are special and have to be escaped using a back slash character (\\)::

    - Asterisk = \*
    - Underscore = \_
    - Backslash = \\
    - Backtick = \`
    - Invisible\ space (did you see it?)
    
Which gives the following:

- Asterisk = \*
- Underscore = \_
- Backslash = \\
- Backtick = \`
- Invisible\ space (did you see it?)

The invisible space is used in places where the end of some special formatting needs to be shown to be separate from the following text. Sometimes, for example, when using sub\ :sub:`script` or super\ :sup:`script`, or occasionally when you have a full stop following the end of a URL, for example. The invisible space tells the parser to stop parsing and that the text following the "space" is to be considered as a separate parsing entity.

The text above, where we have subscript and superscript, was created as follows::

    Sometimes, for example, when using sub\ :sub:`script` or super\ :sup:`script`, or occasionally ... 

You can see the use of the invisible space to separate the ':sub:' and ':sup:' from the first part of the word.



Syntax/Location Table
---------------------

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

    
However, if there are alternate forms for the command, the table should look like this::

    +----------+-----------------------------------+
    | Syntax   | Command(a,b) or                   |
    |          +-----------------------------------+
    |          | Command(a,b,c)                    |
    +----------+-----------------------------------+
    | Location | QL ROM, TOOKIT II, SOMEWHERE ELSE |
    +----------+-----------------------------------+


which becomes the following after a build:

+----------+-----------------------------------+
| Syntax   | Command(a,b) or                   |
|          +-----------------------------------+
|          | Command(a,b,c)                    |
+----------+-----------------------------------+
| Location | QL ROM, TOOKIT II, SOMEWHERE ELSE |
+----------+-----------------------------------+


Which gives a better layout in the generated HTML. 

..  note:

    The above format is not yet fully in use in the manual. There is another layout for the table when there are more than one syntax, but it doesn't render correctly in PDF, so this version should be used instead.

You might think that the following will work::

    +----------+-----------------------------------+
    | Syntax   | Command(a,b) or                   |  
    |          | Command(a,b,c)                    |
    +----------+-----------------------------------+
    | Location | QL ROM, TOOKIT II, SOMEWHERE ELSE |
    +----------+-----------------------------------+

Unfortunately, it doesn't. The data in the cell(s) are reformatted and multiple spaces and/or line feeds will be removed and replaced by a single space - just like HTML does. You can see how it *doesn't* look correct here:

+----------+-----------------------------------+
| Syntax   | Command(a,b) or                   |
|          | Command(a,b,c)                    |
+----------+-----------------------------------+
| Location | QL ROM, TOOKIT II, SOMEWHERE ELSE |
+----------+-----------------------------------+

    
Tables
------

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

Getting text on separate lines within cells is interesting, and a bit of a hack. You've already seen it above for the Syntax/Location tables, but here we are again::

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

Looks good eh? No? Oh well, this works, but only for HTML output::

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

The best looking result, which works in HTML, PDF and (as far as I can tell) all other formats, is to merge cells::

    +--------+-----------------+
    | Head 1 | Head 2          |
    +========+=================+
    | Cell 1 | Cell 2 - line 1 |
    |        +-----------------+
    |        | Cell 2 - line 2 |
    +--------+-----------------+
    | Cell 4 | Cell 5          |
    +--------+-----------------+

+--------+-----------------+
| Head 1 | Head 2          |
+========+=================+
| Cell 1 | Cell 2 - line 1 |
|        +-----------------+
|        | Cell 2 - line 2 |
+--------+-----------------+
| Cell 4 | Cell 5          |
+--------+-----------------+
    

Lists
-----

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

In the above, we had to start item 4 with the digit 4. There might be a way to get this to work automagically, I'm still looking.

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
        
        Like this one you are currently reading. Just make sure that each paragraph is separated by a blank line, and indented to the same level.
    
A Term
    A definition goes here.
    
B Term
    B definition goes here. You can have many paragraphs too.
    
    Like this one you are currently reading. Just make sure that each paragraph is separated by a blank line, and indented to the same level.

    
Program Listings
----------------

In-line
~~~~~~~

This is an example of an inline section of code, ``1000 A$ = 'This is Fun!'``. We use the following to make it so::

    This is an example of an inline section of code, ``1000 A$ = 'This is Fun!'``.

    
Single line
~~~~~~~~~~~

A single line of code is defined thus::

    ::

        100 PRINT "Hello World!"
    
Which renders to the following::

    100 PRINT "Hello World!"

The double colon can go at the end of the preceding line, followed by a blank, followed by the indented code, or, can be on a line of its own, followed by a blank then the indented code.

If the double colon is at the end of a line of text, then a single colon will be created in the output. If the double colon is on a line of its own, then no colons will be generated.   


Multiple lines
~~~~~~~~~~~~~~

Multiple lines of code are defined thus::

    ::

        100 REPeat Silly
        110   PRINT "Hello World!"
        120 END REPeat Silly
    
Which renders to the following::

        100 REPeat Silly
        110   PRINT "Hello World!"
        120 END REPeat Silly

The double colon can go at the end of the preceding line, followed by a blank, followed by the indented code, or, can be on a line of its own, followed by a blank then the indented code. 

Code Highlighting
-----------------

Give the above for single and multiple line code listings, you can add syntax highlighting, if desired. Sphinx uses a Python library called `pygments <http://pygments.org/>`__ to do the syntax highlighting. To use this in your docs, simply set up your code blocks as follows::

    .. code-block:: python
        
        total = 0
        
        # Remember, range(a, b) is from a to (b-1) inclusive!
        for x in range(1, 667):
            total += x
            
        print("The sum of all the numbers from 1 to 666 is %d" % (total))

Unfortunately, MC68000 assembly language and SuperBASIC do not have highlighters defined. yet!

The above source code renders to the following:

    .. code-block:: python
        
        total = 0
        
        # Remember, range(a, b) is from a to (b-1) inclusive!
        for x in range(1, 667):
            total += x
            
        print("The sum of all the numbers from 1 to 666 is %d" % (total))


Links
-----

Normal http:// type links do not need any special formatting - they are identified as links to a URL, and will be rendered as such. Links within the document, either in the current source file, or to other source files, do require a bit of formatting.

The general format for links is::

    `link text here <URL Here>`__
    
The various different link types are detailed below.

External links
~~~~~~~~~~~~~~

For example::

    This is a link to my `GitHub repository <https://github.com/NormanDunbar/SuperBASIC-Manual.git>`__. Try it.
    
This is a link to my `GitHub repository <https://github.com/NormanDunbar/SuperBASIC-Manual.git>`__. Try it.

Chapter & Section Headings 
~~~~~~~~~~~~~~~~~~~~~~~~~~

Each chapter and section heading becomes it's own link but *only within the same source file*. You simply enclose the chapter or section header in backticks and a trailing underscore to create a link::

    This one links to `Code Highlighting`_ above.
    
This one links to `Code Highlighting`_ above.

Embedded underscores etc need to be escaped.

Sadly, cross source file links cannot be created this way, as this example demonstrates. It tries to link to a section heading in part two::

    `Forking the Repository`_ is a good place to start...
    
`Forking the Repository`_ is a good place to start...
    
All you get is an errors when building the document::

    ERROR: Unknown target name: "forking the repository".

If you wish to put your own text rather than the section header, you should replace spaces, underscores etc with a hyphen in the link's URL to get to that section and lower case the remaining letters. For example::

    This is a link to the section above on `Escaping stuff <#escaping-special-characters>`__.
    
This is a link to the section above on `Escaping stuff <#escaping-special-characters>`__.

However, if the section in in another document, *and* only HTML is to ever be generated, then the following will work, but hard codes the output file::

    This is a link to the `Python <software.html#python>`__ section in the Software chapter.
    
This is a link to the `Python <software.html#python>`__ section in the Software chapter.

Sadly, this latter link will only work for HTML formatted output. If you generate other formats - PDF for example - then there will be warnings that the link is not valid and indeed, the link will not work. 

For best results, regardless of the output format desired, see the next item.

.. _LinksToOtherRSTDocuments:
    
Links to Other RST documents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you need to link to a section heading in this, or *another* RST document, then you must use the ':ref:' directive as shown in the following::

    This is a link to :ref:`P2_FreeGitBook` which should be found in part 2 of this manual.

Additionally, and in order to make the link work, you need to create the link named 'P2_FreeGitBook' at the appropriate place in the other document. For best results links to other documents should point at a section or sub-section heading, so put the link just above that location::

    .. _P2_FreeGitBook:

    Free Git Book
    -------------

    You might like to download and read the *Pro Git* book, by Scott Chacon & Ben Straub. This is a book published by Apress but which is given away for free on the web at https://git-scm.com/book/en/v2 - various formats are available.
    
    ...

This is a link to :ref:`P2_FreeGitBook` which should be found in part 2 of this manual.

You will note that the text inserted as the link text, is the section header of the section immediately following the link definition (in the other document), in this case, 'Free Git Book'.
    
    
Footnotes
---------

And finally, for now, footnotes. You add a footnote indicator to your text like this::

    This text has a footnote [#foot_1]_ embedded in it.

This text has a footnote [#foot_1]_ embedded in it.

..  note::

    You can, if you don't like the space before the footnote indicator in the generated text, use an invisible space as described above. I prefer to use one myself, but it's not essential. For example::
   
       This text has a footnote\ [#foot_1]_ embedded in it.

At the *bottom* of the file you are adding the footnote to, you add the following::

    .. :rubrick: Footnotes

And then, beneath that you add the footnote text for *all* the footnotes in this current file::

    .. [#foot_1] This is the example footnote.    
    .. [#foot_2] This is another footnote.
    

There are other ways of adding footnotes, but I find this to be the best as you explicitly name each footnote. RST allows auto numbering of footnotes, but then you must remember to add in new footnotes in the same order after the ``.. rubrick: Footnotes``, as they appear in the text - or it all gets messy!


    
.. :rubrick: Footnotes

.. [#FN1] RST is what I'm calling the ReStructuredText files from now on. It saves typing, and I'm basically lazy!
.. [#foot_1] This is the example footnote.