# CIF - The Crystallographic Information File

## Introduction to the CIF

The small-molecule Crystallographic Information File (CIF: Hall, Allen &
Brown, *Acta Crystallographica*, **A47**, 655-685, 1991) is a universal
format for the electronic storage and exchange of crystallographic
information. It has been adopted as the international standard for this
purpose by the International Union of Crystallography (IUCr), and is
used in:

- Assembling laboratory archives.

- Transferring crystallographic information between laboratories.

- Depositing crystallographic information with most major journals.

- Depositing data with the crystallographic databases.

- As a database output format, e.g. for entries retrieved from the
    Cambridge Structural Database.

A CIF is an electronic ASCII file, which is intended to be human
readable and editable. It consists of a set of data items which may
appear individually or in looped lists. The lines in a CIF must not
exceed 2048 characters in length, although a soft limit of around 80
characters per line is often used for easy readability and to ensure
facile transmission via e-mail.

Full details of the small-molecule CIF, including leading references,
can be found on the IUCr website at [www.iucr.org](http://www.iucr.org),
and only a brief general introduction is provided here.

## Data Names, Data Values and Data Blocks in a CIF

Every *data item* is represented by a unique *data name* followed by its
associated *data value*.

Data items:

- Are described in a dictionary which defines meaning and usage.

- Must start with an underscore (underline) character.

- Can be any type of string (text, numeric or mixed), ranging from a
    single character to many lines of text.

Data values are *delimited* by:

- Spaces.

- Double or single quotes, to delimit a data value that contains
    spaces but does not span lines.

- Pairs of lines beginning with a semicolon, which delimit multi-line
    data items.

Data values may be set to:

- `?` (unknown).

- `.` (inapplicable).

Related data items, e.g. those which relate to an individual crystal
structure are grouped together in a *data block:*

- The beginning of a block is designated by the string `data_`
    prefixing the name of the block.

- The end of a block is recognized by another `data_` record, or by
    an end-of-file mark.

These principles are illustrated in the following examples:

```sh
data_structure_1
_cell_length_a             5.959(1)
_chemical_formula_moiety   ‘C23 H36 O7’
_publ_contact_author
;
Dr S. Motherwell
CCDC
12 Union Road
Cambridge CB2 1EZ
England
;
```

## Looped Lists of Data Items in a CIF

If a data name is preceded by `loop_` then a series of data values
may be associated with it. The following example shows four data values,
individual symmetry operators, associated with a single data name:

```sh
loop_
_symmetry_equiv_pos_as_xyz
‘x, y, z’
‘-x, y+1/2, -z+1/2’
‘-x, -y, -z’
‘x, -y-1/2, z-1/2’
```

It is also possible to group a series of data values together under a
series of different data names, i.e. to express a table of data values
within the CIF, by use of the `loop_` construction. This is
illustrated below for the atom labels and x,y,z-coordinates for four
atoms, where the data names can be regarded as the column headings for a
conventional printed table:

```sh
loop_
_atom_site_label
_atom_site_fract_x
_atom_site_fract_y
_atom_site_fract_z
I1 0.26639(7) 0.61557(3) 0.94292(3)
I2 0.64548(7) 0.36488(3) 0.56299(3)
P3 0.0438(2) 0.27607(11) 0.74432(13)
O1 -0.0989(7) 0.2488(3) 0.6619(4)
```

The end of a loop is recognized by:

- Any new data name, beginning with an underscore.

- Another `loop_` statement.

- A new block starting with a `data_` statement.

- An end-of-file mark.

## The CIF Dictionary

Valid CIF data names and the permitted data value type(s) for each name
are expressed in computer-readable dictionaries, where the dictionary
syntax is defined in a separate Dictionary Definition Language (DDL).
Thus, the dictionary entry for `_cell_length_a` specifies that the
data value will be in Angstroms and that a standard uncertainty (ESD) is
allowed, placed in parentheses immediately following the value.

EnCIFer is able to load dictionaries which conform to the DLL1.4.1
format (referred to as DDL1) including the small molecule core
dictionary and the powder diffraction dictionary. The current DDL1
dictionaries available from the IUCr are included in the EnCIFer
distribution with the permission of the IUCr, who hold the copyright.
EnCIFer supports neither DDL2 nor the proposed DDLm, CIF files or
dictionaries, e.g. the macromolecular CIF dictionary mmCIF.

The latest small-molecule core and other DDL1 dictionaries and details
of the DDL can be found on the IUCr website:
[www.iucr.org](http://www.iucr.org). This site also describes the
operation of COMCIFS, the IUCr Committee that oversees CIF development
and the approval of additional CIF data names.

## Generating and Editing a CIF

The crystallographic part of a CIF is normally generated automatically
by the software package used for structure refinement. These CIF
generators have been tried and tested over the past decade, and it is
seldom necessary to amend any of these data items. Obviously, the
software package can only output data items that it knows about, i.e.
those items that are input to, or are generated by, the refinement
process, or which can reliably be deduced from these data.

For most purposes, it is necessary to edit into the CIF those additional
data items that are needed for archival purposes, or for transmission of
the CIF to a colleague, journal or database. These data items might
include authors’ names and addresses, chemical or physical data, such as
chemical compound names, the melting point, etc.

Some journals permit the text of the manuscript to be incorporated into
the CIF using specific data names. The CIF standard includes support for
simple typesetting features such as subscripts, superscripts and
consequences of multiple ASCII characters (digraphs or trigraphs) to
express non-Roman characters, mathematical symbols etc.

If a CIF is amended or enhanced by manual editing, it is quite easy to
destroy the integrity of the CIF format, so that it cannot be parsed and
interpreted by the many programs (structure validation software,
structure visualizers, etc.) that are now designed to read CIF data. It
is because of these pitfalls in manual editing that the EnCIFer program
has been written.

## Depositing CIFs with Journals and the CCDC

Nearly all journals now expect or require that crystal structure data
associated with published papers shall be deposited in CIF format.
Authors should consult the Notes for Authors for their chosen journal to
see their most recent arrangements for depositing CIF data.

Many major journals have arrangements with the Cambridge
Crystallographic Data Centre, whereby the CIF is deposited with the CCDC
before the paper is submitted for publication. The CCDC supplies a CCDC
Deposition Number and authors include this number in their submitted
manuscript. This number is printed in the published paper and is stored
in the Cambridge Structural Database, where it affords a valuable link
to electronic versions of the journal and allows scientists to request
individual datasets free of charge from the CCDC.

The CCDC also accepts CSD Communications (previously called *Private
Communications to the CSD*), i.e. crystal structures for which formal
journal publication is not envisaged. The data will be checked and
evaluated before inclusion in the CSD, and any problems clarified with
the depositor. The author(s) name(s) and contact address will be
included in the CSD.

Full details about CIF deposition to the CCDC, for both journal
publications and for CSD Communications, can be found on the CCDC
website at [www.ccdc.cam.ac.uk](http://www.ccdc.cam.ac.uk).
