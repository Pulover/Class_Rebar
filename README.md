# Class Rebar

## Class for AutoHotkey Rebar custom controls

AHK version: 1.1.23.01

This class provides intuitive methods to work with Rebar controls created via **Gui, Add, Custom, ClassReBarWindow32**.

## Rebar Methods
* DeleteBand(Band)
* GetBand(Band [, ID, Text, Size, Image, Background, Style, Child])
* GetBandCount()
* GetBarHeight()
* GetLayout()
* GetRowCount()
* GetRowHeight(Band)
* IDToIndex(ID)
* InsertBand(hChild [, Position, Options, ID, Text, Size, Image, Background, MinHeight, MinWidth, IdealSize])
* MaximizeBand(Band [, IdealWidth])
* MinimizeBand(Band)
* ModifyBand(Band, Property, Value [, SetStyle])
* MoveBand(Band, Target)
* OnNotify(Param [, MenuXPos, MenuYPos, ID)
* SetBandStyle(Band, Value)
* SetBandWidth(Band, Width)
* SetImageList(ImageList)
* SetMaxRows([Rows])
* SetLayout(Layout)
* ShowBand(Band [, Show])
* ToggleStyle(Style)

## Useful Rebar Styles
Styles can be applied to Gui command options, e.g.: Gui, Add, Custom, ClassReBarWindow32 0x0800 0x0100

* RBS_BANDBORDERS   := 0x0400 - Add a separator border between bands in different rows.
* RBS_DBLCLKTOGGLE  := 0x8000 - Toggle maximize/minimize with double-click instead of single.
* RBS_FIXEDORDER    := 0x0800 - Always displays bands in the same order.
* RBS_VARHEIGHT     := 0x0200 - Allow bands to have different heights.
* CCS_NODIVIDER     := 0x0040 - Removes the separator line above the rebar.
* CCS_NOPARENTALIGN := 0x0008 - Allows positioning and moving rebars.
* CCS_NORESIZE      := 0x0004 - Allows resizing rebars.
* CCS_VERT          := 0x0080 - Creates a vertical rebar.

## Delete()
Deletes a band from a rebar control.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of the band to be deleted.

## GetBand()
Retrieves information from a rebar band.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of the band.
* *ID* - OutputVar to store the band's ID.
* *Text* - OutputVar to store the band's text.
* *Size* - OutputVar to store the band's size.
* *Image* - OutputVar to store the band's image index.
* *Background* - OutputVar to store a handle to the band's background bitmap.
* *Style* - OutputVar to store the band's style numeric value.
* *Child* - OutputVar to store a handle to the band's child control.

## GetBandCount()
Retrieves the count of bands currently in the rebar control.

### Return
The number of bands in the rebar control.

## GetBarHeight()
Retrieves the height of the rebar control.

### Return
The height of the rebar control in pixels.

## GetLayout()
Retrieves the current layout of bands in the rebar control.

### Return
A string containing information about the current bands. String format is: ID1,Size1,Style1|ID2,Size2,Style2|...

## GetRowCount()
Retrieves the number of rows of bands in a rebar control.

### Return
The number of rows in the rebar control.

## GetRowHeight()
Retrieves the number of rows of bands in a rebar control.

### Return
The height of the row from the corresponding band in pixels.

### Parameters
* *Band* - 1-based index of a band to retrieve the height from.

## IDToIndex()
Converts a band identifier to a band index in a rebar control.

### Return
The 1-based band index if successful, or 0 otherwise.

### Parameters
* *ID* - The application-defined identifier of the band in question.

## InsertBand()
Inserts a new band in a rebar control.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *hChild* - Handle to the control contained in the band, if any.
* *Position* - 1-based index of the location where the band will be inserted. If you set this parameter to 0, the control will add the new band at the last location.
* *Options:        Enter zero or more words, separated by space or tab, from the following list to set the band's initial styles: Break, FixedBmp, FixedSize, Hidden, HideTitle, NoGripper, NoVert, TopAlign, VariableHeight. The following styles are applied by default* - ChildEdge, GripperAlways (can be disabled with NoGripper), UseChevron (only valid if IdealSize is set).
* *ID* - Integer value that the control uses to identify this band. This parameter is required to retrieve and set layouts.
* *Text* - The display text for the band.
* *Size* - Length of the band, in pixels.
* *Image* - 1-based index of any image that should be displayed in the band. SetImageList method must be called prior to this.
* *Background* - Path of a bitmap file that is used as the background for this band.
* *MinHeight* - Minimum height of the control, in pixels.
* *MinWidth* - Minimum width of the control, in pixels.
* *IdealSize* - Ideal width of the band, in pixels. If the band is maximized to the ideal width (see MaximizeBand method), the rebar control will attempt to make the band this width.

## MaximizeBand()
Resizes a band to either its ideal or largest size.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of a band to be maximized.
* *IdealWidth* - If TRUE the ideal width of the band will be used to maximize

## MinimizeBand()
Resizes a band to its smallest size.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of a band to be minimized.

## ModifyBand()
Sets band parameters such as Text and Size.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of a band to be modified.
* *Property:       Enter one word from the following list to select the Property to be set* - Style, ID, Text, Size, Image, Background, MinWidth, MinHeight, IdealSize, Child (handle of control).
* *Value* - The value to be set in the selected Property. If Property is Style you can enter named values as in the InsertBand options, or an integer value.
* *SetStyle* - Only valid if Property is Style. Determines whether to add or remove the styles.

## MoveBand()
Moves a band from one index to another.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of a band to be moved.
* *Target* - 1-based index of a the new band position.

## OnNotify()
Handles rebar notifications. This method should be called from the rebar's G-Label. If A_GuiEvent is "N", pass it A_EventInfo as the Param. You can also call it from a function monitoring the WM_NOTIFY message, pass it lParam as the Param. Currently this method is used to retrieve the position for a menu when the Chevron button is pushed and prevent a number of rows higher then the one set by SetMaxRows method.

### Return
If the ChevronPushed notification is passed returns the index of the band it is from.

### Parameters
* *Param* - The lParam from WM_NOTIFY message.
* *MenuXPos* - OutputVar to store the horizontal position for a menu.
* *MenuYPos* - OutputVar to store the vertical position for a menu.
* *ID* - OutputVar to store the band's ID.

## SetBandStyle()
Sets the style of a band.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of the band.
* *Value* - Named values as in the InsertBand options, or an integer value.

## SetBandWidth()
Sets the width for a docked band.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of the band.
* *Width* - New width in pixels.

## SetImageList()
Sets an ImageList to the rebar control.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *ImageList* - ImageList ID.

## SetLayout()
Sets a layout of bands in the rebar control.

### Return
TRUE if a valid layout was passed, or FALSE otherwise.

### Parameters
* *Layout:         A string containing information about the current bands. String format is* - ID1,Size1,Style1|ID2,Size2,Style2|...

## SetMaxRows()
Sets the maximum number of rows allowed in a rebar control. This method requires the OnNotify method to be implemented.

### Return
The number of rows previously allowed.

### Parameters
* *Rows* - Number of maximum rows allowed. Set it to 0 to disable limit.

## ShowBand()
Shows or hides a given band in a rebar control.

### Return
TRUE if successful, FALSE if there was a problem.

### Parameters
* *Band* - 1-based index of the band.
* *Show* - Set to TRUE to show the band or FALSE to hide it.

## ToggleStyle()
Toggles rebar's style.

### Return
TRUE if a valid style is passed, or FALSE otherwise.

### Parameters
* *Style:          Enter one or more words, separated by space or tab, from the following list to toggle toolbar's styles* - AutoSize, BandBorders, DblClkToggle, FixedOrder, RegisterDropdown, VarHeight, VerticalGripper. You may also enter an integer value to define the style.

