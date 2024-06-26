The origin of the patch and its  purpose is forgotten.
Might need to save this file as `dmenu.1.patched`
```
.TH DMENU 1 dmenu\-VERSION
.SH NAME
dmenu \- dynamic menu
.SH SYNOPSIS
.B dmenu
.RB [ \-b ]
.RB [ \-f ]
.RB [ \-i ]
.RB [ \-v ]
\" >>>>>>>>>>>>>>>>>>>> case-insensitive
\" ==================== case-insensitive
\" <<<<<<<<<<<<<<<<<<<< case-insensitive
\" >>>>>>>>>>>>>>>>>>>> center
\" ==================== center
\" <<<<<<<<<<<<<<<<<<<< center
\" >>>>>>>>>>>>>>>>>>>> fuzzymatch
\" ==================== fuzzymatch
\" <<<<<<<<<<<<<<<<<<<< fuzzymatch
\" >>>>>>>>>>>>>>>>>>>> xyw
\" ==================== xyw
\" <<<<<<<<<<<<<<<<<<<< xyw
\" >>>>>>>>>>>>>>>>>>>> password
\" ==================== password
\" <<<<<<<<<<<<<<<<<<<< password
\" >>>>>>>>>>>>>>>>>>>> incremental
\" ==================== incremental
\" <<<<<<<<<<<<<<<<<<<< incremental
\" >>>>>>>>>>>>>>>>>>>> managed
\" ==================== managed
\" <<<<<<<<<<<<<<<<<<<< managed
\" >>>>>>>>>>>>>>>>>>>> reject-no-match
\" ==================== reject-no-match
\" <<<<<<<<<<<<<<<<<<<< reject-no-match
\" >>>>>>>>>>>>>>>>>>>> prefix-completition
\" ==================== prefix-completition
\" <<<<<<<<<<<<<<<<<<<< prefix-completition
\" >>>>>>>>>>>>>>>>>>>> instant
\" ==================== instant
\" <<<<<<<<<<<<<<<<<<<< instant
\" >>>>>>>>>>>>>>>>>>>> print-input-text
\" ==================== print-input-text
\" <<<<<<<<<<<<<<<<<<<< print-input-text
.RB [ \-m
.IR monitor ]
.RB [ \-w
.IR windowid ]
.RB [ \-l
.IR lines ]
.RB [ \-fn
.IR font ]
.RB [ \-p
.IR prompt ]
\" >>>>>>>>>>>>>>>>>>>> border
\" ==================== border
\" <<<<<<<<<<<<<<<<<<<< border
\" >>>>>>>>>>>>>>>>>>>> dynamic-options
\" ==================== dynamic-options
\" <<<<<<<<<<<<<<<<<<<< dynamic-options
\" >>>>>>>>>>>>>>>>>>>> grid
\" ==================== grid
\" <<<<<<<<<<<<<<<<<<<< grid
\" >>>>>>>>>>>>>>>>>>>> preselect
\" ==================== preselect
\" <<<<<<<<<<<<<<<<<<<< preselect
\" >>>>>>>>>>>>>>>>>>>> initial-text
\" ==================== initial-text
\" <<<<<<<<<<<<<<<<<<<< initial-text
\" >>>>>>>>>>>>>>>>>>>> json
\" ==================== json
\" <<<<<<<<<<<<<<<<<<<< json
\" >>>>>>>>>>>>>>>>>>>> navhistory
\" ==================== navhistory
\" <<<<<<<<<<<<<<<<<<<< navhistory
\" >>>>>>>>>>>>>>>>>>>> line-height
\" ==================== line-height
\" <<<<<<<<<<<<<<<<<<<< line-height
\" >>>>>>>>>>>>>>>>>>>> high-priority
\" ==================== high-priority
\" <<<<<<<<<<<<<<<<<<<< high-priority
.RB [ \-nb
.IR color ]
.RB [ \-nf
.IR color ]
.RB [ \-sb
.IR color ]
.RB [ \-sf
.IR color ]
\" >>>>>>>>>>>>>>>>>>>> fuzzyhighlight
\" ==================== fuzzyhighlight
\" <<<<<<<<<<<<<<<<<<<< fuzzyhighlight
.P
.BR dmenu_run " ..."
.SH DESCRIPTION
.B dmenu
is a dynamic menu for X, which reads a list of newline\-separated items from
stdin.  When the user selects an item and presses Return, their choice is printed
to stdout and dmenu terminates.  Entering text will narrow the items to those
matching the tokens in the input.
.P
.B dmenu_run
is a script used by
.IR dwm (1)
which lists programs in the user's $PATH and runs the result in their $SHELL.
.SH OPTIONS
.TP
.B \-b
dmenu appears at the bottom of the screen.
.TP
.B \-f
dmenu grabs the keyboard before reading stdin if not reading from a tty. This
is faster, but will lock up X until stdin reaches end\-of\-file.
.TP
.B \-i
dmenu matches menu items case insensitively.
.TP
.B \-v
prints version information to stdout, then exits.
.TP
\" >>>>>>>>>>>>>>>>>>>> case-insensitive
\" ==================== case-insensitive
\" <<<<<<<<<<<<<<<<<<<< case-insensitive
\" >>>>>>>>>>>>>>>>>>>> center
\" ==================== center
\" <<<<<<<<<<<<<<<<<<<< center
\" >>>>>>>>>>>>>>>>>>>> fuzzymatch
\" ==================== fuzzymatch
\" <<<<<<<<<<<<<<<<<<<< fuzzymatch
\" >>>>>>>>>>>>>>>>>>>> xyw
\" ==================== xyw
\" <<<<<<<<<<<<<<<<<<<< xyw
\" >>>>>>>>>>>>>>>>>>>> password
\" ==================== password
\" <<<<<<<<<<<<<<<<<<<< password
\" >>>>>>>>>>>>>>>>>>>> incremental
\" ==================== incremental
\" <<<<<<<<<<<<<<<<<<<< incremental
\" >>>>>>>>>>>>>>>>>>>> managed
\" ==================== managed
\" <<<<<<<<<<<<<<<<<<<< managed
\" >>>>>>>>>>>>>>>>>>>> reject-no-match
\" ==================== reject-no-match
\" <<<<<<<<<<<<<<<<<<<< reject-no-match
\" >>>>>>>>>>>>>>>>>>>> prefix-completition
\" ==================== prefix-completition
\" <<<<<<<<<<<<<<<<<<<< prefix-completition
\" >>>>>>>>>>>>>>>>>>>> instant
\" ==================== instant
\" <<<<<<<<<<<<<<<<<<<< instant
\" >>>>>>>>>>>>>>>>>>>> print-input-text
\" ==================== print-input-text
\" <<<<<<<<<<<<<<<<<<<< print-input-text
.BI \-m " monitor"
dmenu is displayed on the monitor number supplied. Monitor numbers are starting
from 0.
.TP
.BI \-w " windowid"
embed into windowid.
.BI \-l " lines"
dmenu lists items vertically, with the given number of lines.
.TP
.BI \-fn " font"
defines the font or font set used.
.TP
.BI \-p " prompt"
defines the prompt to be displayed to the left of the input field.
.TP
\" >>>>>>>>>>>>>>>>>>>> border
\" ==================== border
\" <<<<<<<<<<<<<<<<<<<< border
\" >>>>>>>>>>>>>>>>>>>> dynamic-options
\" ==================== dynamic-options
\" <<<<<<<<<<<<<<<<<<<< dynamic-options
\" >>>>>>>>>>>>>>>>>>>> grid
\" ==================== grid
\" <<<<<<<<<<<<<<<<<<<< grid
\" >>>>>>>>>>>>>>>>>>>> preselect
\" ==================== preselect
\" <<<<<<<<<<<<<<<<<<<< preselect
\" >>>>>>>>>>>>>>>>>>>> initial-text
\" ==================== initial-text
\" <<<<<<<<<<<<<<<<<<<< initial-text
\" >>>>>>>>>>>>>>>>>>>> json
\" ==================== json
\" <<<<<<<<<<<<<<<<<<<< json
\" >>>>>>>>>>>>>>>>>>>> navhistory
\" ==================== navhistory
\" <<<<<<<<<<<<<<<<<<<< navhistory
\" >>>>>>>>>>>>>>>>>>>> line-height
\" ==================== line-height
\" <<<<<<<<<<<<<<<<<<<< line-height
\" >>>>>>>>>>>>>>>>>>>> high-priority
\" ==================== high-priority
\" <<<<<<<<<<<<<<<<<<<< high-priority
.BI \-nb " color"
defines the normal background color.
.IR #RGB ,
.IR #RRGGBB ,
and X color names are supported.
.TP
.BI \-nf " color"
defines the normal foreground color.
.TP
.BI \-sb " color"
defines the selected background color.
.TP
.BI \-sf " color"
defines the selected foreground color.
.TP
\" >>>>>>>>>>>>>>>>>>>> fuzzyhighlight
\" ==================== fuzzyhighlight
\" <<<<<<<<<<<<<<<<<<<< fuzzyhighlight
.SH USAGE
dmenu is completely controlled by the keyboard.  Items are selected using the
arrow keys, page up, page down, home, and end.
.TP
.B Tab
Copy the selected item to the input field.
.TP
.B Return
Confirm selection.  Prints the selected item to stdout and exits, returning
\" >>>>>>>>>>>>>>>>>>>> print-input-text
\" ==================== print-input-text
success.
\" <<<<<<<<<<<<<<<<<<<< print-input-text
.TP
.B Ctrl-Return
Confirm selection.  Prints the selected item to stdout and continues.
.TP
.B Shift\-Return
Confirm input.  Prints the input text to stdout and exits, returning success.
\" >>>>>>>>>>>>>>>>>>>> print-input-text
\" ==================== print-input-text
\" <<<<<<<<<<<<<<<<<<<< print-input-text
.TP
.B Escape
Exit without selecting an item, returning failure.
.TP
.B Ctrl-Left
Move cursor to the start of the current word
.TP
.B Ctrl-Right
Move cursor to the end of the current word
.TP
.B C\-a
Home
.TP
.B C\-b
Left
.TP
.B C\-c
Escape
.TP
.B C\-d
Delete
.TP
.B C\-e
End
.TP
.B C\-f
Right
.TP
.B C\-g
Escape
.TP
.B C\-h
Backspace
.TP
.B C\-i
Tab
.TP
.B C\-j
Return
.TP
.B C\-J
Shift-Return
.TP
.B C\-k
Delete line right
.TP
.B C\-m
Return
.TP
.B C\-M
Shift-Return
.TP
.B C\-n
Down
.TP
.B C\-p
Up
.TP
.B C\-u
Delete line left
.TP
.B C\-w
Delete word left
.TP
.B C\-y
Paste from primary X selection
.TP
.B C\-Y
Paste from X clipboard
.TP
.B M\-b
Move cursor to the start of the current word
.TP
.B M\-f
Move cursor to the end of the current word
.TP
.B M\-g
Home
.TP
.B M\-G
End
.TP
.B M\-h
Up
.TP
.B M\-j
Page down
.TP
.B M\-k
Page up
.TP
.B M\-l
Down
.SH SEE ALSO
.IR dwm (1),
.IR stest (1)
```