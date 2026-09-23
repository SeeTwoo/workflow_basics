# workflow_basics

*vim/neovim*

    Vim/Neovim has modes, three most basic ones are Normal, Insert and Command. While Insert is the expected behaviour of a text editor (key is pressed, something appears), it should be used very sparsely in small surgical strikes. Everything else, deleting, copying, pasting, moving the cursor around, and more, should be done from the other modes. The default one is Normal

    Normal mode can be reached from pretty much anywhere by pressing the <ESC> key (escape key, not E, then S, then C)
    In Normal mode, keys can move the cursor 
    
    h,j,k and l allow to go respectively left, down, up and right
    _   moves to the first non whitespace (space, tab, newline...) character of the line
    w   moves to the next word
    e   moves to the end of the next word
    b   moves to the previous word
    gg  moves to the top of the file (lots of action can also be performed with a combination of keys !)
    G   moves to the bottom of the file
    typing a number N followed by gg goes to the Nth line. e.g. 21gg goes to line 21.

    keys can also do actions

    d   to delete
    y   to yank (copy)
    p   to paste
    c   to change (delete and then enter insert mode)

    hitting an action twice applies it to the current line

    dd  deletes the current line
    yy  copies the current line
    cc  changes the current line

    the actions also combine with the motion, making this system extremely powerful and ergonomic

    dw deletes till the next word
    d3gg deletes everything from the line the cursor is currently on until the 3rd line (works with any line ;)
    dG deletes everything until the end of the file
    tricky one :
    da{ Deletes Around the braces the cursor is in (first group it finds)

    You can also step in Insert mode in a lot of different ways

    i   basic, just insert after the cursor
    a   inserts before the cursor (sometimes useful)
    A   inserts at the end of the line
    o   creates a line underneath and enters insert mode
    O   creates a line over and enters insert mode
    
    ALL OF THAT IS ALREADY A LOT TO TAKE IN
    you do not have to remember everything, just let it hover somewhere in your mind that a good text editor can do all of this for you so when you feel the need you can look how to proceed (usually when you have been doing the same annoying key combination ten times in a row, there usually is a faster way)

    Next there is command mode

    again, commands can do a whole bunch of shit. To enter command mode, press ":" from Normal mode
    most basic commands are

    q   to quit
    w   to write (save) the file. can take the name of the file as an argument if the file doesn't have a name yet
    x   to write and quit
    e   to edit another file (i am in file1.c and I want to go to file2.c without closing/reopening vim/nvim)

    CONFIG

    vim and neovim are both highly configurable
    to me, when both are available, HOW they are configurable is what makes me choose neovim
    vim uses its own scripting language which is said to be clunky by people smarter than me
    neovim embeds lua which is a very small and easy language (i'd say easier than python)

    vim's config file is ~/.vimrc
    nvim's config file is ~/.config/nvim/init.lua
    
    only thing I have shown you for now is the line numbers
    
    in vim you put
    set number
    in your .vimrc

    in nvim you put
    vim.o.number = true
    in you init.lua

*GDB*

    GDB is the Gnu DeBugger
    It allows us to inspect how the programs we write run
    
    to use gdb it is better to compile the code with the -g option
    fyi you can vary the "detail" of the debuging information with a number
    -g1
    -g2
    -g3
    I think in gcc, -g  defaults to -g2
    I have only ever used -g or -g3, never noticed the difference but I know it exists so... yeah

    long story short you compile something like

    gcc -Wall -Wextra -Werror -g3 <filename>

    then you launch gdb with

    gdb --tui <executable name>
    
    --tui is important ! it stands for "text user interface" this is the pretty view where we can see the code run line by line. It is old and sometimes breaks/displays gibberish so you have to "refresh" with Ctrl+l

    gdb has different commands

    run starts running the program, if no breakpoint was set it will run almost as if it was just ran from the shell, without giving much useful information, except maybe for a backtrace when crashes (like the scanf one) appears

    break (or simply b) sets breakpoints where gdb will halt the code in the execution.
    break <the function name where we want to stop and go line by line>

    next (or n) will execute the current line and go to the next line of code

    step (or s) will step into the current line if it is a function call
    
    imagine
        void    somefunction(void) {
            logic();
        }
        
        int main()
        {
            somefunction();
            somevariable = 2;
        }
    if we are on somefunction, n will just go to the next line while s will go in somefunction's code so we can check more thoroughly

    print (or p) will print the value of a variable once
    print <variable name>
    
    display (no shorthand I think) will display the value of a variable at each new gdb command, allowing us to track its state
