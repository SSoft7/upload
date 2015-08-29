# Configuration #



## Introduction ##

Here you can find information on how to configure the upload script files. If you want to know more about the functionalities of the script you can look on the [overview](Overview.md) page.


## The home directory ##

In the home directory you can find two different kinds of resource files, the `.webui.rc` file which holds information for the webui, and the `.upload.rc` type files which hold information about the sites you can/want to upload to.


### .upload.rc ###

In the file itself there are already comments with an explanation what the setting is for, however on the following wiki page they are explained in more detail where possible:

[.upload.rc configuration](uploadrc.md)


### .webui.rc ###

In the file itself there are already comments with an explanation what the setting is for, however on the following wiki page they are explained in more detail where possible:

[.webui.rc configuration](webuirc.md)


### wrapper ###

If you are planning on using the webui you need to edit a single line in the `wrapper` file:
```
HOME=/home/user
```
In this enter your home path (most likely just replace `user` with your username).


## rTorrent or other automation ##

If you have the `upload` script installed and configured your `.upload.rc` files you can add a line to your `.rtorrent.rc` so it will call the `/home/user/upload/wrapper` file upon a download's completion:
```
system.method.set_key = event.download.finished,upload_torrent,"execute=/home/user/upload/wrapper,rtorrent,$d.get_chunk_size=,$d.get_base_path="
```
This will call the `/home/user/upload/wrapper` file which in turn executes the `upload` script.
**Note**: replace the `/home/user/upload/wrapper` with the path to your wrapper (most likely just replace `user` with your username)


Currently the `wrapper` file has only a single `upload` line in it for rtorrent:
```
# if invoked by rtorrent
elif [ $1 = "rtorrent" ]; then
    cd "$HOME/upload"
    upload -z $2 "$3" >/dev/null 2>&1 &
fi
```
In this case it will take the default `.upload.rc` file to use as resource. If you want to change this you can easily add the `-s <site>` option:
```
# if invoked by rtorrent
elif [ $1 = "rtorrent" ]; then
    cd "$HOME/upload"
    upload -s abbr -z "$2" "$3" >/dev/null 2>&1 &
fi
```
where `abbr` is the case-sensitive abbreviation which is used for the resource file for the specific site (i.e. `.abbr.rc`). If you want you could add several of these lines (under eachother) to automate the uploading to several sites.

The call to the `upload` script is without specifying a category to upload in, so you need to set up filters in your `.upload.rc`.

To automate the script from another program (i.e. FTP program that has an oncomplete even) you could add a piece of code similar to the one for rtorrent under it with the parameters you want to use.


## The WebUI ##

In order to be able to use the webui the web user needs to be able to execute the wrapper file in the users their home upload directory as that user. In order to do so you need to add an extra line in the `/etc/sudoers` file.

In the webui directory there is only one file you need to edit which is the `settings.php` file. You can however if you want to add more .css files, this can be easily done by copying either the `light.css` or `dark.css` file and replacing the values.

Users who want to use the WebUI also need to have matching `.abbreviation.rc` ((where `abbreviation` is the abbreviation of the site as it's used in `settings.php`) files in their `/home/user/upload/` directory so the script knows to which site it needs to upload.

### visudo ###

To edit the `/etc/sudoers` file you need to run the following command as **root** or **sudo**:
```
visudo
```
This should open the `/etc/sudoers.tmp` file where you can add the following line:
```
www-data ALL=(user1, user2) NOPASSWD: /home/user1/upload/wrapper, /home/user2/upload/wrapper
```
Of course you need to replace user1 and user2 with the user(s) you want to be able to use the webui upload command. If your web user has a different name than `www-data` (i.e. `http`) you need to replace this as well.

This command will allow your web user (i.e. `www-data`) to execute the file `/home/user1/upload/wrapper` as `user1` without having to enter a password (normally when you `sudo` you need to enter a password).


### settings.php ###

In the file itself there are already comments with an explanation what the setting is for, however on the following wiki page they are explained in more detail where possible:

[settings.php configuration](webconfig.md)