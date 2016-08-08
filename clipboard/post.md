Ratpoison: Clipboard Stack
==========================


This is the second post about the [Ratpoison window
manager](http://www.nongnu.org/ratpoison/).

How many times did you found your self keeping snippets of text in a text editor
just so you can use them later because your clipboard will be overwrited with
the new selection?

Here is a very neat solution using ratpoison: a clipboard stack.

Using `xclip`, a simple shell script and the appropriate ratpoison key bindings
we could accomplish the following:

*Note that `C-t` is the default Ratpoison escape sequence.*

With `C-t =`  the clipboard stack is displayed using `ratmen` so we can select
the snippet we want to be the current one.

        shot 1

With `C-t #` a ratmen menu is displayed so we can perform operations on the
stack such as:

- Push: Push the current selection into the stack
- Pop: Take the last snippet in the stack as the current selection (so we can
        paste it with `Ctrl+v` as usual)
- Delete: Display the list of snippets in the stack so we can select one to
delete it
- Purge: Completely purge the content of the clipboard stack

        shot 2


We get this functionality using the ratpoison bindings:

        bind numbersign  exec clipboard_stack.sh menu
        bind equal  exec clipboard_stack.sh select

**This snippet appears in my `.ratpoisonrc` file that you can read entirely
[here](https://github.com/alx741/dotfiles/blob/master/ratpoison/.ratpoisonrc)**


Note that i've used key bindings that corresponds to the default ones that tmux
uses for the same task.

So now we can push into the stack the selections we know we could use latter and
select them from the list wen needed.

The script depends on
[ratmen](http://www.update.uu.se/~zrajm/programs/ratmen/?M=D)
, [xclip](https://sourceforge.net/projects/xclip/)

And you can get it from my
[Dotfiles](https://github.com/alx741/dotfiles/blob/master/scripts/.scripts/ratpoison/clipboard_stack.sh)

To try it out be sure to define your Ratpoison bindings referencing the right
location of the script.
