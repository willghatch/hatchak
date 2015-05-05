Hatchak
=======

a Dvorak-based keyboard layout for super users

Made by William Hatch <willghatch@gmail.com>

The major design goals were the following:

- Make all keys pressable without moving hands to another part of the keyboard
- Make modifier keys generally easier and more ergonomic to press, and have as many as possible available
- Keep letters in Dvorak layout

Other benefits include:

- Have numbers arranged like numpad, but accessable in normal layout with CONSISTENT modifier to access them (unlike on laptop keyboards that have it similarly)
- Eliminate the need to worry about most differences in laptop keyboards with regards to modifier key layout
- Eliminate the need to worry about small keyboards lacking all of the extra functional keys
- AWESOMENESS

I've implemented the keyboard in XKB, which will make it work on any system with a modern X server (Most any UNIX clone), and supposedly Weston (the display server of the (current) future for GNU/Linux.  With any luck the Mir display server will use XKB as well.  The basic features (including all ascii characters) should be implementable on Android's current keyboard system, but I doubt L5-shift or Hyper would be doable.  I expect that to be true on all non-XKB systems at this point.

I've now implemented the layout for the Linux console (tty), although without L5+ or super/hyper.  Also I've implemented the layout for Android, although without hyper.  Android has a few annoying issues that I haven't worked out yet.

If someone wants to port this, feel free.  I'll probably never make a port for a proprietary OS, and while I don't see many users of such systems wanting to use weird key layouts anyway, if it's of use to you... great.

This layout may change somewhat over time.  For now, this is the gist of things:

- Letters are in standard Dvorak layout, as is shift, comma, and period.
- There is a "Level3" shift (on capslock and quote keys), as well as a "Level5" (on Ctrl keys)
- The keys for tab, tilde, 1, and 2 are respectively control, alt, super, and hyper
- The keys for quote, leftbracket, rightbracket, equal, and minus are respectively control, alt, super, and hyper
- Numbers are accessed with L3 shift, and are placed like a number pad on the right hand
- All ascii non-alphanumerics are on either the number keys or in L3-land.
- L5 has control keys, like arrows, pageup/down, etc on or near the hjkl keys
- L5 on g (u key) is greek dead key
- Tab is on the 3 key
- caps lock is on the grave/tilde key


Issues
------

Some programs will not see keys in L3+ land if you switch keyboard layouts while they're running (QT based programs).  If you restart the program then they work as expected.
On Android I can't find a way to do L3 shift without programs simultaneously seeing that Alt is pressed.  This causes issues with eg. Jackpal Terminal.

