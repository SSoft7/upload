# Frequently Asked Questions #



## Introduction ##

This page is pretty self-explanatory, here I will post the most frequently asked questions about the `upload` script. If you have any questions you can either contact me on IRC (I'm usually on `irc.p2p-network.net` as `ScarS` however you may find me on other networks under that nick as well), or you can leave a comment with a question.


## Questions and answers ##

Here you will find the the questions and their answers:


### How do I use the script? ###

More information about how to use the script can be found on the [usage](Overview#Usage.md) wiki page.


### Do I need root or sudo privileges to install the uploader? ###

No, you do not need root or sudo privileges. If you don't have these you should [install the script and other needed binaries into your local bin directory](http://code.google.com/p/upload/wiki/Installation#Without_root_/_sudo_privileges).
If you do not have sudo or root privileges you cannot use `rtorrent_fast_resume.pl` (unless `Convert::Bencode` is installed) or use the WebUI though.


### Is rTorrent required to use this script? ###

No, `rtorrent` is not required, you could also use some other `*`nix torrent client which supports loading files from a torrents/watch directory. If you do not use `rtorrent` you cannot use `rtorrent_fast_resume.pl` though, however that client may have an alternative way of dealing with skipping a hashcheck.


### Could you add a default resource file for my site? ###

Sure, just post a new [issue](http://code.google.com/p/upload/issues/entry) and leave the proposed `.upload.rc` (where `upload` is replaced with your site abbreviation) and array for `settings.php` for the WebUI and I'll add it.


### What happens when there is no .nfo file? ###

A temporarily `.nfo` file will be created so the nfo and description can be filled. This temporarily nfo file will not be included in the torrent though (this is not needed either). The temporarily nfo that will be created will look like this:

```
name: Release.Name.S00E00.DVDRip.XviD-GRP
category: TV/XviD
size: 174 MB
No NFO was supplied for this release
```


## Troubleshooting ##

### I get the error that something isn't a command, but they seem right ###

Make sure that the command file has been modified to be executable (`chmod 755` usually). You can check this with `ls -l` (lowercase L) and see if the x option is available. Also check the next question about the path being wrong.


### I get the error that one of my paths is wrong, but they seem right ###

Make sure the right settings file is loaded. It should output which settings file it loads and if you use a `.site.rc` and you forgot to use the `-s site` or `-r .site.rc` option it will load the default `.upload.rc` which possibly has the wrong settings.


### I get the error that the category was no found in the list of categories ###

Make sure you are trying to upload into a valid category. You can use the `-l` (lowercase L) flag to find out the available categories.


### I get the error that I used an invalid piece size option ###

If you are using the `-y` trigger make sure the value is between 15 and 28, the script will then use `your value^2` bytes as piece size.

If you are using the `-z` trigger make sure the value is between 32768 and 268435456 which is the byte size the torrent will **NOT** be created with.


### I get the error that I entered too many variables ###

Make sure that if the path to the file or directory you want to upload contains a space you either escape the space (by adding a backslash in front of it) or adding quotes (either double `"` or single `'`) around the whole path string.


### I get the error that I could not be logged in, however I think I have all the settings right ###

Double check the [login settings](http://code.google.com/p/upload/wiki/uploadrc#login_settings) and make sure all variables are entered correctly.

Your password can **NOT** contain an ampersand (`&`) or equal sign (`=`).

If you have a dollar sign (`$`) or a backslash (`\`) in your password you should add a backslash (`\`) in front of it because else it will not read your password correctly.

`LOGINTXT` should be a text that can **NOT** be found on the login page. I.e. if your nick is _login_ you should **NOT** use this as `LOGINTXT`, use something else unique that can **NOT** be found on the login page. This text is **case-sensitive**.

`LOGINUSR` and `LOGINPWD` should **NOT** contain your site username password but should only indicate the form input names. (so i.e. the input is `<input type="text" name="username" />` as field where you have to enter your username then the `LOGINUSR` should be `username`.

Also make sure the URL to the login page is right. In the example .rc files the site abbreviation is used and **NOT** the full URL so make sure you change this. The URL is used in several variables in the .rc file so make sure you change all of them.


### All torrents I upload say they are dupes, but they are not on the site yet ###

Make sure your `SEARCHURL` is correct, try this out yourself on the site. If this value is wrong it may load the normal browse/torrents page which will (almost) always have results.


### I cannot log in to my WebUI ###

Make sure your home directory is readable, the upload directory is readable, and the `.webui.rc` is readable.

The WebUI looks in `/home/USER/upload/.webui.rc` for the login password. `/home/` is defined in `settings.php`. Your log in will also fail if your `data` variable (path to your downloads) does not contain your username, this is to prevent anyone from listing contents that are not theirs. If your data directory is in a different place I suggest you create a symbolic link to the data (i.e.: `ln -s /path/to/data/ /home/USER/data/`).

If you use SELinux you have to allow your web user to read the home directory and the contents. As **root** or **sudo** run the following commands:

```
setsebool -P httpd_enable_homedirs 1
setsebool -P httpd_read_user_content 1
```


### When I upload through the WebUI it doesn't give an error but it doesn't change the page either ###

Make sure the `HOME` value in the `wrapper` file in your home `upload` dir is correct.


### I uploaded a release to multiple sites but it only shows up once in my client ###

Several clients will not load a torrent with the same info-hash in the client twice. The best way to avoid getting the same info-hash is by using a different piece size to create the torrent. You can use the `-y` option to create a torrent with a specified piece size.