# settings.php #

## Introduction ##

Here you can find information on how to configure the `settings.php` file for the webui. In the file itself there are already comments with an explanation what the setting is for, however I will explain them in a bit more detail where possible.


## The settings.php configuration ##

```
$homedir = "/home";
```
Here you have to enter the path to the home directory. When users try to log in it will check for the username in this directory and if one exists it will look for the `.webui.rc` file for a matching entered password.

```
$sites = array(
    "TV"  => array(
        "Appz/0DAY", "Appz/Mac", "Appz/PC-ISO",
        "Game/Packs", "Games/Misc", "Games/NDS", "Games/PC-ISO", "Games/PS3", "Games/PSP", "Games/Wii", "Games/X360",
        "Documentaries", "Episodes/TV-Boxset", "BlurayTV", "Episodes/TV-DVDR", "Episodes/TV-Foreign", "Episodes/TV-XviD", "Episodes/TV-x264",
        "Movies/Boxsets", "Movies/DVDR", "Movies/Foreign", "Movies/MDVDR", "Movies/XviD", "Movies/x264",
        "Packs/Music", "Music/MP3", "Music/Video", "Retro/Music",
        "Packs/0DAY", "Packs/Ebooks", "Requests", "Ebooks"
    ),
    "AO" => array(
        "Movies|HD", "Movies|XviD", "Movies|DVDR", "Movies|Pack", "Movies|Pack-HD", "Movies|XXX",
        "TV|XviD", "TV|HD", "TV|DVDR", "TV|Pack", "TV|Pack-HD",
        "Apps|PC", "Apps|MAC", "Apps|Nix", "Apps|Mobile",
        "Games|PC", "Games|Xbox", "Games|PS3", "Games|Wii",
        "E-Books", "Misc."
    )
);
```
Here you have to enter which sites and their corresponding categories will be available to be shown in the dropdowns. The dropdowns on the webui page will have the same order as this array unless the sitesort and/or catsort values are set to 1. The array of categories is slightly different from the one in the `.upload.rc` files. Here the categories should be separated by a comma and it should hold only category names (so if you have the IDs after the category in the `.upload.rc` file you should **not** have those here)

```
$default["theme"] = "light";
```
Here you can set the default theme/stylesheet that will be used if the user hasn't specified one. The possible options are light or dark, or if you added any custom stylesheet files you can use those as well. This should be the name of the .css file without the .css extension.

```
$default["sizes"] = 0;
```
Here you can set the default value if sizes should be shown when hovering over the release (i.e. 1.37 GiB). Set this to 1 to enable it by default or to 0 to disable it by default.

```
$default["datasort"] = "latest";
```
Here you can set the default data sorting that will be used if the user hasn't specified one. Possible values are latest or alphabetically.

```
$default["dataorder"] = "desc";
```
Here you can set the default data order that will be used if the user hasn't specified one. Possible values are asc or desc.

```
$default["sitesort"] = 0;
```
Here you can set if the sites will be sorted alphabetically if the user hasn't specified it. Set this to 1 to enable it by default or to 0 to disable it by default.

```
$default["catsort"] = 0;
```
Here you can set if the categories will be sorted alphabetically if the user hasn't specified it. Set this to 1 to enable it by default or to 0 to disable it by default.