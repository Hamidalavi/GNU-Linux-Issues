# Wine Config - No Internet Connection

First sure your ping works: `sudo chmod 4755 /bin/ping`

Enable internet (ICMP):

- `sudo setcap cap_net_raw+epi "$(readlink -f "/usr/bin/wine")"`

or

- `sudo setcap cap_net_raw+epi /usr/bin/wine-preloader` *** work

If this ways not work, remove shared libraries error by: `sudo setcap -r "$(readlink -f "/usr/bin/wine")"`

Disable internet (ICMP):

- `sudo setcap -r /usr/bin/wine-preloader` *** work

wine configuration:

- `winecfg`
- `wine control`
- `winetweaks`
