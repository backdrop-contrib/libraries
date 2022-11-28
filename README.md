Libraries API
=============

Libraries API provides external library handling for other Backdrop modules.

**NOTE:** If a module you're trying to use depends on Libraries API, please
suggest to the module maintainer that they update their module to either use core's
library functions, or bundle the library in their module.

In general, Libraries API shouldn't be needed on Backdrop sites, since 3rd party
libraries **should** be bundled into the modules that require them, where *licensing
permits*.

Javascript and CSS Libraries
----------------------------

If you're a module maintainer and currently depend on Libraries API for JS or CSS
libraries, where possible, please replace Libraries API-specific functions with
their Backdrop core equivalents:

`hook_libraries_info()` -> [`hook_library_info()`](https://api.backdropcms.org/api/backdrop/core%21modules%21system%21system.api.php/function/hook_library_info/1)
`hook_libraries_info_alter()` -> [`hook_library_info_alter()`](https://api.backdropcms.org/api/backdrop/core%21modules%21system%21system.api.php/function/hook_library_info_alter/1)
`libraries_load()` -> [`backdrop_add_library()`](https://api.backdropcms.org/api/backdrop/core%21includes%21common.inc/function/backdrop_add_library/1)
`libraries_info()` -> [`backdrop_get_library()`](https://api.backdropcms.org/api/backdrop/core%21includes%21common.inc/function/backdrop_get_library/1)

Note that this isn't simply a matter of renaming the functions. You will need to
rewrite some of your code. Check the API documentation for more information.

PHP Libraries
-------------

If the PHP library's license is compatible with GPL 2, then bundling the library
into your module is preferred. You can include the library in a sub-folder of the
module and call the functions from your code, or load classes using
`hook_autoload_info`.

Sharing libraries across modules
--------------------------------

If your module requires a 3rd party library that is already used and bundled by
another module, then your module should either depend on that other module, or
the 3rd party library should be split out of the "parent" module that it used to
ship with, and moved into a new contrib library-only module. This new separate
module will only be used to hold the library (implementing `hook_library_info()`
/`hook_library_info_alter()`). Then all other contrib modules that require the
3rd party library, should declare the library module as a dependency in their
.info files, using `dependencies[] = name_of_library_module`.

When licensing is not compatible with GPL
-----------------------------------------

This Libraries API module is still relevant for libraries which are not compatible
with the GPL, and cannot be included in the module and hosted alongside GPL code.

Installation
------------

- Install this module using the official Backdrop CMS instructions at
  <https://backdropcms.org/guide/modules>.

Current Maintainers
-------------------

- Looking for a maintainer...

Credits
-------

This module is a Backdrop port of Drupal's contributed module
'[Libraries](https://www.drupal.org/project/libraries)'.

- Ported to Backdrop CMS by [Graham Oliver](https://github.com/Graham-72).
- Originally written for Drupal by [Daniel Kudwien](https://www.drupal.org/u/sun).

License
-------

This project is GPL v2 software. See the LICENSE.txt file in this directory for
complete text.
