# Basic Commands

## Search & Replace

**Search:**

`C-s` Begin incremental search (**isearch-forward**) (**isearch-repeat-forward**)

`C-r` Begin reverse incremental search (**isearch-backward**) (**isearch-repeat-backward**)

`C-s` and `C-r` will repeat the previous search forward/backward and preserve the searching mode.

**Symbol Search:**

`M-s _` Begin or change to an incremental forward symbol search (**isearch-forward-symbol**)

`M-s .` Start a symbol incremental search forward with the symbol found near point added to the search string initially (**isearch-forward-symbol-at-point**)

`C-s C-w` Start an incremental search, then add the word or symbol under point to your search

**Unconditional Replace:**

`M-x replace-string RET string RET newstring RET`

`M-x replace-regexp RET regexp RET newstring RET`

**Query Replace:**

`M-% string RET newstring RET` Replace some occurrences of *string* with  *newstring*. (**query-replace**)

`C-M-% regexp RET newstring RET` Replace some matches of *regexp* with *newstring*. (**query-replace-regexp**)

`SPC` `y` to replace the occurrence with *newstring*

`DEL` `n` to skip to the next occurrence without replacing this one.

`RET` `q` to exit without doing any more replacements.

`.` to replace this occurrence and then exit without searching for more occurrences.

`!` to replace all remaining occurrences without asking again.

`^` to go back to the position of the previous occurrence.

`u` to undo the last replacement and go back to where that replacement was made.

`U` to undo **all** the replacements and go back to where the first replacement was made.

`C-r` to enter a **recursive editing** level. `C-M-c` to exit recursive editing level and proceed to the next occurrence

`C-w` to delete the occurrence and then enter a recursive editing level as in `C-r`.

`e` to edit the replacement string in the minibuffer, exit by typing `RET`. The minibuffer contents replace the current occurrence and become the new replacement string for any further occurrences.

`E`  is like `e`, but the next replacement will be done with exact  case.



Case Sensitivity in Text Search Commands
`M-x toggle-case-fold-search`



## Change Location

The location of the cursor in the text is also called "point". To paraphrase, the cursor shows on the screen where point is located in the text.

- `C-f` `C-b` Move forward/backward one **character** (**forward-char**/**backward-char**)
- `C-n` `C-p` Move down/up one **screen line** (**new-line**/**previous-line**)
- `C-a` `C-e` Move to the beginning/end of the **line** (**move-beginning-of-line**/**move-end-of-line**)
- `M-a` `M-e` Move to the beginning/end of a **sentence**, which means repetition works.
- `M-f` `M-b` Move forward/backward one **word** (**forward-word**/**backward-word**)
- `M-<` `M->` Move to the beginning/end of the **buffer** (**beginning-of-buffer**/**end-of-buffer**)
- `M-{` `M-}` Move back/forward to previous/next **paragraph** beginning/end (**backward-paragraph**/**forward-paragraph**).



### Scroll

`M-x scroll-up-line`

`M-x scroll-down-line`

​	To scroll the current window by one line at a time



`(setq scroll-step 1)` : **Scroll one line** when reaching the bottom of the screen with `C-v`



- `M-n` `M-p` Scroll down/up one screen line (Customized elisp function and key binding)

Add the following lines to `.emacs` if the shortcuts are not active.

```
;; Useful shortcut to scroll back and forth
(defun scroll-up-keep-cursor ()
  "Scroll up without moving cursor."
  (interactive)
  (scroll-up 1))

(defun scroll-down-keep-cursor ()
  "Scroll down without moving cursor."
  (interactive)
  (scroll-down 1))

(global-set-key (kbd "M-n") 'scroll-up-keep-cursor)
(global-set-key (kbd "M-p") 'scroll-down-keep-cursor)
```



- `C-v` `M-v` Scroll the display one screen forward/backward (**scroll-up-command**/**scroll-down-command**) 

  (If your meta key is not working, in order to type a key that contains meta, you can instead type `ESC`, then the remaining keys. Here `M-v` equals `ESC` `v`.)

- `M-<` `M->` Move to the top/end of the buffer (**beginning-of-buffer**/**end-of-buffer**)


**Synchronise scrolling**:
- `M-x scroll-all-mode`

Any scrolling command (e.g., `C-v`, `M-v`) applied in one window will be mirroed in all others


**Window**

- `M-r` Move the point to the three lines, in cyclic order (**move-to-window-line-top-bottom**)
  - the center-most text line of the screen, 
  - then the top-most line, 
  - then the bottom-most line.
- `C-l` Clear screen and redisplay all the text, moving the text around the cursor to 
  - the center of the screen, 
  - then top of the screen, 
  - and then the bottom.



**Specified position**:

`M-g c` Read a number `n` and move point to buffer position `n`.

`M-g g` Read a number `n` and move point to the beginning of line number `n` (**goto-line**).



**In Sentence**

`M-m` Move (forward or back) to the first non-whitespace character on the current line (**back-to-indentation**)



### Jump

**In Parenthesis Structure**

`C-M-n` Move forward over a parenthetical group (**forward-list**).

`C-M-p` Move backward over a parenthetical group (**backward-list**).

`C-M-u` Move up in parenthesis structure (**backward-up-list**).

`C-M-d` Move down in parenthesis structure (**down-list**).



**Jump back**

`C-x C-@` Add current point to mark ring

`C-x C-SPC`  Pop mark ring (**pop-global-mark**)



`C-SPC C-SPC` Set the mark, pushing it onto the **mark ring**. without activating it

`C-u C-SPC` Move point to where the mark was, and restore the mark from the ring of former marks



### Cursor Position

`C-x =` Show detailed cursor position information

`M-x column-number-mode` Show cursor column number in mode line

`M-x display-line-numbers-mode` Display line numbers next to each line


### Relative line numbers

Display relative line numbers to enhance navigation and editing efficiency

```elisp
;; Display relative line numbers
(setq display-line-numbers-type 'relative)
(global-display-line-numbers-mode t)
```


## Copy & Paste

`M-w` Copy the region into the kill ring (**kill-ring-save**)

`C-y` Yank the last kill into the buffer, at point (**yank**)

The *kill ring* is a list of blocks of text that were previously killed. There is only one ring, shared by all buffers.

`M-y` Cycle through the possibilities or to select one of the earlier kills. (**yank-pop**)



## Erase Text

**character**:

`DEL` Delete the character just before the cursor, usually labeled "Backspace"

`C-d` Delete the character after point (**delete-char**)

**word**:

`M-d` Kill forward to the end of the next word (**kill-word**)

`M-DEL` Kill back to the beginning of the previous word (**backward-kill-word**)



`M-z char` Kill through the next occurrence of *char* (**zap-to-char**)

`M-x zap-up-to-char char` Kill up to, but not including, the next occurrence of *char*

`M-x just-one-space` Delete spaces and tabs around point, leaving one space.

The difference between "killing" and "deleting" is that "killed" text can be reinserted (at any position), where as "deleted" things cannot be reinserted in this way (you can, however, undo a deletion)



### Useless Whitespace

`M-x delete-trailing-whitespace`

​	To delete all trailing whitespace.

`M-\` Delete spaces and tabs around point (**delete-horizontal-space**)

`M-x just-one-space`

​	Delete spaces and tabs around point, leaving one space

`M-SPC` Delete spaces and tabs around point in flexible ways (**cycle-spacing**)

​	Firstly, like **just-one-space**

​	Secondly, like **delete-horizontal-space**

​	Thirdly, restores the original whitespace characters, then it cycles

`C-x C-o` Delete blank lines around the current line (**delete-blank-lines**)



## Filling Text

(This seems designed for Human Languages, as opposed to, say, a computer programming language)

Filling text means breaking it up into lines that fit a specified width. Emacs does filling in two ways. In Auto Fill mode, inserting text with self-inserting characters also automatically fills it. 

`M-x auto-fill-mode`

​	Enable or disable Auto Fill mode

`SPC`

`RET`

​	In Auto Fill mode, break lines when appropriate



`C-x f` Set the fill column (**set-fill-column**)

`M-x fill-region` Fill each paragraph in the region (**fill-region**)

`M-x center-line` Center a line



## Mark & Region

Each buffer remembers previous locations of the mark, in the *mark ring*. Commands that set the mark also push the old mark onto this ring. One of the use of mark ring is to remember spots that you may want to go back to.

`C-SPC C-SPC`

​	Set the mark, pushing it onto the mark ring, without activating it.

`C-u C-SPC` 

​	Move point to where the mark was, and **restore the mark** from the ring of former marks (**set-mark-command**)

`C-x C-x` Set the mark at point, and activate it; then move point where the mark used to be (**exchange-point-and-mark**)


The **region** is the portion of the buffer between the *mark* and the *current point*.

`C-SPC` 

​	Set the mart at point, and activate it (**set-mark-command**)

​	A second `C-SPC` will **deactivate** the mark



**Mark Textual Objects**:

`M-@` Set mark at the end of the next word (**mark-word**). This does not move point. **Repeated** invocations of this command extend the region by advancing the mark **one word at a time**.

`C-M-@` Set mark after end of following balanced expression (**mark-sexp**). This does not move point.

`M-h` Put point and mark around this or next paragraph (**mark-paragraph**).

`C-M-h` Move point to the beginning of the current defun, and set mark at the end (**mark-defun**).

`C-x C-p` Put point and mark around this page (or another page) (**mark-page**).

`C-x h` Select the **whole buffer** as the region




## Balanced Expression

Each programming language mode has its own definition of a balanced expression. Balanced expressions typically include **individual symbols, numbers, and string constants, as well as pieces of code enclosed in a matching pair of delimiters**.

`C-M-f` Move forward over a balanced expression (**forward-sexp**).
`C-M-b` Move backward over a balanced expression (**backward-sexp**).

`C-M-k` Kill balanced expression forward (**kill-sexp**).

`C-M-t` Transpose expressions (**transpose-sexps**).

`C-M-@`
`C-M-SPC` Put mark after following expression (**mark-sexp**).



## Lines



`M-^` **Join** two lines by deleting the intervening newline, along with any indentation following it (**delete-indentation**)



### Blank Lines

`C-o` Insert a blank line after the cursor (**open-line**)

`C-x C-o` Delete all but one of many consecutive blank lines (**delete-blank-lines**)



### Kill lines

`C-k` Kill rest of line or one or more lines (**kill-line**), text on the current line before point is not killed.

When `C-k` is given a positive argument *n*, it kills *n* lines and the newlines that follow them. With a negative argument *−n*, it kills n lines preceding the current line, together with the text on the current line before
point. `C-k` with an argument of zero kills the text **before point** on the current line.

`C-k` kills contents of a nonempty line, while kills the Newline of an empty line.

To kill an entire non-blank line, go to the beginning and type `C-k` **twice**.



`M-k` Kill to the end of the sentence (**kill-sentence**)

`C-S-backspace` Kill an **entire line** at once (**kill-whole-line**) 

`C-w` Kill the region (**kill-region**)


### Wrap lines

In Emacs, you can break long lines based on a maximum line width (e.g., 80 characters) using various built-in and external modes.

`M-q` (**fill-paragraph**)

	Wraps the current paragraph.

`M-x fill-region`

	Wraps the selected region.

`M-x toggle-truncate-lines`

	Emacs may truncate long lines with `$` markers in narrow terminals. This command toggles it with the wrapping display.

`fill-column` settings:

```elisp
;; Set default fill-column width
(setq fill-column 80)

;; Enable auto-fill-mode for all buffers
(add-hook 'text-mode-hook 'auto-fill-mode)

;; For programming modes, use:
(add-hook 'prog-mode-hook 'auto-fill-mode)
```

## Rectangles

### Kill Rectangles

`C-x r k` Kill the text of the region-rectangle, saving its contents as the last killed rectangle (**kill-rectangle**)

`C-x r M-w` (**copy-rectangle-as-kill**)

​	**Save** the text of the region-rectangle as the last killed rectangle

`C-x r d` (**delete-rectangle**)

​	**Delete** the text of the region-rectangle

`C-x r y` (**yank-rectangle**)

​	**Yank** the last killed rectangle with its upper left corner at point



### Insert Rectangles

`M-x string-insert-rectangle RET string RET`

​	Insert string on each line of the rectangle

`C-x r t string RET`
	Replace rectangle contents with string on each line (**string-rectangle**).

`C-x r o` (**open-rectangle**)

​	**Insert** blank space to fill the space of the region-rectangle.
​	This pushes the previous contents of the region-rectangle to the right.

`C-x r N` 

​	Insert line numbers along the left edge of the region-rectangle (**rectangle-number-lines**).
​	This pushes the previous contents of the region-rectangle to the right.

​	Normally, the numbering begins from 1 (for the first line of the rectangle). With a prefix argument, the command prompts for a number to begin from, and for a format string with which to print the numbers.

`C-x r c` 

​	Clear the region-rectangle by replacing all of its contents with spaces (**clear-rectangle**).



## Indentation

`TAB` (**indent-for-tab-command**)

The exact behavior of `TAB` depends on the major mode. In Text mode and related major modes, `TAB` normally inserts some combination of space and tab characters to advance point to the next tab stop.

For this purpose, the position of the first non-whitespace character on the preceding line is treated as an additional tab stop, so you can use `TAB` to **align point with the preceding line**. 

`C-q TAB` Insert a tab character in the buffer.



`C-M-o` Split the current line at point (**split-line**).

​	The text on the line after point becomes a new line, indented to the same column where point is located. This command first moves point forward over any spaces and tabs. Afterward, point is positioned before the inserted newline.

`M-^` Merge the previous and the current line (**delete-indentation**). This joins the two lines cleanly, by replacing any indentation at the front of the current line, together with the line boundary, with a single space.

As special case (useful for Lisp code), the single space is omitted if the characters to be joined are consecutive opening and closing parentheses, or if the junction follows another newline

`M-m` Move (forward or back) to the first non-whitespace character on the current line (**back-to-indentation**)



`M-i` Indent whitespace at point, up to the next tab stop (**tab-to-tab_stop**)

`C-M-\` Indent all the lines in the region (**indent-region**)

`C-x TAB` Indent all lines that begin in the region.

- If called with no argument, activates a transient mode for adjusting the indentation of the affected lines interactively, typing **LEFT** and **RIGHT** indents leftward and rightward.
- If called with a prefix arguments *n*, indents the lines forward by *space*s (without enabling transient mode).



### Tab Stops

Emacs defines certain column numbers to be tab stops. These are used as stopping points by **TAB** when inserting whitespace in Text mode and related Modes, and by commands like `M-i`.

The variable **tab-stop-list** controls these positions The default value is **nil**, which means a tab stop every 8 columns.



### Customizing C  Indentation

`C-c . style RET`

​	Select a predefined style (`c-set-style` in CC mode, `c-ts-mode-set-style` in `c-ts-mode` based on tree-sitter)

Predefined styles: gnu, k&r, bsd, stroustrup, linux, python, java, whitesmith, ellemtel, and awk.



`M-x c-guess` 

​	Guess a style in a sample code buffer



`M-x tabify`

​	Convert existing spaces to tabs in buffer



## Completion

Completion is normally done in the minibuffer, but you can also complete symbol names in ordinary Emacs buffers.

`C-M-i` Invokes the command **completion-at-point**

`M-/` Completes words based on the text present in the current buffer and other buffers (**dabbrev-expand**)



variable **completion-at-point-functions**

Add a custom function that gathers variable names from the buffer for completion, to this hook:

```lisp
(defun my-buffer-variable-completion ()
	(let ((start (save-excursion (skip-syntax-backward "w_") (point)))
			(end (save-excursion (skip-syntax-forward "w_") (point))))
		(list start end
			(completion-table-dynamic
			(lambda (_)
				(let (vars)
					(save-excursion
						(goto-char (point-min))
						(while (re-search-forward "\\_<\\(\\sw+)\\)\\_>" nil t)
							(push (match-string-no-properties 1) vars)))
						(delete-dups vars)))))))
						
(add-hook 'completion-at-point-functions 'my-buffer-variable-completion)
```

### Abbrevs

A defined *abbrev* is a word which *expands*, if you insert it, into some different text. Abbrevs are defined by the user to expand in specific ways. For example, you might define 'foo' as an abbrev expanding to 'find outer otter'. Then you could insert 'find outer otter' into the buffer by typing `f o o SPC`.

A second kind of abbreviation facility is called *dynamic abbrev expansion*. You use dynamic abbrev expansion with an explicit command to expand the letters in the buffer before point by looking for other words in the buffer that start with those letters.

A third kind, *hippie expansion*, generalizes abbreviation expansion.



When you insert a word-separator character following the abbrev, that expands the abbrev--replacing the abbrev with its expansion.

Abbrevs expand only when Abbrev mode, a buffer local minor mode, is enabled.

`M-x abbrev-mode`

​	Toggles Abbrev mode

`C-x a g` Define an abbrev (**add-global-abbrev**)

`C-x a l` Define an abbrev specific to the current major mode (**add-mode-abbrev**)



## Numeric arguments

also called a prefix argument.

`M-5 0 C-n` Move down fifty lines.

`C-u n` Specify a numeric argument by some digits (**universal-argument**)



## Fix Typo

### Undo

`C-x u` Undo a command

`C-/` Redo a command (Bring the reverted changes back)



### Cancel

`C-g` Cancel the command

This is very useful to stop proceed command after pressing `C-x` prefix.



### Transposing Text

`C-t` Transpose two characters (**transpose-chars**)

`M-t` Transpose two words (**transpose-words**)

`C-x C-t` Transpose two lines (**transpose-lines**)



### Case Conversion

`M-l` 	Convert **following** word to lower case (**downcase-wrod**)

`M-- M-l` Convert last word to lower case. `Meta--` is Meta-minus.

`M-u` 	Convert **following**  word to upper case (**upcase-word**)

`M-- M-u` Convert last word to all upper case.

`M-c` 	Capitalize the **following** word (**capitalize-word**)

`M-- M-c` Convert last word to lower case with capital initial.



`C-x C-u` Convert everything in region to lower case (**upcase-region**)

`C-x C-l` Convert everything in region to upper case (**downcase-region**)



### Checking and Correcting Spelling

`M-$` Check and correct spelling of the word at point (**ispell-word**). If the region is active, do it for all words in the region instead.

`M-x ispell` Check and correct spelling of all words in the **buffer**. If  the region is active, do it for all words in the **region** instead.

`M-x ispell-buffer`

`M-x ispell-region`

`M-x ispell-message`



**valid response**:

`digit`: Replace the word

`**SPC**`: Skip this word

`r new RET`: Replace the word, just this time, with *new*

`R new RET`: Replace the word with *new*, and do a **query-replace** so you can replace it elsewhere in the buffer if you wish

`a`: Accept the incorrect word -- treat it as correct, but only in this editing session

`A`: Accept the incorrect word -- treat it as correct, but only in this editing session and in this buffer

`i`: Insert this word in your **private dictionary file** so that it will be considered correct from now on, even in future sessions

`m`: Like **i**, but you can also specify dictionary completion information

`u`: Insert the lower-case version of this word in your **private dictionary file**





## Comments

`C-c C-c` (in C-like modes)

​	Add comment delimiters to all the lines in the region (**comment-region**)

`M-;` 

​	Insert or realign comment on current line; if the region is active, comment or uncomment the region instead (**comment-dwim**)

`C-x C-;`

​	Comment or uncomment the current line (**comment_line**)

`M-j` or `C-M-j`

​	Breaks the current line, and inserts the necessary comment delimiters and indentation to continue the comment (**default-indent-new-line**)



## Text-based Table

`M-x table-fixed-width-mode`
	To toggle the automatic table resizing feature
`M-x table-insert`
	Prompts for the number of table columns, rows, cell width and cell height



### Org Table mode

Add the content below in `.emacs` to enable `orgtbl-mode` in rst file editing

```
;; First ensure Org is loaded
(require 'org)
;; enable ORG table mode in rst file
(add-hook 'rst-mode-hook #'orgtbl-mode)
```



ref: https://orgmode.org/manual/Built_002din-Table-Editor.html

`C-c C-c` 	re-align tables

For **RST tables**, manual separator adjustment is often needed after content changes, while **Org tables** handle alignment automatically on `TAB`/`C-c C-c`.

Convert Org table to RST table:

`M-x orgtbl-to-rst`

`C-c |`



Convert RST table to Org table:

`M-x org-table-convert_region`



## Display



### Text Scale

**text-scale-adjust**

`C-x C-+` or `C-x C-=` Increase the font size of the default face in the current buffer

`C-x C--` Decrease it

`C-x C-0` Restore to the default (global) font size



### Theme display

Accommodate to loading themes in un-known background mode, like from SSH terminal, which is normally dark.

```
;; Set default background mode (important for theme loading)
(setq frame-background-mode 'dark)
```



## Repeating

`C-x z` Repeat a command


## Backup
Specify a location to store backup files generated by emacs

```
;; Create backup directory if it doesn't exist
(setq backup-directory-alist `(("." . "~/.emacs_backups")))
(make-directory "~/.emacs_backups" t)
```


## Help

`C-h` Get help

`C-h k` Learn what a key does what

`C-h f` Get information about a function

`M-x help` Open the help window

​	Then there is a list of prompts for further manipulations. For example:

​	`a PATTERN`: type `a` the a RegEx to show commands matching, like `apropos`



# Advanced misc

## Key Binding

If you want to use a different key-binding, you can add the following to your Emacs configuration (`.emacs` or `init.el`)

```lisp
(global-set-key (kbd "C-c /") 'dabbrev-expand)
```



Check current keybindings:

```
C-h m
```

Unset and rebind conflicting keybindings:

```
(define-key markdown-mode-map (kbd "M-n") nil)
(define-key markdown-mode-map (kbd "M-n") 'scroll-up-line)
```



## Reloading configuration

`M-x load-file`

- Similarly, you can load your configuration file directly by using `M-x load-file`, then entering the path to your configuration file (e.g., `~/.emacs` or `~/.emacs.d/init.el`).



## Extending The Command Set

There are many, many more Emacs commands than could possibly be put on all the control and meta characters. Emacs get around this with the X (eXtend) command. This comes in two flavors:

`C-x` Character eXtend. Followed by one character

`M-x` Named command eXtend. Followed by a long name



## Recursive Editing Levels

Sometimes you will  get into what is called a "recursive editing level". This is indicated by square brackets in the mode line, surrounding the parentheses around the major mode name. For example, you might see [(Fundamental)] instead of (Fundamental).

To get out of  the recursive editing level, type <ESC> <ESC> <ESC>. This is an all-purpose "get out" command. You can use it for eliminating extra windows, and getting out of the minibuffer.

You cannot use `C-g` to get out of a recursive editing level. This is because `C-g` is used for canceling commands and arguments **WITHIN** the recursive editing level.



## Compiling in Emacs

To run make or another compilation command, type M-x compile. This reads a shell
command line using the minibuffer, and then executes the command by running a shell
as a subprocess (or inferior process) of Emacs. The output is inserted in a buffer named
*compilation*. The current buffer’s default directory is used as the working directory for
the execution of the command, so by default compilation takes place in that directory.

Starting a compilation displays the *compilation* buffer in another window but does
**not** select it. While the compilation is running, the word ‘run’ is shown in the major mode
indicator for the *compilation* buffer, and the word ‘Compiling’ appears in all mode lines.
You do not have to keep the *compilation* buffer visible while compilation is running;
it continues in any case. When the compilation ends, for whatever reason, the mode line
of the *compilation* buffer changes to say ‘exit’ (followed by the exit code: ‘[0]’ for a
normal exit), or ‘signal’ (if a signal terminated the process).

`M-x compile`

`M-x recompile`

`M-x kill-compilation` Kill the running compilation subprocess

**Compilation Mode**:

The *compilation* buffer uses a major mode called Compilation mode. Compilation mode
turns each error message in the buffer into a hyperlink; you can move point to it and type
RET, to visit the locus of the error message in a separate window. The locus is the specific position in a
file where that error occurred.

The appearance of the *compilation* buffer can be controlled by customizing the faces
which are used to highlight parts of the *compilation* buffer, e.g., compilation-error or
compilation-warning, for error and warning messages respectively. Note that since those
faces inherit from the error and warning faces, it is also possible to customize the parent
face directly instead.

`M-g n` Visit the locus of the next error message or match (**next-error**).

`M-n` Move point to the next error message or match, without visiting its locus (**compilation-next-error**).

`M-p` Move point to the previous error message or match, without visiting its locus (**compilation-previous-error**).



**grep**:

Just as you can run a compiler from Emacs and then visit the lines with compilation errors, you can also run grep and then visit the lines on which matches were found. This works by treating the matches reported by grep as if they were errors. The output buffer uses Grep mode, which is a variant of Compilation mode

`M-x grep` Run `grep` command like compiling

`M-x grep-find` Run `grep` via `find`




# File Handling

## Visit

Visiting a file means reading its contents into an Emacs buffer so you can edit them. Emacs makes a new buffer for each file that you visit.

`C-x C-f` Visit a file (**find-file**)

`C-x C-r` Visit a file for viewing, without allowing changes to it (**find-file-read-only**)

`C-x C-v` Visit a different file instead of the one visited last (**find-alternate-file**)

`C-x 4 f` Visit a file, in another window (**find-file-other-window**)

`C-x 5 f` Visit a file, in a new frame (**find-file-other-frame**)

`M-x find-file-literally` 

​	Visit a file with no conversion of the contents

## Save

`C-x C-s` Save a file (**save-buffer**)

`C-x s` Save some buffers

`C-x C-w` Save the current buffer with a specified file name (**write-file**)

`M-x rename-visited-file`

​	Change the file name under which the current buffer will be saved

## Exit

`C-x C-c` End Emacs session

`C-z` Suspend Emacs



## Visit File Directories

`C-x C-d dir-or-pattern RET`

​	Display a brief directory listing (**list-directory**)

`C-u C-x C-d dir-or-pattern RET`

​	Display a verbose directory listing

`M-x make-directory RET dirname RET`

​	Create a new directory named *dirname*

`M-x delete-directory RET dirname RET`

​	Delete the directory named *dirname*. If it isn't empty, you will be asked whether you want to delete it recursively.



# File Management - Dired

Dired makes an Emacs buffer containing a listing of a directory, and optionally some of its subdirectories as well. You can use the normal Emacs commands to move around in this buffer, and special Dired commands to operate on the listed files. Dired works with both local and remote directories.

## Entering

`C-x d` Invoke Dired (**dired**)

​	This reads a directory's name using the minibuffer, and opens a *Dired buffer* listing the files in that directory.

## Navigation

All the usual Emacs cursor motion commands are available in Dired buffers. The keys `C-n` and `C-p` are redefined to run **dired-next-line** and **dired-previous-line**, respectively, and they put the cursor at the beginning of the file name on the line, rather than at the beginning of the line.

`SPC` and `n` in Dired are equivalent to `C-n`, `p` is equivalent to `C-p`.

`j` (**dired-goto-file**) prompts for a file name using minibuffer, and moves points to the line in the Dired buffer describing that file.

`M-s f C-s` (**dired-isearch-filenames**) 

​	Performs a forward incremental search in the Dired buffer, looking for matches only amongst the file names and ignoring the rest of the text in the buffer.

`M-s f M-C-s` (**dired-isearch-filenames-regexp**)

​	Does the same, using a regular expression search.

## Deleting

`d`	Flag this file for deletion (**dire-flag-file-deletion**)

`u`	Remove the deletion flag (**dired-unmark**)

`DEL`	Move point to previous line and remove the deletion flag on that line (**dired-unmark-backward**)

`x`	Delete files flagged for deletion (**dired-do-flagged-delete**)

## Visiting

There are several Dired commands for visiting or examining the files listed in the Dired buffer. All of them apply to the current line's file; if that file is really a directory, these commands invoke Dired on that subdirectory (making a separate Dired buffer)

`f`	Visiting the file (Equivalents are `RET`, `e`)

`o`	 Like `f`, but uses another window to display the files buffer (**dired-find-file-other-window**)

`v`	View the file described on the current line, with View mode (**dired-view-file**)

`^`	Visit the parent directory of the current directory (**dired-up-directory**)





# Buffers

The text you are editing in Emacs resides in an object called a *buffer*. Each time you visit a file, a buffer is used to hold the file's text. Each time you invoke Dired, a buffer is used to hold the directory listing. If you send a message with `C-x m`, a buffer is used to hold the text of the message. When you ask for a command's documentation, that appears in a buffer named ***Help***.

Each Emacs window displays one Emacs buffer at any time.

## Create and Select Buffers

`C-x b buffer RET`

​	Select or create a buffer named *buffer* (**switch-to-buffer**)

`C-x 4 b buffer RET`

​	Similar, but select *buffer* in another **window** (**switch-to-buffer-other-window**)

`C-x 5 b buffer RET`

​	Similar, but select *buffer* in a separate **frame** (**switch-to-buffer-other-frame**)



## List Existing Buffers

`C-x C-b` List buffers in Display buffer

`.` in the first field of a line indicates that the buffer is current. 

`%` indicates a read-only buffer. 

`*` indicates that the buffer is modified.

If several buffers are modified, it may be time to save some with `C-x s`.



## Miscellaneous Buffer Operations

`C-x C-q` Toggle read-only status of buffer (**read-only-mode**)

`C-x x r RET buffer RET`

​	Change the name of the current buffer. (**reaname-buffer**)

`C-x x u` Rename the current buffer by adding <number> to the end. (**rename-uniquely**)

`M-x view-buffer RET buffer RET`

​	Scroll through buffer `buffer` in View mode.



## Kill Buffers

`C-x k buffer RET`

​	Kill buffer *buffer* (**kill-buffer**), default to current buffer.

`M-x kill-some-buffers`

​	Offer to kill each buffer, one by one.

`M-x kill-matching-buffers`

​	Offer to kill all buffers matching a regular expression



## Indirect Buffers

`M-x make-indirect-buffer RET base-buffer RET indirect-name RET`

​	Create an indirect buffer named *indirect-name* with base buffer *base-bffer*

`C-x 4 c` Create an indirect buffer that is a twin copy of the current buffer, and select it in another window (**clone-indirect-buffer-other_window**)



## Minibuffer

The *minibuffer* is where Emacs commands read complicated arguments, such as file names, buffer names, Emacs command names, or Lisp expressions. We call it the "minibuffer" because it's a  special-purpose buffer with a small a mount of screen space. You can use the usual Emacs editing commands in the minibuffer to edit the argument text.

When the minibuffer is in use, it appears in the **echo area**, with a cursor.

### Completion

When completion is available, certain keys (usually `TAB`, `RET`, and `SPC`) are rebound in the minibuffer to special completion commands. These commands attempt to complete the text in the minibuffer, based on a set of *completion alternatives* provided by the command that requested the argument. You can usually type `?` to see a list of completion alternatives.



## Display buffer

It is a common Emacs operation to display or pop up some buffer in response to a user command. There are several different ways in which commands do this.

Many commands, like `C-x C-f` (**find-file**), by default display the buffer by “taking over” the selected window, expecting that the user’s attention will be diverted to that buffer.

Some commands try to display intelligently, trying not to take over the selected window, e.g., by splitting off a new window and displaying the desired buffer there. Such commands, which include the various help commands, work by calling **display-buffer** internally. 



# Frames & Windows

When Emacs is started on a graphical display, e.g., on the X Window System, it occupies a graphical system-level display region. In this manual (GNU Emacs Manual), we call this a *frame*, reserving the word "window" for the part of the frame used for **displaying a buffer**. A frame initially contains one window,  but it can be subdivided into multiple windows. A frame normally also contains a menu bar, tool bar, and echo area.

Typing `C-x C-c` closes all the frames on the current display, and ends the Emacs session if it has no frames open on any other displays. To close just he selected frame, type `C-x 5 0`.

## Key Characteristics of Frames:

- **Top-Level Container**: A frame is a high-level container that holds one or more windows.
- **Multiple Frames**: You can open multiple frames within a single Emacs session.
- **Graphical and Text Terminals**: Frames can be displayed on both graphical and text terminals.
- **Shared Buffers**: All frames within an Emacs session share the same set of buffers. Any buffer can be displayed in any window of any frame.

## Key Characteristics of Windows:

- **Subdivisions of Frames**: Windows are smaller sections within a frame.
- **Buffer Display**: Each window shows the contents of a buffer. Multiple windows can display the same buffer.
- **Splitting**: Windows can be split horizontally or vertically to create additional windows within the same frame.
- **Navigation**: You can navigate between windows using keyboard shortcuts like `C-x o` (switch to other window).

A window in Emacs is a subdivision of a frame, windows cannot exist independently; they must reside within a frame. Each window belongs to one and only one frame.

A frame is what we call one collection of windows, together with its menus, scroll bars, echo area, etc.

On a text terminal, Emacs can display only one Emacs frame at a time.

## Frame Commands

`C-x 5 0` Delete the selected frame (**delete-frame**)

`C-x 5 u` When **undelete-frame-mode** is enabled, undelete one of the 16 most recently deleted frames. Without a prefix argument, undelete the most recently deleted frame. With a numerical prefix argument between 1 and 16, where 1 is the most recently deleted frame, undelete the corresponding deleted frame.

`C-z` Minimize (or iconify) the selected Emacs frame (**suspend-frame**)

`C-x 5 o` Select another frame, and raise it. If you repeat this command, it cycles through all the frames on your terminal

`C-x 5 1` Delete all frames on the current terminal, except the selected one.

`M-F10` Toggle the maximization state of the current frame. When a frame is maximized it fills the screen.

`C-x 5 2` Create a new frame and switch to it



## Window Commands

All commands that display information in a window, including (for example) `C-h f` (**describe-function**) and `C-x C-b` (**list-buffers**), usually work by displaying buffers in a nonselected window without affecting the selected window.

Each window has its own mode line, which displays the buffer name, modification status and major and minor modes of the buffer that is displayed in the window.


`C-x 2` Split the selected window into two windows, one above the other (**split-window-below**)

`C-x 3` Split the selected window into two windows, positioned side by side (**split-window-right**)

`C-x o` **Select** another window (**other-window**)

`C-M-v` Scroll the next window upward (**scroll-other-window**)

`C-M-S-v` Scroll the next window downward (**scroll-other-window-down**)

`C-M-S-l` Recenter the next window (**recenter-other-window**)



`C-x 4 b bufname RET`

​	Select buffer *bufname* in another window (**switch-to-buffer-other-window**)

`C-x 4 C-o bufname RET`

​	Display buffer *bufname* in some window, without trying to select it (**display-buffer**)

`C-x 4 f filename RET`

​	Visit file *filename* and select its buffer in another window (**find-file-other-window**)

`C-x 4 d directory RET`

​	Select a **Dired buffer** for directory *directory* in another window (**dired-other-window**)


Deleting and Resizing:

`C-x 0` Delete the selected window (**delete-window**)

`C-x 1` Delete all windows in the selected frame expect the selected window (**delete-other-windows**)

`C-x ^` Make selected window taller (**enlarge-window**)

`C-x }` Make selected window wider (**enlarge-window-horizontally**)

`C-x {` Make selected window narrower (**shrink-window-horizontally**)

`C-x -` Shrink this window if its buffer doesn't need so many lines (**shrink-window-if-larger-than-buffer**)

`C-x +` Balance the sizes of all the windows of the selected frame (**balance-windows**)


# Mode

## The Echo Area

The line at the **very bottom of the frame** is the *echo area*. It is used to display small amount of text for various purposes.



## The Mode Line

At the bottom of each **window** is a *mode line*, which describes what is going on in the current buffer. When there is only one window, the mode line appears **right above the echo area**; it is the next-to-last line in the frame. On a graphical display, the mode line is a drawn with a 3D box appearance. Emacs also usually draws the mode line of the selected window with a different color from that of unselected windows, in order to make it stand out.

The text displayed in the mode line has the following format:

```cs:ch-fr buf	pos line	(major minor)```

On a text terminal, this text is followed by a series of dashes extending to th right edge of the window. These dashes are omitted on a graphical display.

### cs: character set

The `cs` string and the colon character after it describe the character set and newline convention used for the current buffer. Normally, Emacs automatically handles these settings for you, but it is sometimes useful to have this information. 

### ch: changes

The **stars** (`ch`) near the front mean that you have made changes to the text. Right after you visit or save a file, that part of the mode line shows no stars, just dashes.

`%%`: means the buffer is in read-only mode

`**` means there are changes in current buffer

### fr: frame name

The `fr` is frame name in text terminal.

### buf: buffer name

The `buf` is buffer name.

### mode

Last but not least, the part of the mode line inside the parentheses is to tell you what editing modes your are in.



The least specialized mode is called *Fundamental mode*.

Most major modes fall into there major groups.

- Normal text
- Programming languages
- Noe-files



At any time one and only one major mode is active, and its name can always be found in the mode line.

Each *major mode* is the name of an extended command, which is how you can switch to that mode. For example, `M-x fundamental-mode` is a command to switch to Fundamental mode.

`C-h m` View documentation on your current *major mode*

Each *minor mode* can be turned on or off by it self, independent of all other minor modes, and independent of your *major mode*. So you can use no *minor modes*, or one *minor mode*, or any combination of several *minor modes*.



## View mode

View mode is a minor mode that lets you scan a buffer by sequential screenfuls. It provides commands for scrolling through the buffer conveniently but not for changing it.

Apart from the usual Emacs cursor motion commands, you can type `SPC` to scroll forward one windowful, **S-SPC** or **DEL** to scroll backward, and **s** to start an incremental search.

`M-x view-buffer`

​	Prompts for an existing  Emacs buffer, switches to it, and enables View mode.

`M-x view-file`

​	Prompts for a file and visits it with View mode enabled.

Typing `q` (**View-quit**) disables View mode, and  switches back to the buffer and position before View mode was enabled. Typing `e` (**View-exit**) disables View mode, keeping the current buffer and position.



## markdown-mode

Install:

``` sudo apt install elpa-markdown-mode```

Install `grip-mode`:

```M-x package-install RET grip-mode RET```

Install `grip`:

`pip install grip`

ref: https://dev.to/rushankhan1/write-effective-markdown-in-emacs-with-live-preview-41p9

grip: command-line python application.

live preview:

```
(setq grip-binary-path "/path/to/grip")
(add-hook 'markdown-mode-hook 'grip-mode)
(setq grip-url-browser "google-chrome")
```



## Text mode

Text mode is a major mode for editing files of text in a human language. Files which have names ending in the extension **.text** are usually opened in Text mode. To explicitly switch to Text mode. type `M-x text-mode`.

In Text mode, the **TAB (indent-for-tab-command)** command usually inserts whitespace up to the next tab stop, instead of indenting the current line.



## Org Mode

- **TAB** / **S-TAB** – (un)fold (parts / the whole document)
- **M-up/down** – move a headline up or down
- **M-left/right** – promote or demote a headline
- **M-RET** – insert a new headline
- **C-h t** – Emacs tutorial

Unordered lists start with `-,+,or \*`. Ordered lists start with a **number** and a **dot**. Descriptions use `::`.

```
You can make words *bold*, /italic/, _underlined_, =code= and ~verbatim~, and, if you must, +strike-through+.
```

It will look like this:

You can make words **bold**, *italic*, underlined, `code` and `verbatim`, and, if you must, ~~strike-through~~.



- **S-left/right** – cycle workflow
- **C-c / t** – show TODOs in current document

To start working with TODOs , just add the TODO keyword in a headline

```
** TODO buy airplane
```

Configuring TODOs, adding workflow states to the beginning of the file

```
#+TODO: TODO IN-PROGRESS WAITING DONE
```



- **C-c a** – agenda
- **C-c [** – add document to the list of agenda files
- **C-c ]** – remove document from the list of agenda files
- **C-c .** – add date
- **C-u C-c .** – add time and date
- **C-g** – stop doing what you are trying to do, escape





# Variables

A *variable* is a Lisp symbol which has a value. The symbol's name is also called the *variable name*. A variable name can contain any characters that can appear in a file, but most variable names consist of ordinary words separated by hyphens.

The name of the variable serves as a compact description of its role. Most variables also have a *documentation string*, which describes what the variable's purpose is, what kind of value it should have, and how the value will be used. You can view this documentation using the help command `C-h v` (**describe-variable**).

`C-h v var RET` 

​	Display the value and documentation of variable var (**describe-variable**)

`M-x set-variable RET var RET value RET`

​	Change the value of variable *var* to *value*



## Hooks

Hooks are an important mechanism for customizing Emacs. A hook is a Lisp variable which holds a list of functions, to be called on some well-defined occasion. (This is called *running* the hook.)

Most hooks are normal hooks. This means that when Emacs runs the hook, it calls each hook function in turn, with no arguments. We have made an effort to keep most hooks normal, so that you can use them in a uniform way. Every variable whose name ends in **-hook** is a normal hook.

A few hooks are *abnormal hooks*. Their names end in **-functions**, instead of **-hook** (some old code may also use the deprecated suffix **-hooks**). What makes these hooks abnormal is the way its functions are called -- perhaps they are given arguments, or perhaps the values they return are used in some way. For example, **find-file-not-found-functions** is abnormal because as soon as one hook function returns a non-nil value, the rest are not called at all. The documentation of each abnormal hook variables explains how its functions are used.

Add a function to a hook:

```(add-hook 'text-mode-hook 'auto-fill-mode)```

