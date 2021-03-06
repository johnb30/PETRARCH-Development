PETRARCH
========

Code for the new Python Engine for Text Resolution And Related Coding Hierarchy (PETRARCH) 
event data coder. The coder now has all of the functions from the older TABARI coder 
and the new CAMEO.verbpatterns.140609.txt dictionary incorporates both parser-based matching 
and extensive synonym sets. The program coded 60,000 AFP sentences from the GigaWord corpus 
without crashing, using the included dictionaries.

For more information, please visit the (work-in-progress)
[documentation](http://petrarch.readthedocs.org/en/latest/#).

##Installing

Installing the program is as simple as:

`pip install git+https://github.com/openeventdata/petrarch.git`

This will install the program with a command-line hook. You can now run the program using:

``petrarch <COMMAND NAME> [OPTIONS]``

You can get more information using:

``petrarch -h``

**StanfordNLP:**

If you plan on using StanfordNLP for parsing within the program you will also
need to download that program. PETRARCH uses StanfordNLP 3.2.0, which can be
obtained from
[Stanford](http://www-nlp.stanford.edu/software/stanford-corenlp-full-2013-06-20.zip). 
PETRARCH's default configuration file assumes that this is unzipped and located
in the user's home directory in a directory named ``stanford-corenlp/``, e.g., ``~/stanford-corenlp``.

The program is stable enough that it is useable, and it is not *that* likely that there 
will be large changes in the API. 

##Running

###But first, a note.

It is possible to run PETRARCH as a stand-alone program. Most of our
development work has gone into incorporating PETRARCH into a full pipeline of
utilities, though, e.g., the [Phoenix pipeline](https://github.com/openeventdata/phoenix_pipeline).
There's also a RESTful wrapper around PETRARCH and CoreNLP named
[hypnos](https://github.com/caerusassociates/hypnos). It's probably worthwhile
to explore those options before trying to use PETRARCH as a stand-alone.

###With that out of the way...

Currently, you can run PETRARCH using the following command if installed:

``petrarch parse -i <INPUT FILE> -o <OUTPUT FILE>``

If not installed:

``python petrarch.py parse -i data/text/GigaWord.sample.PETR.xml -o test_output.txt``

There's also the option to specify a configuration file using the ``-c <CONFIG
FILE>`` flag, but the program will default to using ``PETR_config.ini``.

When you run the program, a ``PETRARCH.log`` file will be opened in the current
working directory. This file will contain general information, e.g., which
files are being opened, and error messages.

##Unit tests

Commits should always successfully complete

``petrarch validate``

This command defaults to the ``PETR.UnitTest.records.txt`` file included with the
program. Alternative files can be indicated using the ``-i`` option. For example
(this is equivalent to the default command):

``petrarch validate -i data/text/PETR.UnitTest.records.xml``

The final record should read

    Sentence: FINAL-RECORD [ DEMO ]
    ALL OF THE UNIT TESTS WERE CODED CORRECTLY. 
    No events should be coded
    No events were coded
    Events correctly coded in FINAL-RECORD
    Exiting: <Stop> record 

There's also a check of the basic functionalities of PETRARCH available using
`pytest`. If you have `pytest` installed simply run `py.test` in the top-level
directory.

##Compatibilities with TABARI dictionaries

PETRARCH has a much richer dictionary syntax than TABARI, and because PETRARCH uses 
parsed input, many dictionary entries used by TABARI for noun-verb disambiguation are 
no longer needed. While the initial versions of the program could use existing TABARI 
dictionaries, PETRARCH-formatted dictionaries are now required: these are available in 
this repository and in https://github.com/openeventdata/Dictionaries.
