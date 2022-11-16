# Syntax and Dictionary Checking

## Error, Warning and Remark Display Windows

When a CIF is opened in EnCIFer, it is parsed to check for CIF syntax
and CIF dictionary compliance. Optionally, it may be checked for the
presence of mandatory data items and data consistency.

Error, warning, and remark messages are displayed in an expanding list
view on the lower left, and a summary is written to a scrolling log at
the lower right of the window.

The relative widths of the two windows may be altered by clicking and
dragging the vertical splitter between the windows (the <-||->
cursor should appear).

The scrolling log may be cleared by right-clicking in the **Log** window
and selecting **Clear** from the resulting pop-up menu.

## Updating Error, Warning and Remark Messages

After the CIF has been edited, the file may be re-parsed to re-check for
errors and warnings by:

- Hitting **Tools** on the top-level menu and selecting **Check**.

- Clicking the **Re-check** icon in the toolbar.

- Using the **Ctrl+K** keyboard shortcut.

Any errors or warnings are added to the scrolling log. The expanding
    list view is updated to show the current error and warning messages.

## Navigating Error, Warning and Remark Messages

To expand the list view:

- Click the **Expand** icon alongside the red *errors*, yellow
    *warnings*, or blue *remarks* triangles.

Double-clicking on an error, warning or remark message in the list view
moves the cursor to the corresponding line in the CIF, provided that the
CIF has not been edited so as to change the line numbering since the CIF
was last parsed. The corresponding line is then highlighted in yellow.
For a few errors, such as those for duplicate data item names, two lines
will be highlighted, one in yellow and the other in green.

Right-clicking on the error, warning or remark message shows the
documentation help for the message. This includes advice on common
causes of the error, warning or remark and how to correct them.

## Configuring the Number of Error and Warning Messages

The number of error and warning messages displayed can be configured in
the **Preferences** dialog box:

1. Hit **Edit** in the top-level menu, select **Preferences**, and
    click the **CIF checking** tab.

1. The **Maximum consecutive error lines** setting controls how many
    consecutive error lines may be encountered before error checking is
    abandoned. It also controls the number of consecutive warning lines
    which are shown, further warnings being omitted until after a line
    without warnings is encountered.

1. To change the setting, type in the **Text** edit box or use the
    arrows to increment or decrement the number.

1. Click the **OK** button to apply a change, **Defaults** to return to
    the default setting or **Cancel** to abandon changes.

## CIF Dictionary Options

EnCIFer loads DDL1.4.1 dictionary files with the extension .dic in the
dict directory of the distribution on startup (see [The CIF Dictionary](encifer-02.md#the-cif-dictionary)).
The **Output** pane reports which dictionaries have been loaded and any
errors in reading dictionaries.

Additional DDL1.4.1 dictionaries with the extension .dic may be added to
this directory if you have write permission, or the dictionaries can be
updated with more recent versions.

By default, all dictionaries which are loaded successfully are enabled
and used to check the CIF data items and values. Individual dictionaries
may be disabled in the **Preferences** dialog box:

1. Hit **Edit** in the top-level menu, select **Preferences** and click
    the **Dictionaries** tab.

1. The available dictionaries are listed in a spreadsheet, with
    associated version numbers and dates.

1. Click the appropriate checkboxes in the spreadsheet to enable or
    disable particular dictionaries.

## Soft Line-Length Limit

The current CIF 1.1 specification permits lines up to 2048 characters in
length, whereas CIF 1.0 only permitted lines 80 characters or less.
EnCIFer will give an error if a line exceeds a hard limit of 2048
characters or a warning if a line exceeds a soft limit which can be set
in the range 72-2048 characters (default 80) in the **Preferences**
dialog box:

1. Hit **Edit** in the top-level menu, select **Preferences** and click
    the **CIF checking** tab.

1. To set the desired limit, type in the **Text** edit box or use the
    arrows to increment or decrement the number.

## Mandatory Data Items

### Overview of Mandatory Data Items

EnCIFer can check for the presence of data items, listed in configurable
files, required by journal publishers or crystallographic databases (see
[Format of the Mandatory Data Items File](encifer-07.md#format-of-the-mandatory-data-items-file)
and [Setting the Mandatory Data Items File](encifer-07.md#setting-the-mandatory-data-items-file)).

A distinction is made between blocks comprising publication information,
(`_journal`, `_publ`) chemical and crystallographic data,
(`_atom_site`, `_atom_sites`, `_cell`, `_chemical`,
`_diffrn`, `_exptl`, `_geom`, `_refine`, `_symmetry`) or
both. A remark message is given if a data name is not present in an
appropriate data block or if the data value is `?` (unknown). No
remark is given if the data value is `.` (inapplicable). If there is
no block in the CIF of a particular type, remarks are given for the
first block.

If a data item has an *alternate* or *replace* relation to another data
item in the CIF dictionary, the related data item is also checked. If a
related item is present in the data block with a value other than `?`
(unknown) no remark is generated, e.g. no remark will be given for:
`_refine_ls_R_factor_gt` if the alternate term
`_refine_ls_R_factor_obs` is set.

### Format of the Mandatory Data Items File

This file is in plain text CIF format, with up to three blocks:

- `data_publication` - items required in publication data blocks.

- `data_crystal` - items required in crystal data blocks.

- `data_all` - items required in all blocks.

The required data items are listed in each text block (the data item
value is ignored), e.g.

```sh
# Data required in publication information blocks
data_publication
_publ_contact_author_name ?
_publ_contact_author_address ?

# Data required in crystal data blocks
data_crystal
_cell_length_a
...
_symmetry_equiv_pos_as_xyz
```

### Setting the Mandatory Data Items File

In order to set the mandatory data items in the file:

1. Hit **Edit** on the top-level menu and select **Preferences**.

1. In the **Preferences** dialog box, click the **CIF checking** tab,
    hit the **Browse** button and select the template file in the
    **Open** dialog box.

1. Check the **Check for Mandatory Data Items** box to enable checks
    using the contents of this file.

1. A file, `recommended.cif`, is provided with the EnCIFer
    distribution. This contains a list of items that are commonly
    required by chemistry journals which publish the results of crystal
    structure determinations, and for deposition at the CCDC. This file
    may be customized to suit the requirements of a particular journal.

1. Some additional mandatory data items files are provided which are
    already tailored to the requirements of particular journal
    publishers e.g., `mandatory_rsc.cif`. Please refer to the comments
    in these files, detailing the conditions of use, and to the notes
    for authors for the particular journal.

1. As these files are themselves in CIF format, they can also be opened
    and edited using EnCIFer.

## Data Item Consistency Checks

EnCIFer performs some consistency checks between related data item
values. Failures of these checks appear as remarks or warnings, as
appropriate. By default, the checks are enabled, to adjust this setting:

1. Hit **Edit** on the top-level menu and select **Preferences**.

1. In the **Preferences** dialog box, click the **CIF checking** tab,
    check or uncheck the **Perform data consistency checks** box.

Details follow on each of the checks made.

If any of the data items mentioned in the checks are not present or have
`?` or `.` values, the check is not performed, and no messages
generated.

### Symmetry Operator-Space group Name Consistency

This checks that if a space group name is provided in a
`_symmetry_space_group_name_H-M` item it is consistent with symmetry
operators provided in `_symmetry_equiv_pos_as_xyz`. Related data item
names will be used as appropriate.

### Atom Label Uniqueness

Looped `_atom_site_label` values are checked to ensure they are
unique.

### Formula Weight Consistency

A `_chemical_formula_weight` value is checked to be within 1.1
Daltons of the weight calculated from the value of
`_chemical_formula_sum`.

## Summary of Error Messages

These usually indicate serious errors in the CIF syntax. The error
messages include:

- Data item \<data name\> has already been set in this data_
    block.

- No data items in loop_.

- Too many or too few data values in the loop.

- Data name \<data name\> immediately followed by another data
    name.

- Data name \<data name\> more than 75 characters long.

- Data name \<data name\> not followed by data value.

- CIF contains more than one data block called \<data block\>.

- CIF contains no data_ blocks.

- No terminating (‘) quote.

- No terminating (“) quote.

- Text block finished at end of file without final ‘;’ .

- Text block finished at end of file without final ‘;’ .

- (Line) More than 2048 characters long.

- Invalid non-printable character \<octal value\>.

- Invalid printable character \<octal value\>.

- Closing (;) semicolon not followed by white space.

### Data item \<data name\> has already been set in this data_ block

This error occurs if the same data name appears more than once in the
same data block. This can happen if a data block header has been omitted
or incorrectly formatted, such that two blocks are interpreted as one.

### No data items in loop_

This error occurs if the `loop_` keyword is present, but it is not
followed by any data item names. This can happen if the `loop_`
keyword is followed immediately by data values or another CIF keyword.

### Too many or too few data values in the loop

This error indicates that the number of data values in the loop is not
an exact multiple of the number of data item names given in the loop.
Typical causes of these problems include:

- No data values in the loop, just data names. Every data name must
    have at least one data value in the loop.

- Spacing is omitted between values in the loop, e.g. `...` should
    be `. . .`

- Quotes are omitted around data values such that they are interpreted
    as multiple values rather than a single value, e.g. `J. A. Smith`
    should be `‘J. A. Smith’`.

- Text after the loop is interpreted as data values, e.g. because a
    data name has been omitted, a comment (#) character omitted or a
    keyword has been misspelt.

### Data name \<data name\> immediately followed by another data name

This error occurs when there are two consecutive data names. The first
data name should be followed by a data value.

### Data name \<data name\> more than 75 characters long

Data names may be no more than 75 characters in length.

### Data name \<data name\> not followed by data value

This error occurs when a data name is followed by another keyword (e.g.
`loop_` or `data_`). The data name should be followed by a data
value before the keyword.

### CIF contains more than one data block called \<data block\>

This error occurs when more than one data blocks have the same name in
the data block header. All data blocks must be given a unique name.

### CIF contains no data_ blocks

This error occurs if there are no data block headers
(`data_<name>`).

### No terminating (“) quote

These errors occur if a data value has an opening but not a closing
single or double quote on the same line, or if there is a spurious
opening quote (e.g. `‘psi-scan` should be `psi-scan`, `‘psi-scan’`
or `“psi-scan”`). This can occur if a data value delimited by single
or double quotes has been split over two lines. This can sometimes
happen if email or other software wraps text lines at less than 80
characters.

Either the text should be moved to the same line, or be treated as a
multiple line value and delimited with semicolons.

### Opening (;) semicolon not first character on line & Terminating (;) semicolon not first character on line

These errors occur if semicolons delimiting a text string are the first
non-space characters on a line but are not the first character as
required. Any spaces before the semicolons should be deleted.

### Text block finished at end of file without final ‘;’

This error indicates that a closing semicolon has been omitted, causing
the remainder of the CIF to be interpreted as a runaway multiple line
data value, or there is an additional spurious semicolon in the CIF
which has the same effect. It is important to ensure that all semicolons
occur in pairs around data values. The syntax highlighting in the editor
should help to show the cause of this problem.

### (Line) More than 2048 characters long

The CIF 1.1 specification requires lines to be no more than 2048
characters in length. Line breaks should be inserted to ensure all lines
are 2048 characters or less in length. Where necessary, single or
double-quoted strings should be converted to semicolon-delimited
multiple-line strings to conform to the line length limit.

### Invalid non-printable character \<octal value\> & Invalid printable character \<octal value\>

These messages indicate that the CIF contains characters which are not
included in the allowed character set. The characters have their own
syntax highlighting style so that they can be easily seen on the lines
containing these errors.

Non-printable characters are usually control characters, whereas
printable characters may be accented characters or special symbols.
Printable characters should be converted to the CIF digraph or trigraph
sequences.

Select the **Special characters** dialog box from the top-level **Help**
menu. If the printable character displays correctly in the **Editor**,
it is usually possible to do the conversion automatically by cutting and
pasting the text containing the invalid characters. Non-printable
characters should be converted to spaces or be deleted altogether.

### Closing (;) semicolon not followed by white space

When a semicolon delimited text block is closed, it must be followed by
at least one white space character. This white space character will
often be a new line, but spaces are sometimes used within loops.

This error is most often found within a loop where all values are
quoted, for example author names and addresses. It can also be found
where values are immediately followed by comments. For example, the
following will generate this error as there is no space between `;`
and `#`.

```sh
_publ_contact_author_address
;
12 Union Road
Cambridge
CB2 1RF
;# comment
```

## Summary of Warning Messages

These include warnings:

- For less serious CIF syntax errors.

- Where data names are not found in the currently enabled CIF
    dictionaries.

- Where data values do not conform to the values permitted for the
    corresponding data names in the CIF dictionaries.

### CIF Syntax Warning Messages

This section contains a list of all commonly occurring CIF syntax
warning messages:

- Missing identifier for data_ block.

- Data item found before the first data_ block.

- Ignored string \<string\>.

- Ignored string (possible semi-colon mismatch).

- Ignoring uncommented string(s) before first data block.

- (Line) More than \<soft line length limit\> characters long.

- Repeated keyword \<keyword\>.

- Data value contains mismatched subscript (or superscript) markup.

- End of file marker \<marker\> is non-standard.

#### Missing identifier for data_ block

This warning indicates that the block name has been omitted from the
data block header. Each data block should have a unique identifier
appended to the `data_` keyword, e.g. `data_compound_1`.

#### Data item found before the first data_ block

This warning occurs if data names are encountered before the first
`data_` keyword. A data block, consisting of the keyword `data_`
plus some unique identifier e.g. `data_compound_1` should appear
before any data items.

#### Ignored string \<string\>

This warning occurs if text is encountered which is not interpreted as
a data value, comment or keyword. This may be due to a number of
common problems:

- A data value containing spaces is not quoted correctly. All
    single-line data values containing spaces must be delimited with
    single or double quotes, otherwise text after the first space is not
    interpreted as part of the data value, e.g. `rotating anode
    generator` should be `‘rotating anode generator’`.

- A data value delimited by single or double quotes has been split
    over two lines (this can sometimes happen if email or other software
    wraps text at less than 80 characters). Either the text should be
    moved to the same line, or treated as a multiple line value and
    delimited with semicolons, e.g.

```sh
‘a long
string’
```

should be:

```sh
‘a long string’
```

or:

```sh
;
a long
string
;
```

- The opening semicolon of a multiple-line data value has been
    omitted, such that text after the closing semicolon is interpreted
    as another data value, e.g.

```sh
chemical_name_systematic
A compound name
;
```

should be:

```sh
chemical_name_systematic
;
A compound name
;
```

The syntax highlighting in the editor should help to show this.

- Multiple data values are associated with a data item name, but the
    `loop_` keyword has been omitted. Without the `loop_` keyword,
    a data name may only be associated with one data value, e.g.

```sh
_publ_author_name ‘J. Soap’ ‘J. Bloggs’
```

should be:

```sh
loop_

 _publ_author_name ‘J. Soap’ ‘J. Bloggs’
```

- A comment has not been preceded by a hash (#) character, e.g.

```sh
_publ_contact_author_name ‘J. Soap’ Name of contact author
```

should be:

```sh
_publ_contact_author_name ‘J. Soap’ # Name of contact author
```

#### Ignored string (possible semi-colon mismatch)

This warning usually occurs if a semicolon closing a multiple-line data
value has been omitted, or if an extra semicolon is present at the start
of a line somewhere in the CIF. It is important to ensure that all
semicolons occur in pairs around data values as the first character on a
line. The syntax highlighting in the editor should help to show the
cause of these problems.

#### Ignoring uncommented string(s) before first data block

This warning indicates that there is text before the first data block
header (`data_` keyword) in the CIF which is not formatted correctly
as CIF. This may comprise email headers, textual comments or similar.
All such text should be removed from the CIF or be commented out by
placing hash (#) characters at the start of each line.

#### (Line) More than \<soft line length limit\> characters long

The line is longer than the current soft line length limit (default 80)
(see [Soft Line-Length Limit](encifer-07.md#soft-line-length-limit)). Line breaks should be inserted to ensure
all lines are shorter than the current soft line length limit. Where
necessary, single or double-quoted strings should be converted to
semicolon-delimited multiple-line strings to conform to the line length
limit.

#### Repeated keyword \<keyword\>

This warning most commonly occurs when the `loop_` keyword occurs on
consecutive lines. The duplicate `loop_` keyword should be deleted.

#### Data value contains mismatched subscript (or superscript) markup

Superscript text is indicated by a pair of ^ markers, for example
x<sup>2</sup> is written x^2^ and subscript text is indicated by a pair
of \~ markers, for example H<sub>2</sub>O is written H\~2\~O.

Superscript and subscript markers must be correctly paired and arranged
to return to normal text by the end of each data value, although they
may span multiple lines within a single semicolon delimited text string.
Superscripted and subscripted text, and the markers, are colored
differently to normal text; this may help in seeing where the problem
occurs.

\~ and ^ may also appear when defining accented characters, these uses
are ignored for this check.

#### End of file marker \<marker\> is non-standard

Some early CIF files were terminated with an uncommented sequence
beginning `_eof`. This sequence is not valid according to the version
1.1 specification. These sequences should be commented or deleted.

### CIF Dictionary Compliance Warning Messages

This section contains a list of all commonly occurring CIF dictionary
compliance warning messages:

- Created non-standard data item \<data name\>.

- Data value is not in dictionary enumeration list.

- Data value should be a number.

- Data value is not a correctly formatted number.

- Data value should be greater than a defined limit.

- Data value should be smaller than a defined limit.

- Data value should not have a standard uncertainty (ESD).

#### Created non-standard data item \<data name\>

This warning occurs if the data name cannot be found in a currently
enabled dictionary. This may indicate a number of possible problems:

- A data name has been spelt incorrectly.

- A custom data item has been created.

- A data name from a dictionary which is not currently enabled has
    been used (see [CIF Dictionary Options](encifer-07.md#cif-dictionary-options)).

- The CIF dictionary has been updated since this version of EnCIFer
    was released. The IUCr website can be checked for new versions to
    download (see [CIF Dictionary Options](encifer-07.md#cif-dictionary-options)).

#### Data value is not in dictionary enumeration list

Some data items have an enumeration list of recommended values in the
dictionary which are included in the data item dictionary help (see [Data Item Dictionary Help](encifer-06.md#data-item-dictionary-help)).

This warning indicates that the data value given does not correspond to
any of the recommended values.

#### Data value should be a number

Some data items should have a numeric value (integral or floating-point
without units, but with a standard uncertainty in some cases).

#### Data value is not a correctly formatted number

This warning indicates that the data value does not conform to the CIF
definition of a numeric data value, i.e. integral or floating-point
number with a standard uncertainty in some cases (see
[Summary of Warning Messages](encifer-07.md#summary-of-warning-messages)).
This may be explained by one of the following problems:

- There should be no spaces between the value and the standard
    uncertainty.

- The standard uncertainty should be surrounded by opening and closing
    parentheses, e.g. *12.934(3)*.

- A range of values, e.g. 212–215, is not permitted.

- Units or percentage signs are not permitted in the dictionary.

#### Data value should be greater than a defined limit

Some data items which should have a numeric value have a recommended
numeric range. If the data item is allowed to have a standard
uncertainty (ESD) the range is extended by *+/–3u* where *u* is the
standard uncertainty given in the data value.

These warnings indicate that the data value does not fall within the
recommended range, which are included in the data item dictionary help
(see [Data Item Dictionary Help](encifer-06.md#data-item-dictionary-help)).

#### Data value should not have a standard uncertainty (ESD)

Some data items should not have a standard uncertainty associated with
them. This warning indicates that a standard uncertainty (ESD) has been
given in a numeric data value for such an item, i.e. a number in
parentheses after the numeric value.

### CCDC Data Consistency Check Warning Messages

These messages relate to CCDC Checks (see [Setting the Mandatory Data Items File](encifer-07.md#setting-the-mandatory-data-items-file)).

If the relevant data items are not present or have values `?` or `.`
the related check will not be performed. If you wish this fact to be
reported, use the mandatory data items feature (see [Overview of Mandatory Data Items](encifer-07.md#overview-of-mandatory-data-items)).

This section contains the following messages:

- Error parsing_chemical_formula_sum ‘value’.

- Ignoring invalid symmetry operator text \<text\>.

- Duplicate atom label ‘\<label\>’.

#### Error parsing_chemical_formula_sum ‘value’

This indicates the check of formula weight failed as the sum formula
value could not be parsed.

#### Ignoring invalid symmetry operator text \<text\>

This indicates that whilst attempting to perform space group consistency
checks an unreadable symmetry operator was encountered. This can occur
if comments in a symmetry operator loop are erroneously wrapped when
sending a CIF via email.

Check that each value of data items
`_space_group_symop_operation_xyz` or `_symmetry_equiv_pos_as_xyz`
contains x, y and z values, separated by commas (,).

#### Duplicate atom label \<label\>

This is a failure of the duplicate atom label check as atom labels
should be unique. It means that there are duplicate values for the
`_atom_site_label` data item, which will usually appear in a loop.

## Summary of Remarks Messages

### Mandatory Data Item Remarks Messages

These messages relate to the checking for mandatory data items (see
[Mandatory Data Items](encifer-07.md#mandatory-data-items)):

- Data item \<data item\> not found in block \<block\>.

- Data item \<data item\> not set in block \<block\>.

- Related item \<related item\> not set in block \<block\>.

#### Data item \<data item\> not found in block \<block\>

This indicates that the data item, and any related data item, is not
found in the block.

#### Data item \<data item\> not set in block \<block\>

This indicates that the data item is found but has an unknown value in
the block, and no related item is found with a value other than unknown,
e.g.
mandatory data items file contains: `_refine_ls_R_factor_gt` and CIF
contains either: `_refine_ls_R_factor_gt ?`,
`_refine_ls_R_factor_gt ?` or `_refine_ls_R_factor_obs ?`

#### Related item \<related item\> not set in block \<block\>

This indicates that the data item is not found in the data block and the
related item has an unknown value, e.g.
mandatory data items file contains: `_refine_ls_R_factor_gt` and CIF
contains: `_refine_ls_R_factor_obs ?`

### CCDC Data Consistency Check Remarks Messages

These relate to CCDC Checks (see [Setting the Mandatory Data Items File](encifer-07.md#setting-the-mandatory-data-items-file)).

If the relevant data items are not present or have values `?` or `.`
the related check will not be performed. If you wish this fact to be
reported, use the mandatory data items feature (see [Overview of
Mandatory Data Items](encifer-07.md#overview-of-mandatory-data-items)).

Messages are given as remarks when items individually fulfill the
dictionary requirements but are inconsistent with respect to each other:

- Ignoring supplied space group \<name\>; using space group
    generated from symmetry operators \<name\>.

- Ignoring supplied international tables number \<number\>; using
    space group generated from symmetry operators \<name\>.

- Formula weight \<weight\> different to weight calculated from
    chemical formula \<weight\>.

#### Ignoring supplied space group \<name\>; using space group generated from symmetry operators \<name\>

This is a failure of the space group consistency check, which means that
the text in `_symmetry_space_group_name_H-M` does not match the name
of the space group generated from the operators in
`_space_group_symop_operation_xyz` or
`_symmetry_equiv_pos_as_xyz`.

When loading the structure in the **Visualiser**, the space group
specified by the operators will always be preferred.

#### Ignoring supplied international tables number \<number\>; using space group generated from symmetry operators \<name\>

This is a failure of the space group consistency check, which means that
the value in `_space_group_IT_number` or
`_symmetry_int_tables_number` does not match the number of the space
group generated from the operators in
`_space_group_symop_operation_xyz` or
`_symmetry_equiv_pos_as_xyz`.

When loading the structure in the **Visualiser**, the space group
specified by the operators will always be preferred.

#### Formula weight \<weight\> different to weight calculated from chemical formula \<weight\>

This is a failure of the formula weight consistency check, which means
that the value of the `_chemical_formula_weight` data item does not
match a weight calculated from the value of the
`_chemical_formula_sum` data item.

The values may differ by up to 1.1 Daltons without this message being
generated.
