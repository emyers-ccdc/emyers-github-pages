# Appendices

## Keyboard Shortcuts

| Action                    | PC & UNIX   | macOS              |
|---------------------------|-------------|--------------------|
| Select All Text           | **Ctrl+A**  | **Command key+A**  |
| Show/Hide CIF Browser     | **Ctrl+B**  | **Command key+B**  |
| Copy Text                 | **Ctrl+C**  | **Command key+C**  |
| Delete next character     | **Ctrl+D**  | **Command key+D**  |
| Go to end of line         | **Ctrl+E**  | **Command key+E**  |
| Find Text                 | **Ctrl+F**  | **Command key+F**  |
| Find Next                 | **F3**      | **F3**             |
| Find Previous             | **Ctrl+F3** | **Command key+F3** |
| Go to Line                | **Ctrl+G**  | **Command key+G**  |
| Delete previous character | **Ctrl+H**  | **Command key+H**  |
| Data Item Dictionary Help | **Ctrl+I**  | **Command key+I**  |
| Re-Check CIF              | **Ctrl+K**  | **Command key+K**  |
| Edit Loop                 | **Ctrl+L**  | **Command key+L**  |
| New File                  | **Ctrl+N**  | **Command key+N**  |
| Open File                 | **Ctrl+O**  | **Command key+O**  |
| Print                     | **Ctrl+P**  | **Command key+P**  |
| Quit/Exit                 | **Ctrl+Q**  | **Command key+Q**  |
| Replace Text              | **Ctrl+R**  | **Command key+R**  |
| Save                      | **Ctrl+S**  | **Command key+S**  |
| Paste Text                | **Ctrl+V**  | **Command key+V**  |
| Close File                | **Ctrl+W**  | **Command key+W**  |
| Cut Text                  | **Ctrl+X**  | **Command key+X**  |
| Redo                      | **Ctrl+Y**  | **Command key+Y**  |
| Undo                      | **Ctrl+Z**  | **Command key+Z**  |

## Atomic Displacement Parameters (ADPs)

Atomic Displacement Parameters (also known as *atomic vibration
parameters* and *thermal parameters*) are used to generate displacement
ellipsoids. Displacement ellipsoids represent atomic motion and can be
either isotropic or anisotropic. The shape and size of ADPs can be used
to highlight potential errors with the data; the smaller and more
spherical the ellipses for anisotropic atoms, the better the data (see
*Troublesome Crystal Structures: Prevention, Detection and Resolution*,
R. L. Harlow, *J. Res. Natl. Inst. Stand. Technol.*, **101(3)**, 327,
1996).

For ellipsoids to be displayed in Encifer, it is necessary for the
relevant U<sub>equiv</sub> and U<sub>ij</sub> values to be present in
the CIF file. U<sub>equiv</sub> and U<sub>ij</sub> values are not stored
in the CSD, thus it is not possible to view ellipsoids for entries
output from the CSD. CIFs obtained through the CCDC’s online request
form
([www.ccdc.cam.ac.uk/products/csd/request](http://www.ccdc.cam.ac.uk/products/csd/request/))
may contain these data where provided by the publishing author.

Ellipsoids can be displayed in Encifer by clicking on the **Visualiser**
background, selecting the **Styles** submenu and then selecting
**Ellipsoid**. Settings for the Ellipsoids display style may be
controlled using the **Ellipsoid setting** window, available from the
*same* menu.

Relevant Program Options:

- Displaying ellipsoids (see [Setting a Global Display Style](encifer-11.md#setting-a-global-display-style)).

- Setting ellipsoid display options (see [Setting Ellipsoid Display Options](encifer-11.md#setting-ellipsoid-display-options)).
