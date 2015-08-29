# .webui.rc #

## Introduction ##

Here you can find information on how to configure the `.webui.rc` file. In the file itself there are already comments with an explanation what the setting is for, however I will explain them in a bit more detail where possible.


## The .webui.rc configuration ##

```
pass = abcdefg
```
Here you have to set the password you will use to log in to the webui. Since this file is readable for other users it is recommended that you use a different password then you use in other places.

```
data = /home/user/downloads/
```
Here you have to set the path to your downloads/data directory, the contents of this directory will be listed in the webui and will be selectable for uploading.

```
datasort = latest
```
In the webui you can choose to sort by latest or alphabetically, here you can set the default option which will be used when you load the webui. Possible values are latest or alphabetically. If this setting does not exists or is empty it will be taken from the `settings.php` file.

```
dataorder = desc
```
In the webui you can choose to order by ascending or descending, here you can set the default option which will be used when you load the webui. Possible values are asc or desc. If this setting does not exists or is empty it will be taken from the `settings.php` file.

```
theme = dark
```
Here you can set the theme/stylesheet being used. By default there are only light and dark to choose from, however if another stylesheet is available in the webui directory you can also use that. This should be the name of the .css file without the .css extension. If this setting does not exists or is empty it will be taken from the `settings.php` file.

```
sizes = 1
```
Here you can set whether the size of the directory will be shown when you hover over the release name (i.e. Release - 1.37 GiB). Set this to 1 to enable it by default or to 0 to disable it by default. If this setting does not exists or is empty it will be taken from the `settings.php` file.

```
debug = 0
```
If you set this option to 1 the upload command will not be executed but it will be printed at the top of the page. This can be used to check if the command is correct. If this setting does not exists or is empty it will be taken from the `settings.php` file.

```
sites = AO, TV
```
Here you can choose which sites you want to show in the site dropdown (provided available in the sites array in the `settings.php` file), if left empty it will show all available sites.

```
sitesort = 1
```
If you set this option to 1 it will sort the sites in the dropdown alphabetically, if set to 0 it will use the order they have in the `settings.php` file.

```
catsort = 1
```
If you set this option to 1 it will sort the categories in the dropdown alphabetically, if set to 0 it will use the order they have in the `settings.php` file.