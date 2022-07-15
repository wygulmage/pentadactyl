Pentadactyl for Pale Moon
=========================

This is a community-maintained fork of one of the best XUL-based
Firefox extensions, targeting [Pale Moon](https://www.palemoon.org/)
28.5+.

Binary Releases
---------------

* [GitHub Releases Page](https://github.com/pentadactyl/pentadactyl/releases)
* [Pale Moon Website](https://addons.palemoon.org/addon/pentadactyl-community/)

Building from Source
--------------------

### Build XPI from sources ###

``` shell
git clone --depth 1000 https://github.com/pentadactyl/pentadactyl.git
cd pentadactyl/
make -C pentadactyl xpi
```

This resulting XPI will be placed in the `downloads/` folder.

#### Build dependencies ####

  * zip
  * gmake
  * Standard POSIX commands: awk, echo, sed, sh

While most developers use a Unix-like operating system, you can also build Pentadactyl on Windows with the help of MinGW's MSYS, Cygwin, or SFU. 

### Install without XPI ###

As creating and installing a new XPI file after each update is cumbersome, most developers run Pentadactyl directly from their working copies. This is achieved with [Firefox extension proxy file][1], which is a plain text file named after the extension ID and its contents is just a path to the extension source directory.

Assuming you use the `default` profile, the following command will create the proxy file:

``` shell
cd /path/to/cloned/pentadactyl/
# On clean profile, ensure that 'extensions' directory exists inside of the profile directory.
echo "$(pwd)/pentadactyl" >~/'.moonchild productions/pale moon'/*.default/extensions/pentadactyl@addons.palemoon.org
```

Once you installed Pentadactyl via the proxy file, restart the browser. Afterwards, you can use `:rehash` command to reload the extension without further browser restarts. Moreover, you can bind it to a key chord in your `~/.pentadactylrc`:

``` viml
nmap -ex <C-r> :rehash
```

[1]: https://developer.mozilla.org/en-US/Add-ons/Setting_up_extension_development_environment#Firefox_extension_proxy_file


### Firefox extension proxy file [from dead link above]
Extension files are normally installed in the user profile. However, it is usually easier to place extension files in a temporary location, which also protects source files from accidental deletion. This section explains how to create a proxy file that points to an extension that is installed in a location other than the user profile.

1. Get the extension ID from the extension's install.rdf file.
2. Create a file in the "extensions" directory under your profile directory with the extension's ID as the file name (for example "your_profile_directory/extensions/{46D1B3C0-DB7A-4b1a-863A-6EE6F77ECB58}"). (How to find your profile directory) Alternatively, rather than using a GUID, create a unique ID using the format "name@yourdomain" (for example chromebug@mydomain.com) - then the proxy filename will be same as that ID, with no curly brackets {}.
3. The contents of this file should be the path to the directory that contains your install.rdf file, for example /full/path/to/yourExtension/ on Mac and Linux, and C:\full\path\to\yourExtension\ on Windows. Remember to include the closing slash and remove any trailing whitespace.
    * Note: If you already installed the extension via XPI, you should uninstall it first before creating the pointer file.
    * Also note that the use of proxy files requires that the extension's chrome.manifest defines its chrome urls using traditional directories, rather than a JARed structure. See below.
4. Place the file in the extensions folder of your profile and restart the application.
