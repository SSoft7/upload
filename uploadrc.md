# .upload.rc #



## Introduction ##

Here you can find information on how to configure the `.upload.rc` type files. In the file itself there are already comments with an explanation what the setting is for, however I will explain them in a bit more detail where possible.

It is recommended that if you use multiple sites to upload to you rename the `.upload.rc` file to `.abbreviation.rc` (where `abbreviation` is the abbreviation of the site). This is also required if you want to use the WebUI.

## The .upload.rc configuration ##

### login settings ###

```
USERNAME="user"
```
The username you use to log in to the website

```
PASSWORD="abcdefgijk"
```
The password you use to log in to the website.

**Note**: if you have a dollar sign (`$`) or a backslash (`\`) in your password you should add a backslash (`\`) in front of it because else it will not read your password correctly. The ampersand (`&`) and equal (`=`) sign will also cause problems and these can not be used in your password.

```
LOGINURL="http://www.torrentsite.tld/login.php"
```
The URL where the login form data should be posted to. For gazelle installations this is usually `login.php` and for TBDev installations this is usually `takelogin.php`. You can look at the page source what is written in the `action=""` part of the `<form>` tag.

```
LOGINTXT="user"
```
A _unique_ piece of text from the page you get directed to after you have logged in which will be used to check if you are logged in. A possible value for this could be your username provided this is something unique and will be shown on the page you get directed to after you are logged in.

**Note**: This text is **case-sensitive**.

```
LOGINUSR="username"
```
The form input name which is used to submit the username. You can look at the page source and look at the `<input>` tag which is used for the username. This is usually something like `username` or `user`.

**Note**: This should **NOT** be your username. I.e. the input is `<input type="text" name="username" />` as field where you have to enter your username then the `LOGINUSR` should be `username`.

```
LOGINPWD="password"
```
The form input name which is used to submit the password. You can look at the page source and look at the `<input>` tag which is used for the password. This is usually something like `password` or `pass`.

**Note**: This should **NOT** be your password.


### search settings ###

```
SEARCHURL="http://www.torrentsite.tld/torrents.php?search="
```
The complete URL which is used to search for a release. You can execute a search on the site and look what is in the address bar and copy that here (without the name of what you searched for obviously). The release you want to upload will be appended to the end of this URL so make sure that if there are any extra options in the URL you add those before the search name. i.e. if the url would be `...torrents.php?search=name&incldead=1` you should enter the URL here as `...torrents.php?incldead=1&search=`

```
SEARCHTXT="No results found"
```
A _unique_ piece of text from the search page which will be used to see if there are no results found so the release won't be a dupe.

```
DUPEDL=0
```
This variable should be set to 1 if you want to download the release from the site that has already been uploaded. For this to be possible the direct download link should be available on the search page.

```
DUPEURL="http://www.torrentsite.tld/"
```
This is the URL that will be prepended to the download link. If the direct download link already contains the full URL leave this empty.

```
DUPETXT="action=download"
```
A _unique_ piece of text from the search page which will be used find the exact line where the download link is located.

```
DUPECMD="cut -d \" -f 2"
```
This is the command that will be executed to extract the download link from the complete line which has been obtained by searching for the `DUPETXT`.
This might be too advanced for some users that are not familiar with linux so I suggest you ask someone that is more experienced with string extraction in linux command line to help you with this.
Suggestions are to use the [cut](http://unixhelp.ed.ac.uk/CGI/man-cgi?cut) **or** [sed](http://unixhelp.ed.ac.uk/CGI/man-cgi?sed) commands. In the previous example it uses `cut`, in the next example it uses `sed`:
```
DUPECMD="sed s/.*\(download.php.*torrent\).*/\1/"
```


### upload settings ###

```
UPLOADURL="http://www.torrent-site.tld/upload.php"
```
The URL where the upload form data should be posted to. You can look at the page source what is written in the `action=""` part of the `<form>` tag.

```
ANNOUNCEURL="http://tracker.torrent-site.tld/s0m3p4ssk4yf0rth3s1t3/announce"
```
This is your _personal_ announce URL used to upload the torrent.

```
UPLOADTOR="torrent"
```
The form input name which is used to submit the torrent. You can look at the page source and look at the `<input>` tag which is used for the torrent. This is usually something like `torrent` (TBDev) or `file_input` (Gazelle).

```
UPLOADCAT="cat"
```
The form input name which is used to submit the category. You can look at the page source and look at the `<select>` tag which is used for the category. This is usually something like `category` (TBDev) or `type` (Gazelle).

```
UPLOADXTRA="-F 'submit=true' -F 'nfo_file=@\$NFO' -F 'descr=<\$NFO' -F 'anonymous=on' -F 'auth=s0m34uthk3yf0rth3s1t3t00'"
```
here you can enter any other required (or optional) values that need to be posted such as title, nfo and description. You can use the variables `$NAME` (directory/file name that is being uploaded), `$NFO` (path to the .nfo file) and `$CAT` (category used for uploading), however these should be escaped with a backslash (`\`). The `@` character can be used to specify that **the file** should be uploaded and the `<` character can be used to specify that the **contents** of the file should be uploaded, this applies to the `$NFO` variable.

In Gazelle installations it is usually need to add `submit=true` and possible `auth=authkey`. Some sites also have a checkbox for anonoymous so something like `anonymous=on` could be used.

These values should be added in the form of `-F 'name=value'`.

More information about the possible options can be found on the [curl man page](http://curl.haxx.se/docs/manpage.html).


### path settings ###

```
DOWNLOADS="/home/user/downloads/"
```
This should be the path to your downloads/data directory where the data you want to upload is located.

```
TORRENTS="/home/user/torrents/"
```
This should be the path to your torrent client watch directory, after the torrent is uploaded it will be moved to this directory.

```
LOGFILE="/home/user/upload/upload.log"
```
This is the path to the file where the upload script will log whether uploads have failed of succeeded. If you do not want to use logging set this path to `/dev/null`.

```
CURL="curl"
```
This is the path to the `curl` binary. If the binary is located in your PATH you can just enter `curl`.

```
MKT="mktorrent"
```
This is the path to the `mktorrent` binary. If the binary is located in your PATH you can just enter `mktorrent`.

```
RFR="/home/user/rtorrent_fast_resume.pl"
```
This is the path to `rtorrent_fast_resume.pl`, if you do not wish to use this you can leave it empty.


### advanced settings ###

```
USERAGENT="Mozilla/4.0"
```
This is the string that will be used to specify the user-agent that the upload script "uses" to connect the site. Some sites do not allow wget/curl user-agents so with this you can specify something else.

```
PREPEND="au."
```
This is the string that will be prepended to the torrent before moving it to your torrent client watch directory. It is recommended that you use this in order to avoid getting duplicate/overwritten torrents in your watch directory. If you are going to upload the same releases to multiple sites it is recommended that you set this prefix to the site abbreviation.

```
UPCHECK=1
```
This value should be set to 0 if you do not want the script to check if a torrent is already being uploaded. I you want to upload the same release to multiple sites this is needed however it can also mean that if you accidentally execute the upload command for the same site twice you will waste resources.

```
ALLCATS=(
        "TV/XviD" "TV/HD" "TV/Pack"
        "Movies/XviD" "Movies/DVDR" "Movies/BluRay" "Movie/Pack" "XXX/XviD"
        "Games/PC" "Games/Xbox" "Games/PSX" "Games/Wii" "Games/Misc" "Games/Pack"
        "Music/MP3" "Music/FLAC" "Music/Video" "Music/Misc" "Music/Pack"
        "0day" "Ebook" "Misc"
)
```
This array holds all the categories you are able to upload into on the site. Some characters like `|`, `)` and `(` should be escaped (add a backslash before the character). You should check check source of the upload page to see if the `<option>` tag value has a different value than the category name (this could be a number on some sites, mostly TBDev based). If the option value differs from the category name you should add this **after** the category name in the array.

```
KEYVAL=0
```
As explain at the previous setting some sites have a different option value than the category name. If this is the case you should have added the option values after the category name in the array of the previous setting, and you have to set this value to 1.


### filter settings ###

Filters are read from first to last and the first match will be taken so it is best to have the most specific filters at the top and the more generic filters at the bottom.

```
FILTERS[n]="^(house|simpsons|south.park).*S[0-9]{2}E[0-9]{2}.*XviD"
EXCEPTS[n]="DSR|REPACK"
MINS[n]=70
MAXS[n]=400
CATS[n]="TV/XviD"
let n+=1
```
The filters are needed if you want to allow executing the upload script without specifying a category (i.e. from another program like `rtorrent`). If a category has not been specified the script will check these filters to see if a match has been found and if so it will use the category specified here.

Below are the settings of the filters explained in more detail:

```
FILTERS[n]="^(house|simpsons|south.park).*S[0-9]{2}E[0-9]{2}.*XviD"
EXCEPTS[n]="DSR|REPACK"
```
Here you can specify a _case insensitive_ regular expression which will be matched against the release name. There are several examples in the scripts with possible regular expressions to use, it might be a good idea to discuss setting up these filters with someone who is somewhat experienced with regular expression. A small explanation:
| **symbol** | **meaning** |
|:-----------|:------------|
| ^          | start of the line |
| $          | end of the line |
| (a|b|c)    | match either a, b or c |
| `[`a-z`]`  | match anything from a to z |
| .          | match any character |
| ?          | match 0 or 1 time |
| `*`        | match 0 or more times |
| +          | match 1 or more times |
| {n}        | n characters |

More information about bash regular expression can be found [on this page](http://www.faqs.org/docs/abs/HTML/regexp.html)

```
MINS[n]=70
MAXS[n]=400
```
Here you can specify sizes which will be matched against the release directory. The values should (obviously) be numeric and will be read as MB.

```
CATS[n]="TV/XviD"
```
Here you specify the category where the release should be uploaded into if it passes the filter. If the category option value is different then the category name you should **not** use the category name here but the category option (which is usually a number). If you do enter a category name it should be **case sensitive**

```
let n+=1
```
This line is needed after every filter to increase the filter counter. If you forget this line the filter that comes after this will overwrite the previous filter.