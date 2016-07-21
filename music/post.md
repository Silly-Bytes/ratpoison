Ratpoison: Music control
========================


This is the first of a series of posts about the [Ratpoison window
manager](http://www.nongnu.org/ratpoison/).

Ratpoison comes with great flexibility and allows us to do pretty amazing things
binding custom keys and running external programs and scripts; I'm going to
talk about some of the ones i use in the next posts. For the first one, lets
talk about music.

Some people use a graphical music player like Amarok or just play some Youtube
videos, others prefer text players like MOC or CMUS, but we can reach the top of
flexibility using a music daemon like MPD and use our preferred client (MPC,
Ncmpcpp, Vimpc). All this options have somthing in common: you usually interact
with an interface you have to switch to, interrupting your work flow in order to
control your music, but we can do better.

Using the Ratpoison `keymap` functionality we can define a sub mapping bounded
to a master key, So using the key `m` we can define a whole keymap for `music`
control like this:


        newkmap music
        definekey music space exec ~/.scripts/ratpoison/music_control.sh toggle
        definekey music l exec ~/.scripts/ratpoison/music_control.sh select_song
        definekey music L exec ~/.scripts/ratpoison/music_control.sh select_playlist
        definekey music s exec ~/.scripts/ratpoison/music_control.sh stop
        definekey music i exec ~/.scripts/ratpoison/music_control.sh information
        definekey music n exec ~/.scripts/ratpoison/music_control.sh next
        definekey music p exec ~/.scripts/ratpoison/music_control.sh previous
        definekey music period exec ~/.scripts/ratpoison/music_control.sh seek+
        definekey music comma exec ~/.scripts/ratpoison/music_control.sh seek-
        definekey music greater exec ~/.scripts/ratpoison/music_control.sh seek++
        definekey music less exec ~/.scripts/ratpoison/music_control.sh seek--
        definekey music slash exec ~/.scripts/ratpoison/music_control.sh search
        definekey music r exec ~/.scripts/ratpoison/music_control.sh playback repeat
        definekey music z exec ~/.scripts/ratpoison/music_control.sh playback random
        definekey music y exec ~/.scripts/ratpoison/music_control.sh playback single
        definekey music c exec ~/.scripts/ratpoison/music_control.sh playback consume
        definekey music question help music
        bind m readkey music


**This snippet appears in my `.ratpoisonrc` file that you can read entirely
[here](https://github.com/alx741/dotfiles/blob/master/ratpoison/.ratpoisonrc)**

Here we define a keymap `music` and, at the end, bind it to `m` key so we can
get to it by triggering:
* Note that `C-t` is the default Ratpoison escape sequence.

        C-t m

And then pressing the respective music command:

        space   Pause/Play
        l       Select song from playlist
        L       Select playlist
        s       Stop
        i       Playing information
        n       Next
        p       Previous
        .       seek forward
        ,       seek backward
        >       seek forward more
        <       seek backward more
        /       Search song (in the entire music repository)
        r       Toggle -repeat-
        z       Toggle -random-
        y       Toggle -single-
        c       Toggle -consume-
        ?       Print binded keys help


So, for instance, we could visualize the current playing song, and modes states
by issuing:

        C-t m i

http://imgur.com/5u7ZFIL

Here the first line represents the playing status:

    [|]  Paused
    [>]  Playing

The second line is the song currently playing/paused.
The third line is the song number in the playlist and the time played/remaining.
The forth line Marks with an `*` the enabled modes.


The script depends on
[ratmen](http://www.update.uu.se/~zrajm/programs/ratmen/?M=D)

And you can get it from my
[Dotfiles](https://github.com/alx741/dotfiles/blob/master/scripts/.scripts/ratpoison/music_control.sh)

To try it out be sure to define your Ratpoison bindings referencing the right
location of the script.
