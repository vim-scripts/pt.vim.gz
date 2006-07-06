Fellow vim fans,

There are syntax files on my website (www.zimmerdesignservices.com) Primetime
tcl (pt.vim), dc_shell tcl (dctl.vim).  A file for 
einstimer/booldozer tcl (eins.vim) is also available.

Extract them and put them wherever you like, then you have to hook them in.

Hooking them in via the ~/.vim directory
----------------------------------------

The easiest way to hook them in is to put them in the directory
"~/.vim/syntax" (save them as "dctl.vim" and "pt.vim").  You can then hook
them in by creating a "filetype.vim" file in "~/.vim" with the following:

au BufRead,BufNewFile *.dctl            set filetype=dctl
au BufRead,BufNewFile *.pt            set filetype=pt

On a PC, there are two possibilities for the ".vim" directory.  On my PC, when
I launch from an icon, it looks at "Documents and Settings\<user>", one level
above "My Documents".  When I launch from cygwin, my home dir is set to "My
Documents", so vim looks for vimfiles there.  I suppose I could sort this mess
out somehow, but the easiest thing is to just create it in two places.


If you store your dctl and pt files as .tcl files
-------------------------------------------------

If you store all your dc/pc and pt scripts as .tcl files, you'll have to
tell vim what the filetype is.  Use the "hooking them in via ~/.vim 
directory" approach above, then put one of the following as a comment at
the beginning of the file:

# vim: filetype=dctl
# vim: filetype=pt

Alternatively, you can just issue the command from vim:

: set filetype=dctl
: set filetype=pt

Hooking them in via the .vimrc
------------------------------

This is the way I had done it for years, until I discovered the .vim technique:
I use the ".pt" suffix for PrimeTime files and ".dctl" for
dc_shell tcl-mode files.  So, I have the following lines in my .vimrc to
automatically invoke the correct syntax file:

autocmd BufNewFile,BufRead *.pt set formatoptions=croql tw=0 expandtab autoindent comments=:#
autocmd BufNewFile,BufRead *.pt source $bin/vim/syntax/pt.vim
autocmd BufNewFile,BufRead *.dctl set formatoptions=croql tw=0 expandtab autoindent comments=:#
autocmd BufNewFile,BufRead *.dctl source $bin/vim/syntax/dctl.vim

As you can see, I store the syntax file in directory "$bin/vim/syntax".
Change this as appropriate.  I also assume that you save the files as 
"dctl.vim" and "pt.vim" (without the version numbers).

Dictionary files
----------------

The tarballs also include .dict dictionary files.  I hook these in by creating
a <language>.vim file in .vim/after/syntax, (vimfiles/after/syntax on the PC)
that looks like this:

set complete=k~/.vim/syntax/pt.dict

To use the dictionary file, just start typing a command and hit ctl-n.  Vim
will give you the first dictionary word (in this case, command) that matches.
ctl_n gets the next.  ctl-p goes backwards.  Very handy.


Details
-------

The syntaxing can handle optional arguments and all their legal abbreviations.
The command names themselves, however, have to be spelled out completely.
I haven't figured out a clean way of doing the command abbreviations.

I am also looking for people to test a script that can create syntax
files from the users procs.  Contact me directly (address below) if you'd
like to try it.  Once I'm sure it works, I'll make it a standard part of
the archive.

I'm also playing with some new "dictionary" files that would allow vim
to do automatic command and option completion, if anyone wants to try them.

BTW, these syntax files source the standard tcl syntax file from the
vim release to do most of the tcl stuff.  I have just added the
language-specific extensions.  I'm not an expert in vim syntaxing, but they
seem to work reasonably well.  Send comments and suggestions to:

paulzimmer@zimmerdesignservices.com


Paul Zimmer 
6 July, 2006
