# gopass-i3wm wrapper

This repo provides a bunch of scripts and configs to work with Gopass in i3wm:

* i3wm config - set of menus and hotkeys to call a bash script
* gopass.sh bash script - wrapper which handles different behaviour
* rofi theme - a simple theme file adopted from the default one

One of the behaviour that gopass.sh bash script provides - is an ability to share a password via nginx web server

## Software you will need:
rofi, dmenu, xdotool, tilix (for qr codes)

### i3wm config
#### Basic usage:
Pressing `$mod+Print` - displaying a rofi menu, selecting the item will:
1) copy the password to clipboard
2) store a path to selected item in /dev/shm/dmenu-pass on the localhost

That is covering a most basic everyday needs with fast searching for a passwords
#### i3wm menu
Gopass menu `$mod+Ctrl+Print`

Here you find a 7 different hotkeys that can expand the usage of the gopass.  
All additional hotkeys are using Mod1 modifier to prevent from accidential pressing.  
Before using a menu you should select an item with `$mod+Print`  
* `Mod1+n` - type 'username' from item if found one
* `Mod1+p` - type password. Extremely helpful on a remove consoles eg VmWare
* `Mod1+u` - type 'ur' from item if found one
* `Mod1+e` - type an entry name
* `Mod1+c` - add password to clipboard (as `$mod+Print` does)
* `Mod1+q` - display a qr code for a password with a drop-down tilix terminal
* `Mod1+s` - publish a secret on nginx server via ssh and placing an URI to clipboard

### gopass bash script
Only few vars to mention:  
`QUAKE_TERMINAL_KEY="Super_L+backslash"`  
The idia behind is to use a drop-down quake-like console of tilix terminal and print qr code there.  
`SITE="pass.example.com/share"` - site path, in order to use sharing
`SSH_SERVER` - your ssh server with nginx

### rofi theme 
A modified theme came with PeuxOS I guess.   Didn't spent there much, just updated a colors, columns and made it transparent.   Credentials saved.

### Nginx 
In order to use a sharing you will need to have an nginx server accessible via ssh. I'll left behind .ssh_config and keys.  
I've chosed to use a subdomain and issued letsencrypt certs for sharing domain. Make what feets you best. If you don't have a root on the nginx server set paths in cronjob and nginx config accordingly.
In this package you'll find a nginx confg example and crontask.  

*The default behaviour is to remove a secret just after it has been accessed*  
All unnopened more than 24h secrets removing as well.
In first run you should create a directories on server  
`mkdir -p /dev/shm/pass/share && chown -R root:nginx /dev/shm/pass && chmod -R 750 /dev/shm/pass`

### Afterwords
I hope someone will find this package useful  
Feel free to use it, improve and leave comments  
No warranty, using of this package assume you know what you are doing ;)

