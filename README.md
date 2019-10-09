# Dynamic motd

The aim of this project is to give some informations when you log into a server through SSH.

Example:

```

   ___  ___ _ ____   _____ _ __
  / __|/ _ \ '__\ \ / / _ \ '__|
  \__ \  __/ |   \ V /  __/ |
  |___/\___|_|    \_/ \___|_|


  Raspbian GNU/Linux 10 (buster) (kernel 4.19.75-v7+)

System load:   1.00 1.02 1.01   Up time:       5 days
Memory usage:  15 % of 926MB    IP:            192.168.0.105
Usage of /:    16% of 14G

System load:   1.00 1.02 1.01   Up time:       5 days
Memory usage:  15 % of 926MB    IP:            192.168.0.1 / 85.142.21.134
CPU temp:      39.2°C
Usage of /:    16% of 14G

Last login: Wed Oct  9 18:46:24 2019 from 192.168.0.24
```

**Warning** This Debian and Debian-related distributions only.

## Dependencies

You need to install some packages:

```
apt-get install toilet lsb-release python-utmp bc
```

Optionnally, you can install `needrestart` which is used to show a message if your server need a reboot (main reason (and the only one I know): you have upgraded your kernel).
If you don't install `needrestart`, it will work, but you won't be warned about the need for a reboot.
`needrestart` warns you about services that need to be restarted too (but is slower than `checkrestart` for that, see below).

You can optionnally install `debian-goodies` which provides `checkrestart`, which will be used to warn you about services that need to be restarted. Relying on `needrestart` for that is slow (±7 seconds) while `checkrestart` do it faster (less than one second).

## Installation

```
cp -r update-motd.d/ /etc
rm /etc/motd
ln -s /var/run/motd /etc/motd
```

## Salt

You will find a working salt formula in `init.sls`.

```
cd /srv/salt
git clone https://framagit.org/luc/dynamic-motd.git motd
salt your_server state.sls motd
```

## License

GPLv2. Have a look at the [LICENSE file](LICENSE).

## Acknowledments

- Dustin Kirkland, the guy behind the Ubuntu dynamic motd (I took some scripts from Ubuntu and stole inspiration too :D)
- https://github.com/maxis1718/update-motd.d for the skeleton
- https://github.com/jnweiger/landscape-sysinfo-mini for the python script (slightly modified)
