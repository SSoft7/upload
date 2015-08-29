# ScarS' bash torrent uploader #

Here you can find the script used to create and upload torrents with a single command from the command line.


## Main features ##

  * creates and uploads torrents
  * easily customizable for multiple sites (single script, multiple resource files)
  * easy to be called from an external program like `rtorrent`
  * easy to use WebUI


## More info ##

The original script and resource file were created in October 2009 however this googlecode project was started December 2010. Since I created the script in late 2009 I received requests from several people to modify the script for other sites, which I did. In December 2010 I decided to modify the script so only the resource file needs to be changed in order for the script to work for multiple sites.

As it is just a single line command it can also easily be called from the [rtorrent complete command](Configuration#rTorrent_or_other_automation.md) or from a [PHP script](Overview#WebUI_screenshots.md).

The script will also determine the optimal piece size to use for creating the torrent, and when called from `rtorrent` it will choose a different piece size then the current torrent to avoid dupe hash errors in `rtorrent`.

For information about the the script you can take a look at the
[overview](http://code.google.com/p/upload/wiki/Overview) page and for information about installation you can go to the [install](http://code.google.com/p/upload/wiki/Installation) page.


## Bugs, exploits and suggestions ##

If you find any bugs or have any suggestions you can create a new [issue](http://code.google.com/p/upload/issues/entry) to let me and others know so either me or someone else can provide a fix or update. If you find any possible exploits it is probably better if you do not create a public issue but instead send an email to: `code.or.sleep [at] gmail [dot] com`.

If you would like your site to be added (or removed) from the available `.upload.rc` files and `settings.php` file you can also create a new [issue](http://code.google.com/p/upload/issues/entry) to let me know. If you want it added add the proposed `.upload.rc` file and category array for `settings.php` and/or the source of your upload page.


## Donating ##

If you enjoy using this script and would like to send a donation so I can buy more weed to work on this project you can do so by clicking the button below, thanks in advance:

[![](https://www.paypal.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&currency_code=EUR&business=98L2P7LC3PNJY&item_name=uploader)