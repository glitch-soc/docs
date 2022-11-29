---
title: Flavours and Skins
---

Upstream Mastodon supports changing the site CSS on a per-user basis by specifying files in a special `config/themes.yml` file.
This approach works for simple themes, but it has its limitations:

1.  You can only change the CSS of a page, not its JavaScript or other elements.
2.  The same theme is applied to all pages, regardless of type.

`glitch-soc` uses a flavour+skin system which addresses both of these problems, while making the creation of themes even simpler than it is on upstream.
The system works as follows:

1.  Each instance can have any number of _flavours_, which can contain JavaScript, CSS, or anything else.
    By default, `glitch-soc` comes with two flavours: `glitch`, which is the default, and `vanilla`, which is the frontend used by upstream.

2.  Each flavour can have any number of _skins_, which are alternate stylesheets used with the flavour.
    [The `win95` theme](https://github.com/cybrespace/mastodon/blob/cybrespace/app/javascript/styles/win95.scss) from `cybrespace:mastodon` is an example alternate skin for the `vanilla` flavour.

The flavour and skin of the Mastodon web app can be changed in the user preferences.
For details on creating and installing additional skins and flavours, see below.

###  Installing

To install an existing flavour or skin, you need only to place the flavour or skin file/folder into the appropriate location.
For flavours, this is:

    app/javascript/flavours/

For skins (where `FLAVOUR-NAME` is the name of the flavour that the skin applies to), this is:

    app/javascript/skins/FLAVOUR-NAME/

Mastodon will automatically detect flavours and skins installed into these locations, although you will likely have to restart your server (and, naturally, recompile your assets).
This system works well with installation methods such as git submodules, although of course you can simply add the files manually as well.

###  Skins

Glitch skins are automatically loaded from the folder `app/javascript/skins/FLAVOUR-NAME/`, where `FLAVOUR-NAME` is the name of the flavour that the skin should apply to.
For example, if you are looking to reskin the `glitch` flavour, you should place your skin in the file `app/javascript/skins/glitch/`.

The simplest skin is just a single (S)CSS file, the name of which will be taken as the name of the skin.
This stylesheet will be served instead of the `common` styles, which hold all of Mastodon's default styling.
When you specify a skin, the default styling for a flavour is *not* automatically loaded, so be sure to import it in your stylesheet if needed.

###  Packs

If you want to provide different stylesheets for various pages, you can do this by providing a folder instead of a single stylesheet as your skin.
This folder should contain a number of files, each of which provides the styling for a different _pack_, which is served depending on page type.
The available packs are as follows:

- __`about`:__ Rendered on the `about/` page (but *not* `about/more`, etc) and on hashtag pages; this pack provides the timeline component.
- __`admin`:__ Rendered on all admin pages.
- __`auth`:__ Rendered on auth pages.
- __`common`:__ Rendered on all pages, except those with the `use_common` property set to `false`.
- __`embed`:__ Rendered on embedded pages.
- __`error`:__ Rendered on error pages.
- __`home`:__ Rendered on the home page; ie, the Mastodon web view.
- __`modal`:__ Rendered on modal pages (ie, for remote follows).
- __`public`:__ Rendered on public pages, like static user profiles.
- __`settings`:__ Rendered on all settings pages.
- __`share`:__ Rendered on the "share" page; this pack provides a standalone composer.

The names of the files inside the skin folder should match the pack that they are meant to replace.
For example, if I have styling that I want to show on the web app but *not* on static pages, I should specify it in `app/javascript/skins/FLAVOUR-NAME/SKIN-NAME/home.scss`.

The `glitch` and `vanilla` flavours only use the `common` pack for styling, but you are welcome to add additional styles to other packs if you wish.

###  Flavours

Like skins, flavours are all loaded from a specific folder; namely, `app/javascript/flavours`.
Flavours are specified as folders with a special file, called `theme.yml`, which provides the necessarily metadata for Mastodon to load its files.
Aside from this one required file, the contents of a flavour folder are left entirely up to authors.

The `theme.yml` for a flavour **_must_** have a `pack` property, whose own properties specify the JavaScript files to load for each pack (see above).
These properties must have one of the following values:

- If the property is not specified, then the fallback pack will be used, if applicable.
- If the property is specified but is `null`, then no pack will be used.
- If the property is specified but is a string, then this is interpreted as the pack's filename, and the default options are used.
- Otherwise, the property must be an object specifying options for the pack.

Here is a sample `theme.yml` file that could be used to generate a flavour:

```yaml
pack:  #  Pack files
  common:  #  Options for the `common` pack
    filename: pack/common.js  #  This file contains all the scripts and styles for the pack
    stylesheet: true  #  This must be specified for packs which serve styling
  home: pack/home.js  #  A string can be used if only a filename is needed

fallback: glitch  #  The fallback flavour for any unspecified packs
```

###  Pack options

The following options can be provided to packs:

- __`filename`:__ The filename of the pack. Must be specified for a pack to be loaded.
- __`preload`:__ An array of scripts to preload when rendering the pack, for use with async components. By default, no files are preloaded.
- __`stylesheet`:__ If `true`, this pack contains a stylesheet. Must be specified for styles to be loaded. Defaults to `false`.
- __`use_common`:__ Unless this property is `false`, the `common` pack will also be loaded. Defaults to `true`.

###  Locales

The `locales` property specifies a folder from which to draw locale files to be served with your JavaScript.
The contents of this directory must be `.js` or `.json` files whose names correspond to language tags and whose default exports are a messages object of the same form as provided by vanilla Mastodon.
This messages object can be made accessible in your source by importing `getLocale()` from `locales`.

###  Screenshots

You can specify one or more screenshots to render in the flavour's description page using the `screenshot` property.
Webpack ignores the paths of image assets, so this property should specify *only* the filename.
It is a good idea to namespace the filename of this file using your flavour name to guarantee uniqueness.

The value of the `screenshot` property must be an image file that Webpack already knows about—we won't try to load it for you.
Requiring it somewhere in one of your JavaScript files is probably sufficient.

###  Fallbacks

The `fallback` property specifies a flavour or flavours from which to draw unspecified packs.
By default, unspecified packs are drawn from the default theme.
The value of this property can be either the name of a flavour, or an array of names, in which case the first present flavour will be used.
Setting this property to `null` disables fallback behaviour.

###  Pack directory

Generally speaking, your pack files should be inside of your flavour folder.
If for some reason they aren't (as is the case with the `vanilla` flavour, to maintain upstream compatibility), you can specify a different folder inside which to look for packs with the `pack_directory` property.
This should have a string value, and is resolved relative to the application root, *not* `app/javascript`.

###  Localization

You can provide localization strings for your skins and/or flavours by including a `names.yml` file inside the skin/flavour folder.
For themes, this file should take the following form:

```yml
en:
  flavours:
    FLAVOUR-NAME:
      description: [A description of your flavour]
      name: [Your flavour's name]
  skins:
    FLAVOUR-NAME:
      default: [The name of the default skin for your flavour]
# …more localizations for other languages
```

For skins, you only need the `skins` part of the above file:

```yml
en:
  skins:
    FLAVOUR-NAME:
      SKIN-NAME: [The name of your skin]
# …more localizations for other languages
```

This file is loaded alongside all of the other localization data when your server first starts.
