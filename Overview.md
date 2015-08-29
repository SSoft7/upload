# Overview #



## Introduction ##

Here you can find information about the functionalities of the script, example output and WebUI screenshots. If you want information on how to install the script you can look on the [install](Installation.md) page and for configuration you can look at the [configuration](Configuration.md) page.

## The upload process ##

The `upload` script will walk through a couple steps when you execute it to upload a torrent, below are the steps described:

  * logs you in
  * checks for dupe, if found it downloads the torrent
  * determines the optimal piece size to use
  * creates a torrent
  * checks for dupe again, if found it removes the created torrent and downloads the torrent
  * uploads the torrent
  * runs `rtorrent_fast_resume`
  * moves the torrent to your watchdir


## Usage ##

The most common usage when only using the `.upload.rc` file for a single site is:
```
upload -c "category" /path/to/release/
```
where `category` is the _case-insensitive_ category you want to upload into.

or if you use multiple sites:
```
upload -s abbr -c "category" /path/to/release/
```
where `abbr` is the **case-sensitive** abbreviation which is used for the resource file for the specific site and `category` is the _case-insensitive_ category you want to upload into.

Other possible options are described below:

| **option** | **explanation** |
|:-----------|:----------------|
| -c `<category>` | upload release to category `<category>` |
| -d `<path>` | use `<path>` as your downloads/data directory |
| -h         | show the command information |
| -i         | show extended command information |
| -l         | show available categories |
| -o `<file>` | output log of this upload to `<file>` |
| -p `<password>` | use `<password>` to log in to the site |
| -r `<file>` | use `<file>` as resource file |
| -s `<site>` | use `.<site>.rc` as resource file |
| -t `<path>` | use `<path>` as path to execute the script in |
| -u `<username>` | use `<username>` to log in to the site |
| -w `<path>` | use `<path>` as your torrents/watch directory |
| -x `<test>` | execute `<test>` as test (possible values: cat, mkt, rfr) |
| -y `<number>` | piece size to use (in `2^<number>` bytes, minimum: 15, maximum: 28) |
| -z `<number>` | do NOT use `<number>` bytes as piece size (minimum: 32768, maximum: 268435456) |


## Output and screenshots ##

### Example output ###

Here is an example of the output the script would give when you would execute it manually:
```
user@host:~$ upload -c "tv/xvid" downloads/Some.TV.Show.Release.S01E01.HDTV.XviD-GRP/
torrent upload script v0.9.2 by ScarS

logging in . . . . . logged in

checking for dupe . . . . no dupe found

mktorrent 1.0 (c) 2007, 2009 Emil Renner Berthing

Hashing grp-stsr.0101.hdtv.nfo.
Hashing grp-stsr.0101.hdtv.r00.
Hashing grp-stsr.0101.hdtv.r01.
Hashing grp-stsr.0101.hdtv.r02.
Hashing grp-stsr.0101.hdtv.r03.
Hashing grp-stsr.0101.hdtv.r04.
Hashing grp-stsr.0101.hdtv.r05.
Hashing grp-stsr.0101.hdtv.r06.
Hashing grp-stsr.0101.hdtv.rar.
Writing metainfo file... done.

checking for dupe . . . no dupe found

uploading torrent . . . . . upload complete

Multi file torrent: Some.TV.Show.Release.S01E01.HDTV.XviD-GRP
Total size: 86340942 bytes; 173 chunks; 9 files.

torrent moved to torrent client watch dir.
```


### WebUI screenshots ###

On the list page you can see different colors for the release names, below are the colors and meanings described:
| **color** | **meaning** |
|:----------|:------------|
| <font color='green'>green</font> | uploaded (sorted to the bottom) |
| <font color='blue'>blue</font> | uploading   |
| <font color='red'>red</font> | error (reason in between brackets) |
| <font color='grey'>light/dark grey</font> | hidden (sorted to the bottom) |


There are 3 dropdown boxes behind each release, below are is the reason for each described:
  1. `piece size`: The script will determine the optimal piece size by default, however if you wish to change the piece size (i.e. to avoid dupe hash) you can choose one yourself here.
  1. `site`: here you can select to which site you want to upload
  1. `category`: after you selected which site you want to upload to you can select to which category you want to upload


**The login page**:

![http://upload.googlecode.com/svn/wiki/images/login.png](http://upload.googlecode.com/svn/wiki/images/login.png)


**The light theme**:

![http://upload.googlecode.com/svn/wiki/images/light.png](http://upload.googlecode.com/svn/wiki/images/light.png)


**The dark theme**:

![http://upload.googlecode.com/svn/wiki/images/dark.png](http://upload.googlecode.com/svn/wiki/images/dark.png)