# Installation

_TODO: describe the system requirements and installation process._

## Setting up the `piku` user

_TODO: describe the need for a separate user and why it's configured this way._

If you're impatient, you need to make sure you have a `~/.ssh/authorized_keys` file that looks like this:

```bash
command="FINGERPRINT=<your SSH fingerprint, not used right now> NAME=default /home/piku/piku.py $SSH_ORIGINAL_COMMAND",no-agent-forwarding,no-user-rc,no-X11-forwarding,no-port-forwarding <your ssh key>
```

## uWSGI Installation 

[uWSGI][uwsgi] can be installed in a variety of fashions. However, these instructions assume you're installing it from source, and as such may vary from system to system.

### Raspbian

Since Raspbian's a fairly old distribution by now, its `uwsgi-*` packages are outdated (and depend on Python 2.6), so we have to compile and install our own version, as well as using an old-style `init` script to have it start automatically upon boot.

```bash
sudo apt-get install build-essential python-dev libpcre3-dev
# at the time of this writing, this installs 2.0.12
sudo pip install uwsgi
# refer to our executable using a link, in case there are more versions installed
ln -s `which uwsgi` /usr/local/bin/uwsgi-piku

# set up our init script
sudo cp uwsgi-piku.dist /etc/init.d/uwsgi-piku
sudo chmod +x /etc/init.d/uwsgi-piku
sudo update-rc.d uwsgi-piku defaults
sudo service uwsgi-piku start
```

[uwsgi]: https://github.com/unbit/uwsgi