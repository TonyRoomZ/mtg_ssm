mtg-ssm - Magic: the Gathering Spreadsheet Manager
===================================================

.. image:: https://img.shields.io/coveralls/gwax/mtg_ssm.svg
    :target: https://coveralls.io/r/gwax/mtg_ssm

.. image:: https://img.shields.io/travis/gwax/mtg_ssm/master.svg
    :target: https://travis-ci.org/gwax/mtg_ssm

.. image:: https://img.shields.io/pypi/v/mtg-ssm.svg
    :target: https://pypi.python.org/pypi/mtg-ssm/

.. image:: https://img.shields.io/pypi/pyversions/mtg-ssm.svg
    :target: https://pypi.python.org/pypi/mtg-ssm/

.. image:: https://img.shields.io/pypi/dm/mtg-ssm.svg
    :target: https://pypi.python.org/pypi/mtg-ssm/

`mtg-ssm`_ is a tool for creating/updating user-friendly spreadsheets with
Magic: the Gathering collection information. The tool can also
import/export data to/from these spreadsheets to other formats, such as
CSV files.

.. _mtg-ssm: https://github.com/gwax/mtg_ssm

As a matter of convenience, you can store the created spreadsheet in
Dropbox, Google Drive, or the like and access your collection from
anywhere.

Installation
============

mtg-ssm is available on PyPI so, if you have python (>=3.3) and pip
installed on your system, you should be able to get mtg-ssm by entering
the following into a terminal:

.. code:: bash

    pip3 install mtg_ssm

Updates can be performed by entering:

.. code:: bash

    pip3 install -U mtg_ssm

You can verify installation from the terminal by running:

.. code:: bash

    mtg-ssm --help

Usage
=====

For first time use, you will want to create an empty spreadsheet with
card data:

.. code:: bash

    mtg-ssm create collection.xlsx

In the future, when new sets are released, you will want to update your
collection spreadsheet while keeping existing counts:

.. code:: bash

    mtg-ssm update collection.xlsx

Existing collections
--------------------

If you already have your cards in another collection store, you might
want to import that collection into your card spreadsheet.

First create an input csv file:

.. code:: bash

    mtg-ssm create input_data.csv

Then modify the template to match your counts and import into your
spreadsheet:

.. code:: bash

    mtg-ssm merge collection.xlsx input_data.csv

Export / import to deckbox
--------------------------

If you already have your cards entered into `Deckbox`_, you can export a
csv from deckbox and import the contents into a spreadsheet just as you might
merge from an existing collection using the "deckbox" import format:

.. _Deckbox: https://deckbox.org

.. code:: bash

    mtg-ssm --dialect csv deckbox merge collection.xlsx Inventory_username_2016.March.10.csv

Alternatively, if you have your collection in a spreadsheet already and would
like to load your data into deckbox to check prices or share with other people,
just go the other direction.

.. code:: bash

    mtg-ssm --dialect csv deckbox merge inventory.csv collection.xlsx

Deckbox Warning
~~~~~~~~~~~~~~~

MTG JSON, which we use for card data doesn't always map 1-to-1 to cards in
Deckbox. This means that data can lose granularity in going from one form
to the other, or back. If you intend to use both native mtg-ssm spreadsheets
and Deckbox, I encourage you to choose one to be authoritative and always
export to the other; going back and forth is probably not a good idea.

The following conversion issues are known to exist:

-   Sets that contain multiple versions of the same card (ex. Thallid in Fallen
    Empires) may lose track of the specific version when going back and forth.
-   Alternate art cards (ex. Ertai, the Corrupted in Planeshift) may lose track
    of the art version when going back and forth.
-   Not all Clash Pack cards are available in mtg-ssm.

Contributions
=============

Pull requests are welcome and contributions are greatly appreciated.

Issues can be reported via GitHub.

Acknowledgments
===============

-   `Wizards of the Coast`_: For making Magic: the Gathering and continuing
    to support it. Off and on, it's been my favorite hobby since the
    early '90s.
-   `MTG JSON`_: MTG JSON is an amazing resource for anyone looking to build
    tools around magic card data. It is pretty much **THE** source for
    structured magic card data. Without MTG JSON this project would not have
    been possible.

.. _Wizards of the Coast: http://magic.wizards.com
.. _MTG JSON: http://mtgjson.com


Changelog
=========

1.3.6
-----

-   Removed support for Python 3.3
-   Test and bug fixes
-   Handle newer versions of mtgjson

1.3.5
-----

-   Remove profiling code. If we care, we can invoke profiling with:

    .. code:: sh

        python -m cProfile -o mtg_ssm.prof mtg_ssm/ssm.py create collection.xlsx

-   Fix wheel generation to only build py3 wheels.

1.3.4
-----

-   Increase in verbosity when looking up cards by heuristics (instead of id).

1.3.3
-----

-   Fixed support for Ae/Æ
-   Increased verbosity when searching for cards with a mismatched id
-   Performance improvements
-   Add tests to catch potential missing card issues

1.3.2
-----

-   Changed the backup file naming convention; date is now before extension
-   Minor tweaks and performance enhancements

1.3.1
-----

-   Fix bug where were were never actually reading set names from xlsx
    files.

1.3.0
-----

-   Complete rework of cli (see `--help` for details)

    -   cli is **NOT** the same; old commands will **NOT** work
    -   new global argument flags and dialect selection mechanisms
    -   create: create a new collection
    -   update: update an existing collection
    -   merge: merge multiple collections
    -   diff: get a diff of two collections

-   Lots of under the hood changes and performance improvements
-   Files are still compatible

1.2.4
-----

-   Remove workarounds introduced in 1.2.3

1.2.3
-----

-   Hack to work around missing "releaseDate" and "type" in MTG JSON 3.3.14

1.2.2
-----

-   Add "All Cards" page with index of all cards in XlsxSerializer.

1.2.1
-----

-   Add support for deckbox.org import/export.
-   Backend improvements.

1.2.0
-----

-   Complete rework of the serialization architecture.
-   Rebuild of the manager cli.
-   Incompatible CLI interface changes. See help for new usage information.

1.1.0
-----

-   Complete rework of the data model storage. Drop sqlite based data models in
    favor of custom classes and dict based indexes.
-   Switch to accepting all versions of MTGJSON instead of bumping for every
    release.

1.0.2
-----

-   Version bump MTGJSON support.

1.0.1
-----

-   Fixed some PyPI related issues.

1.0.0
-----

-   Initial stable release.
