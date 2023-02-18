# linux-capslock-delay-fix

*Obs: For Wayland and Xorg - Tested only in Ubuntu 22.04 - Credits to AssGoblin69*  

- `cd /usr/share/X11/xkb/symbols/`
- `sudo chmod 777 capslock`

## Replace

This
```
// This changes the <CAPS> key to become a Control modifier,
// but it will still produce the Caps_Lock keysym.
hidden partial modifier_keys
xkb_symbols "ctrl_modifier" {
    replace key <CAPS> {
        type[Group1] = "ONE_LEVEL",
        symbols[Group1] = [ Caps_Lock ],
        actions[Group1] = [ SetMods(modifiers=Control) ]
    };
    modifier_map Control { <CAPS> };
};
```

For this

```
// This changes the <CAPS> key to become a Control modifier,
// but it will still produce the Caps_Lock keysym.
hidden partial modifier_keys
xkb_symbols "ctrl_modifier" {
    key <CAPS> {
        type="ALPHABETIC",
        repeat=No,
        symbols[Group1] = [ Caps_Lock, Caps_Lock ],
        actions[Group1] = [ LockMods(modifiers=Lock), LockMods(modifiers=Shift+Lock,affect=unlock) ]
    };
};
```
- `sudo chmod 644 capslock`

## Some changes in Gnome Tweaks

- Go to **Keyboard and Mouse** > **Additional Layout Options** > **Caps Lock behavior**
- Change **Disabled** to **Make Caps Lock an Additional Ctrl**
- Note that **Make Caps Lock an Additional Ctrl** is the newer version of **Caps Lock is also Ctrl**

*The final `capslock` file is in the repo*
