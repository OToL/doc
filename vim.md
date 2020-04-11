# MOTIONS

h j k l : left down up right
w : move to beginning of next word
W : move to the beginning of the next WORD
e : move the next word's end
E : move the next WORD's end
b : move the beginning of the previous word
B : move the beginning of the previous WORD
ge : move the end of the previous word
gE : move the end of the previous WORD

f{character} : move to a character forward in current line
F{character} : move to a character backward in current line
t{character} : move until a character forward in current line
T{character} : move until a character backward in current line
; : repeat the last line search (f/F/t/T)
, : repeat the inverse of the last line search (f/F/t/T)

/{pattern} : search pattern forward in document
?{pattern} : search pattern backward
* : search current word forward
# : search current word backward
n : repeat the last search
N : repeat the inverse of the last search

0 : move to the begining of the line
$ : move to the end of the line
^ : move the the first non blank character of the line
g_ : move the last non-blank character of the line

{ : go one paragraph up (i.e. first blank line up)
} : go one paragraph down (i.e. next blank line down)

gg : move to the begining of the document
G : move to the end of the document
{number}gg : go to a specific line

Ctrl+u : half page up
Ctrl+d : half page down
H : go to the beginning of current page
L : go to the end of current page
M : go to the middles of current page
zz : recenter current line to the middle of the page