# Data Wizards

## Overview of Data Wizards

Two wizards are provided in EnCIFer to assist with entering both
publication details and additional chemical and crystallographic data
into a CIF data block, with syntactically correct formatting. These
wizards prompt for data values which are frequently required for
publication, but which are not always generated automatically by crystal
structure solution software.

The publication data wizard and crystal data wizard both operate on the
current CIF block, as determined by the current editor cursor position.
They are activated by either:

- Clicking the **Publication Wizard** or **Crystal Wizard** icons
    respectively on the toolbar.

- Selecting **Tools** on the top-level menu and clicking **Publication
    Wizard** or **Crystal Wizard**.

The **Text Editor** may not be used whilst a wizard is in operation.

The publication data wizard may be used to create a new data block by
placing the cursor before the first block, or be applied to any existing
block.

The crystal data wizard may only be used on a data block which already
contains crystal data (`_chemical`, `_cell` or `_atom_site`
data items).

## Structure of the Wizards

Each wizard comprises a number of pages:

- To move to the next wizard page, click the **Next** button.

- To return to the previous page in the wizard, click the **Back**
    button.

- To abort the wizard from any page, discarding any changes already
    input, click the **Cancel** button.

The first page provides introductory information. The second page shows
any CIF error and warning messages and the other pages of each wizard
allow input of a number of CIF data items:

- Where the data item is already set in the CIF block, the data value
    is shown in the wizard, even where it is set to **`.`** or `?`.

- If data items are left unset (empty) in the wizard, the
    corresponding data name will be omitted from the data block if the
    changes made in the wizard are applied to the editor.

- Data item dictionary help is available for some data items by
    clicking on the appropriate icon on the wizard pages.

<img src="encifer-media/image12.png" style="width:0.48472in;height:0.45486in" />

The final page of each wizard allows data entered or modified in the
wizard to be applied to the CIF block in the **Text Editor** by clicking
**Finish**. Previous pages may be reviewed by clicking **Back**, and the
edits may be discarded by clicking **Cancel**.

Changes applied to the **Text Editor** may be undone, by hitting
**Edit** in the top-level menu and selecting **Undo,** or by using the
**Ctrl+Z** shortcut. This will be one step for a new publication block
or two steps for an existing block (the first undo step removes the
modified data block text, and the second undo restores the original data
block text).

## Using the Wizard when there are CIF Errors or Warnings

Before a wizard can be used to enter data the CIF must be free from
errors, to prevent serious data loss from occurring if changes made in
the wizard are applied to the editor.

When starting a wizard, the CIF will be re-parsed if necessary, and any
errors or warnings are shown on the second page of the wizard. If there
are fatal errors, wizard operation cannot continue, and the errors must
be corrected first. If there are warnings, the wizard can be used but
data loss may occur for some warnings, in particular *Ignored string*
warnings.

## Publication Wizard Outline

### Page 1. Introduction

Introduction to the wizard.

### Page 2. Errors and Warnings

Summary of current error, warning and remarks messages.

### Page 3. Contact Information

This page allows entry of contact author details. If
`_publ_contact_author` is present in the CIF data block, the wizard
will interpret the first line as the contact name and the remainder as
the contact address, unless the `_publ_contact_author_name` is set in
which case it is all interpreted as the contact address.

It is also possible to enter these details in the preferences, such that
they are automatically entered into the wizard if the CIF block has no
contact author data items set.

To set the contact author preference:

1. Hit **Edit** on the main menu > **Preferences** > **Wizard**.

1. The contact author details may then be entered in the edit boxes.

1. Click the **OK** button to apply the changes, or **Cancel** to
    discard changes.

### Page 4. Publication Information

This page asks whether the structure is being submitted to a journal for
publication, is being submitted to a database as a CSD Communication, or
has already been published (the year, page and/or volume are known).
Clicking on the appropriate radio button determines which pages are
subsequently displayed.

### Page 5. Requested Journal

A list of possible abbreviated journal titles is given in a scrolling
list view. These are journals from which crystal structure data has
previously been abstracted by the CCDC.

Double-clicking on a journal title enters it into the **Text** edit box.
Alternatively, a journal title may be typed into the **Text** edit box.
The scrolling list is updated to show only those journals which match
what has been typed, ignoring case and punctuation. The journal
manuscript code as assigned by the journal publisher may be entered in
the **Text** edit box if this is already known.

### Page 6. Journal Details

A scrolling list of journals is given as for the Requested journal name
in page 5 of the wizard. Additionally, page numbers, volume and year may
be entered.

### Page 7. Author Details

Only one author in the CIF loop is displayed at any time. Initially, the
first author in the loop is displayed. Family and first author name and
the address corresponding to the currently displayed author are shown in
separate edit windows. The values may be edited by typing in the edit
windows.

If there are no author details in the CIF, the contact author set on
Page 3 of the wizard is inserted automatically as the first author.

Clicking the **Previous** and **Next** buttons allows the previous and
next author in the loop to be displayed in turn.

To add authors:

1. Click the **Add** button.

1. Type in the author’s details in the **Edit** window.

1. The new author is added to the end of the loop. If the previous
    author in the list has an address set, this address is copied for
    the new author.

The current author may be deleted by clicking the **Delete** button.

### Page 8. Finish

Click the **Finish** button to apply the changes to the CIF in the
editor, or **Back** to review changes.

## Crystal Data Wizard Outline

### Page 1. Introduction

Introduction to the wizard.

### Page 2. Errors and Warnings

Summary of current error, warning and remark messages.

### Page 3. Physical and Chemical Information

Contains:

- Systematic name.

- Common name.

- Moiety formula.

- Sum formula.

- Compound source.

- Physical Properties. A list of common properties is provided in a
    drop-down list. These can be appended to the text by selecting an
    item then pressing the **Add** button. Free text can also be entered
    in the box to the right.

### Page 4. Physical and Chemical Information

Contains:

- Crystallization solvent.

- Melting point.

- Crystal habit.

- Crystal colour.

- Diffraction temperature.

- Diffraction pressure.

### Page 5. Symmetry Information

The crystal system may be set from a pull-down list containing the
allowed CIF values. The wizard tries to ensure consistency between the
space group number in *International Tables for Crystallography*
(IUCr/Kluwer, 1993) and the Hermann-Mauguin (H-M) symbol:

- The wizard shows an editable pull-down list of common space group
    settings corresponding to the *International Tables* number.

- Other H-M symbols may be entered by clicking and typing in the **H-M
    symbol** edit box, pressing **Return** to complete the edit.

- The *International Tables* space group number will be updated if the
    H-M symbol is recognized.

- Setting the *International Tables* number updates the list of
    possible space groups.

EnCIFer tries to ensure consistency between the Hermann-Mauguin symbols
and the symmetry equivalent positions:

- A warning is given if they do not agree, suggesting an H-M symbol
    derived from the equivalent positions where possible.

- If the H-M symbol is not given in the CIF, EnCIFer tries to derive
    it from the symmetry equivalent positions.

- Absolute Configuration. Allowed values can be selected from a
    drop-down list. Press the **Item help** icon for a full description
    of the values.

### Page 6. Diffraction Information

Details of:

- Radiation probe. Selection of the probe is made from the drop-down
    list.

- Radiation type.

- Radiation wavelength.

- Radiation source class.

- Radiation source type.

### Page 7. Finish

Click the **Finish** button to apply the changes to the CIF in the
editor, or **Back** to review changes.
