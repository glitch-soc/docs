---
title: Themes
---

Upstream Mastodon supports changing the site CSS on a per-user basis by specifying files in a special `config/themes.yml` file.
Glitch themes work a little differently:

1.  Glitch themes can include JavaScript and other resources, not just (S)CSS.
    They are built using the same pack system used by Webpack for Mastodon's vanilla assets.

2.  Glitch themes are designed to be incredibly easy to install, at the cost of being a little more difficult to create.
    In particular, installing a glitch theme is as simple as dragging/cloning a folder into `app/javascript/themes`, which means glitch themes work well with technologies like git submodules.

Glitch themes are presented to users in exactly the same fashion as upstream themes.
For information on creating a theme, read below.

###  Theme structure

Glitch themes are specified by folders inside of the `app/javascript/themes` directory.
The theme name inherits from the name of the folder.
Each theme folder must contain at least a `theme.yml` file, which is described further below.
Themes may also contain any number of other files; the organization of content inside of the theme folder is left entirely up to authors.

###  A basic CSS theme

The most basic glitch theme will have a `theme.yml` file that looks something like the following:

```yml
pack:
  common:
    filename: index.js
    stylesheet: true

fallback: glitch
```

The `pack` property specifies the pack files for the theme.
In our example, we specified a `common` pack file, with a filename of `index.js`, which contains a stylesheet.
The common pack is where glitch and vanilla Mastodon store all of their styling.
By specifying an alternate pack, we serve our styling instead.

The `fallback` property gives a theme which should be used for any unspecified pack files.
In our case, we want to use `glitch` packs to serve our various javascripts.

Our `index.js` file will look something like this:

```js
//  These lines are the same as in glitch:
import 'font-awesome/css/font-awesome.css';
require.context('../../images/', true);

//  …But we want to use our own styles instead.
import './myTheme.scss';
```

And, finally, our `myTheme.scss` might look like the following:

```scss
//  Variable declarations

//  …… ……
//  …… ……

import 'themes/glitch/styles/index.scss';

//  Styling declarations

//  …… ……
//  …… ……
```

We import the glitch styles inside of our theme SCSS and then add our own afterwards to override them.
All relative paths are resolved relative to the `app/javascript` directory, so you don't need to worry about getting the right number of `..`s in your import declarations.

###  Supplying other packs

Of course, you can overwrite other packs than just `common`.
The packs which are currently used by glitch are as follows:

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

These are specified as properties on the `pack` object.
The values for each pack property must be one of the following:

- If the property is not specified, then the fallback pack will be used, if applicable.
- If the property is specified but is `null`, then no pack will be used.
- If the property is specified but is a string, then this is interpreted as the pack's filename, and the default options are used.
- Otherwise, the property must be an object specifying options for the pack.

###  Pack options

The following options can be provided to packs:

- __`filename`:__ The filename of the pack. Must be specified for a pack to be loaded.
- __`preload`:__ An array of scripts to preload when rendering the pack, for use with async components. By default, no files are preloaded.
- __`stylesheet`:__ If `true`, this pack contains a stylesheet. Must be specified for styles to be loaded. Defaults to `false`.
- __`use_common`:__ Unless this property is `false`, the `common` pack will also be loaded. Defaults to `true`.

###  Fallbacks

The `fallback` property specifies a theme or themes from which to draw unspecified packs.
By default, unspecified packs are drawn from the default theme.
The value of this property can be either the name of a theme, or an array of names, in which case the first present theme will be used.
Setting this property to `null` disables fallback behaviour.

###  Pack directory

Generally speaking, your pack files should be inside of your theme folder.
If for some reason they aren't (as is the case with the `vanilla` theme, to maintain upstream compatibility), you can specify a different folder inside which to look for packs with the `pack_directory` property.
This should have a string value, and is resolved relative to the application root, *not* `app/javascript`.
