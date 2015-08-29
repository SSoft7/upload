# Installation #



## Introduction ##

Here you can find information on how to install the upload script. If you want to know more about the functionalities of the script you can look on the [overview](Overview.md) page.


## Requirements ##

To be able to use the upload script there are some other programs required, here is a list of the required programs:


### bash ###

For the upload script you are required to use `bash` **version 3.2 or higher**. You can check your `bash` version with the following command:
```
bash --version
```
If you have an old `bash` version you can most likely update it with the following command (for debian-based distro's):
```
apt-get update
apt-get upgrade
```


### curl ###

You can check if you have `curl` installed with the following command:
```
which curl
```
This should output something like `/usr/bin/curl`, if you do not get any output `curl` is most likely not installed. To install `curl` you can run the following command as **root** or **sudo** (for debian-based distro's):
```
apt-get install curl
```
More information about `curl` can be found on the [curl website](http://curl.haxx.se/) and information about compiling it manually can be found on the [curl install page](http://curl.haxx.se/docs/install.html).


### mktorrent ###

For the upload script you are required to use `mktorrent` **version 0.6 or higher**. You can check if you have `mktorrent` installed with the following command:
```
which mktorrent
```
This should output something like `/usr/local/bin/mktorrent`, if you do not get any output `mktorrent` is most likely not installed. To install `mktorrent` you can run the following commands:
```
wget http://downloads.sourceforge.net/mktorrent/mktorrent-1.0.tar.gz
tar -xzf mktorrent-1.0.tar.gz
rm mktorrent-1.0.tar.gz
cd mktorrent-1.0/
make USE_LARGE_FILES=1
make install
```
The `make install` command should be executed as **root** or **sudo**, if you do not have this privilege you can also move the `mktorrent` file which has been created in the `mktorrent-1.0/` dir to your local `/bin` dir. More information about your local `/bin` dir can be found in [upload the bin directory](Installation#The_bin_directory.md) part of this wiki page.


### rtorrent\_fast\_resume.pl ###

It is recommended that you use `rtorrent_fast_resume.pl` with this script, however this is **not required**, and if you do not have **root** or **sudo** you might not be able to use it. The reason it is recommended is because it will allow you to skip the initial hash check when the torrent gets added to `rtorrent`. As you are the person who created the torrent you can be certain that you have the files from the torrent 100% complete.
`rtorrent_fast_resume.pl` can be downloaded from the [libtorrent common tasks](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks#Addingfastresumedatatotorrentfiles) page. To download the script to your home directory you can execute the following command:
```
cd ~/
wget http://libtorrent.rakshasa.no/downloads/rtorrent_fast_resume.pl
chmod 755 rtorrent_fast_resume.pl
```

In order to use `rtorrent_fast_resume.pl` you need `Convert::Bencode` from CPAN. If you do not have this installed you can do so by executing the following command as **root** or **sudo** (so yes, this means that if you do not have this permission and are not able to ask someone to do this for you that you cannot use `rtorrent_fast_resume.pl`):
```
perl -MCPAN -e 'install Convert::Bencode'
```
When it asks you if you want to automate the installation answer yes.


## The bin directory ##

### With root / sudo privileges ###

Download the script from SVN directly into your `/usr/local/bin/` directory and make it executable (you need to run these commands as **root** or **sudo**):
```
svn export http://upload.googlecode.com/svn/trunk/bin/upload /usr/local/bin/upload
chmod 755 /usr/local/bin/upload
```


Or download the gzipped file (make sure to check for the latest version on the [downloads](http://code.google.com/p/upload/downloads/list) page):
```
wget http://upload.googlecode.com/files/upload-v0.9.4.gz
```
and `gunzip` it to your `/usr/local/bin/` directory and make it executable (you need to run these commands as **root** or **sudo**):
```
bash -c "gunzip -c upload-v0.9.4.gz > /usr/local/bin/upload"
chmod 755 /usr/local/bin/upload
```
and then you can remove the .gz file:
```
rm -f upload-v0.9.4.gz
```


### Without root / sudo privileges ###

If you do not have **root** or **sudo** permissions you can also move these files to your local `/bin` directory by replacing the `/usr/local/bin/` with with `~/bin/` in the previous commands.


If your local `/bin` directory does not exist yet you can easily create it with the `mkdir` command:
```
mkdir ~/bin
```

This directory will be prepended to your `PATH` variable upon logging in so you might have to log out and log in in order to be able to run the `upload` script from the `PATH`. If you have any active screen sessions (in which you want to use the `upload` command) you will have to restart these as well. Alternatively you could execute the script as `/home/user/bin/upload` (replacing user with your username) rather than `upload`.


## The home directory ##

To get the files for your home directory move to your homedir:
```
cd ~/
```

Then download the home directory part of the script from SVN:
```
svn checkout http://upload.googlecode.com/svn/trunk/home upload
```

or download the tarball and unpack it (make sure to check for the latest version on the [downloads](http://code.google.com/p/upload/downloads/list) page):
```
wget http://upload.googlecode.com/files/home-v0.9.4.tar.gz
tar -zxf home-v0.9.4.tar.gz
rm home-v0.9.4.tar.gz
```

For security make sure you modify the upload resource files so you are the only one being able to access them:
```
chmod 600 upload/.*.rc
```

However the `.webui.rc` file should be readable for the web user:
```
chmod 644 upload/.webui.rc
```

The `wrapper` file should be modified to be executable:
```
chmod 700 upload/wrapper
```

You can now edit the resource files, more information about this can be found on the [configuration](http://code.google.com/p/upload/wiki/Configuration#The_home_directory) page.

**Note**: for some sites there is already a default included which makes it easier for you to set it up.

## The WebUI ##

To get the files for the web directory move to the web directory (note: you need either **root** or **sudo** to download files to your web directory):
```
cd /var/www/
```

Download the web directory part of the script from SVN:
```
svn checkout http://upload.googlecode.com/svn/trunk/web uploader
```

or download the tarball and unpack it (make sure to check for the latest version on the [downloads](http://code.google.com/p/upload/downloads/list) page):
```
wget http://upload.googlecode.com/files/web-v0.9.4.tar.gz
tar -zxf web-v0.9.4.tar.gz
rm web-v0.9.4.tar.gz
```

You can now edit the `settings.php` file to configure the uploader webui and add the required line(s) to `/etc/sudoers`, more information about this can be found on the [configuration](http://code.google.com/p/upload/wiki/Configuration#The_WebUI) page.