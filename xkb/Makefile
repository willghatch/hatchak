# Making a single file is not necessary on X11, but is necessary most of the time for Wayland.

hatchak-single-file.xkb: hatchak.xkb types/hatchak compat/hatchak symbols/hatchak
	xkbcomp -I. hatchak.xkb -xkb -o hatchak-single-file.xkb
