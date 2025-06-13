Hatchak
=======

A Dvorak-based keyboard layout with more layers and modifiers.

This is essentially my personal keyboard layout, and I don't believe anybody else uses it.

I may move around things like unicode character placement.
But I'm confident that ascii characters, modifiers, and most unicode will remain in-place at this point.

The major design goals were the following:

- Make all keys pressable without moving hands to another part of the keyboard
- Make modifier keys generally easier and more ergonomic to press, and have as many as possible available
- Keep letters in Dvorak layout

Other benefits include:

- Have numbers arranged like numpad, but accessable in normal layout with consistent modifier to access them (unlike on laptop keyboards that have it similarly)
- Eliminate the need to worry about most differences in laptop keyboards with regards to modifier key layout
- Eliminate the need to worry about small keyboards lacking all of the extra functional keys

I've implemented the keyboard in XKB, which will make it work on any system with a modern X server (Most any UNIX clone), and supposedly Weston (the display server of the (current) future for GNU/Linux.  With any luck the Mir display server will use XKB as well.  The basic features (including all ascii characters) should be implementable on Android's current keyboard system, but I doubt L5-shift or Hyper would be doable.  I expect that to be true on all non-XKB systems at this point.

I've now implemented the layout for the Linux console (tty), although without L5+ or super/hyper (somewhat out of sync, but better than the Andoird version).  Also I've implemented the layout for Android, although without hyper (I don't use it, and it's outdated).  Android has a few annoying issues that I haven't worked out yet.

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

Images
------

Level 1-2 -- IE normal and shifted
![Example](https://github.com/willghatch/hatchak/raw/master/images/hatchak-g1-l1-2.jpg)
Level 3-4 -- IE L3 shifted and L3+shift
![Example](https://github.com/willghatch/hatchak/raw/master/images/hatchak-g1-l3-4.jpg)
Group 2 (level 1-2) -- this is achived with ISO_GROUP_LATCH, which is where the asterisk is on qwerty.  Note that groups don't seem supported under Wayland, so this only works for the XKB version under X11.
![Example](https://github.com/willghatch/hatchak/raw/master/images/hatchak-g2-l1-2.jpg)

Implementations
---------------

The main implementation is the XKB implementation, which works on Linux (and other Unix) on X11 and Wayland.
(XKB is far and away the best and most flexible keyboard implementation used by any major operating system, although it still leaves much to be desired, is poorly documented, etc.)
The XKB implementation will always be up to date.
Other implementations may be incomplete (due to lacking functionality in the keyboard system of another OS, or due to laziness, etc).
Other implementations include:

- Android
- MacOS
- Kanata (which provides Windows support)
- Linux console (IE the Linux kernel's built-in terminal keyboard system)

Each implementation at least supports 3 layers, which includes supporting all ascii characters.

Issues
------

Some programs will not see keys in L3+ land if you switch keyboard layouts while they're running (QT based programs).  If you restart the program then they work as expected.

On Android I can't find a way to do L3 shift without programs simultaneously seeing that Alt is pressed.  This causes issues with eg. Jackpal Terminal.

Thoughts
--------

I first made Hatchak and started using it in 2014.
I decided to switch keyboard layouts for ergonomic concerns.
I had started to feel some minor pain, and I decided that stretching my pinky fingers to especially the control keys on a standard keyboard was likely the biggest issue (I had recently started using modifier keys much more frequently, especially control and super [Windows key]).
As of 2025, I've been using this layout for over 10 years, as well as using ergonomic keyboards most of the time, and I can say that I'm glad that I made the switch, and that I strongly believe that it helped with the pain that I started feeling, and likely prevented more severe and possibly lasting symptoms.
I consider Hatchak to be significantly better than most alternative keyboard layouts, primarily because it moves modifier keys, which was my main problem with Qwerty.

After using it for a few months and getting back to (or at least close to) my previous typing speed with Qwerty, I was glad that I had made the switch, but I also felt like there were various improvements to be made.
Moving the modifiers (eg. control, alt, super, and extra modifiers not normally found on American keyboards) to easier, more ergonomic positions was great, but also encouraged much more use of modifiers.
I did some usage tracking, and found that I was using especially the control key more than many letter keys.
Combined with usage of my “jk” Vim alias that I used at the time to exit insert mode in Vim, which I decided I should move to a “control+SOME_KEY” combination, it would be enough to justify being on the home row, even.
In other words, the keyboard is not only a device for writing text, but also a general controller for controlling software.
Text input and non-text software control are frequently intermixed, and in different situations either one can be more dominant.
Optimizing a keyboard for writing text is missing half of the picture of keyboard use -- at least, for nerds like me.

Since then I've always intended to make another keyboard layout that's even better.
I made a few prototypes that I never thought were good enough, and I've kept track of notes and ideas about it ever since.
But since it's been over a decade now, I'm less confident that I'll ever actually make another serious attempt to make a better keyboard layout and switch to it.

While I have many ideas of what I would do for a new keyboard layout, the most important ideas of a better layout are probably (in order of importance):

1. to include modifier keys like Control among the letter keys, not off in the periphery.
2. to use “sticky keys” for modifiers rather than the typical modifier usage pattern of holding the modifier down until after the other key is pressed, then releasing the modifier.
3. I've waffled about whether to write a third one, but #2 and other ideas that I have imply using more state in keyboarding, and the most important thing with all of this state is to have a consistent and easy way to return to the default state.  IE have a button to clear all latches, locks, layers, or other exotic modes or states, and go back to the default state.  This is critical when you accidentally mash your keyboard (or a child or coworker does), leaving it in a weird and unknown state.

Part of what has kept me from making a better layout, though, is the serious limitations of all major keyboard systems.
The keyboard system of each major operating system is quite limited.
XKB, for Linux, is by far the most flexible and powerful.
But it supports only a small number of modifier keys (Hatchak uses every modifier that XKB supports!  And XKB supports more than the systems for Windows, MacOS, and Android!), it has poor utilities for managing keyboard state (eg. modifier state for latched (sticky) and locked modifiers/groups, for example you can't bind a key to be a “reset all keyboard state” key for when you accidentally mash your keyboard and get into a weird latch/lock state), etc.
Custom firmware for keyboard hardware and event sniffing and spoofing software can remedy parts of this, but are typically limited in different ways -- eg. custom keyboard firmware can support extra layers but can't reliably send Unicode characters, and can't add more Control-like modifiers for making key bindings for software control instead of typing.
Hatchak is already at the edge of what the best operating system keyboard customization supports, and for a future keyboard I want to go farther.
But to go farther likely requires a combination of multiple pieces of software, be much more finnicky, and work on fewer platforms.
