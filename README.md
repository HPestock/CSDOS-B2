# CSDOS-B2
CSDOS Branch 2 (p5.js version, old version has not been supported since b0.1)

CSDOS is an operating system written in javascript with the p5.js graphics library. 

The most recent public build of CSDOS can be run at https://hpestock.github.io/CSDOS-B2/index.html <br>
The most recent unstable build of CSDOS can be run at https://editor.p5js.org/hpestock/sketches/3j858CE5Y <br>
The most recent stable build of CSDOS can be found at https://github.com/HPestock/CSDOS-B2/ <br>

# Executable Files

There are multiple types of executable files currently supported in CSDOS-- 

Javascript Executable Files (.ef): <br>
These files run Javascript through the eval() function, they have complete access to the system and are unprotected from errors. <br>
.ef files are run with the rjef command, which is aliased as "$". Syntax: `rjef [Program Directory]`

Universal Javascript Executable Files (.uef): <br>
These files run Javascript through the eval() function, where .ef files are allowed to directly modify global kernel variables, .uef files should use API functions in order to allow for universal compatibility on systems with concordant methods and specifications. <br>
.uef files are run with the rjef command, which is aliased as "$". Syntax: `rjef [Program Directory]`

Shell Script (.sh): <br>
These files contain a list of commands to be directly evaluated by the command processor. Each command is seperated by a newline character (LF \n). <br>
.sh files are run with the /bin/bac program (.ef) with the syntax `rjef /bin/bac [Script Directory]`

CSDOS Safeguard Executable Language (.csl/.csel): <br>
These files run an interpreted scripting language developed for CSDOS in order to avoid unrecoverable system crashes, which happen when the eval() method encounters an error. <br>
.csl files are run with the /bin/csel-int.ef program with the syntax `rjef /bin/csel-int.ef -i [Script Directory] [Optional: -v, Enables Verbose Output]`

CSDOS Bytecode VM [CBC] (.bin): <br>
These files are run with the CBC Virtual Machine, which is not currently in a usable state. <br>
(When CBC Binaries can be executed) .bin files are loaded into the CBC VM and run with the /bin/cbcmgr.ef program (CBC Manager) with the syntax `rjef /bin/cbcmgr.ef [Binary Directory]`

Brainf Files (.bf): <br>
Brainf is an esoteric programming language with an instruction set of only eight characters, an implementation comes preloaded on CSDOS. <br>
.bf files are run with the /bin/brainf/brainf-int.ef program, and loaded by the /bin/brainf/brainf-int-load.ef program with syntax `rjef /bin/brainf/brainf-int-load.ef [Brainf File]`

# Built-in Tools

There are many built-in tools included with CSDOS-- 

/bin/copy.ef<br>
Copy tool: copies a file<br>
Syntax: `rjef /bin/copy.ef [Existing File Directory] [New File Directory]`

/bin/del.ef<br>
File remove tool: deletes a file<br>
Syntax: `rjef /bin/del.ef [File Directory]`

The following are deprecated tools still available in CSDOS: <br>
/bin/text.ef<br>
/bin/clz.ef<br>

# File Directory Syntax

All folder directories end in '/', files are not allowed to contain '/'. <br>
A directories are indexed in the format `dir/dir/dir/file`. <br>
The root directory is '/', all regular folders and files should be contained under '/', however in cases such as the 'boot/' directory, exceptions are viable. 

# Kernel API Functions

There are multiple API functions contained in the kernel: 

API_RESETRET()<br>
Reset return variables (use at end of standard programs to terminate their frame-loop execution)

API_CKEY()<br>
Get string of most recently used control key (returns string)

API_CKEYDO()<br>
Get boolean of whether a control key has been pressed (returns boolean)

API_DIDCKEYCHK()<br>
Indicate that the most recently pressed control key has been processed (ckeydo = false)

API_SETRETVAR(x)<br>
Set the program return variable (retvar) to x

API_SETRETCMD(x)<br>
Set the program return command (retcmd) to x [string] (use API_SETRETCMD("rjef "+API_DIRCALLED()) for standard program loop functionality)

API_GETRETVAR()<br>
Get the program return variable (expected to return integer)

API_GETRETCMD()<br>
Get the program return command (returns string)

API_DIRCALLED()<br>
Get the directory of the currently running file (use so a file may be called without knowing its directory beforehand, allows for changing name and directory of any uef file) (returns string)

API_RETDIRCALLED(x)<br>
Set directory called (dircalled) (use after calling processcmd() with a variable saving API_GETDIRCALLED() from before processcmd() was called, only needed if rjef is a possible command)

API_CLRINPT()<br>
Clear input buffers (call at the beginning and end of a program's execution)

API_SETTEXTBUFFER(x)<br>
Set the text buffer to x (video mode must be "buffer" or interchangeable for this to affect the display)

API_GETCCATAT()<br>
Get string of at symbol concatenator (@ by default in command line) (retuns string)

API_GETCCATBAR()<br>
Get string of bar symbol concatenator (: by default in command line) (returns string)

API_GETCCATEND()<br>
Get string of end symbol concatenator ($[space] by default in command line) (returns string)

API_GETCCATCUR()<br>
Get string of cursor symbol concatenator (_ by default in command line) (returns string)

API_APPENDTEXTBUFFERPRE(x)<br>
Append string x to the command line display (textbufferpre) (ending string with \n is suggested, otherwise will place text at beginning of machine info)

API_GETVIDEOMODE()<br>
Get video mode string ("buffer", "p5", "buffer_fontstack") (returns string)

API_SETVIDEOMODE(x)<br>
Set video mode ("buffer", "p5", "buffer_fontstack") to x

API_BACKSPACEINPT()<br>
Remove most recent key from keyinput buffer

API_GETKEYINPT()<br>
Returns keyinput (string)

API_SETKEYINPT(x)<br>
Set keyinput to x

API_GETTEXTBUFFERPRE()<br>
Return textbufferpre
