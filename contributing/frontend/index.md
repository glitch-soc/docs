---
title : Contributing to the Frontend
---

>   Hey there!
>   Glad you're interested in helping us with this project.
>   Below are some guidelines and important things to note when contributing to the `glitch-soc` frontend (the "web view" app).
>   If you have any questions, don't be afraid to reach out!!
>
>   <footer>With love,<br>:heart: <a href="https://glitch.social/@kibi">kibigo!</a></footer>

Mastodon's frontend is developed with [React](https://facebook.github.io/react/) and [Redux](http://redux.js.org/) and served using [Webpack](https://webpack.js.org/).
Depending on what you're hoping to work on, you can get by without understanding the specifics of Redux or Webpack but knowledge of React is a must.
That said, React isn't too difficult to pick up and they have some very nice reference materials on their website :woman_technologist:.

Mastodon runs its code through a linter to make sure it maintains some semblance of order and consistency, and you should run these tests before you push.
You can use `npm test` to do this; on Vagrant, that's `vagrant ssh -c "cd /vagrant && npm test"` (assuming you have already called `vagrant up`).

In general, it's best if you have a development environment so that you can test your code, and you should reach out to someone on the `glitch-soc` development team if you need help setting that up.

###  Basic guidelines

Mastodon uses :v: two (2) spaces for indentation everywhere.

In JavaScript files, variable names are usually `camelCased`, except in the case of global constants, which are often in `SCREAMING_SNAKE_CAPS`.
JSX components are naturally `PascalCased`, as JSX requires a leading capital letter.

With regard to HTML `class` names, everything is lowercase and components are typically separated with a double-underscore, with hyphens betwen words.
For example, `.status__header-button__smile` would describe the "smile" component inside of the "header button" component inside of "status".
`class` names are kinda arbitrary so don't worry about it too much lol.

Try to make sure every file ends in a blank line to keep Git happy :kissing_heart:.
Also try to make sure lines don't have trailing spaces to keep things clean.
Many editors have plugins that will do this for you.

There are a few other rules that you'll notice when linting because they'll throw errors; for example, curly braces need whitespace around them and list items should terminate in a comma when they're on their own line (even if they're the last item).
You'll pick these up as you go along and just try to make everything look consistent.

###  Long lines

Generally, I like to avoid long lines.
It's possible to go too far with this (and I probably have in places :sweat_smile:) but just try to keep things looking nice.
It's less of a big deal with code, but with documentation especially you should make an effort to keep it readable.

I tend to wrap lines after 71 characters (such that the terminal `LF` is № 72) if anyone is wondering.
I think upstream development favours a number closer to 80.

###  Components and structure

All of the frontend assets which Mastodon uses are stored in the `app/javascript/` folder.
There are a few places of interest here:

####  :file_folder: The `mastodon` folder

The `mastodon` folder contains components from upstream (vanilla) Mastodon.
These components might have some glitch modifications, but if so they should be kept small.
__Not all of these files are used :scream:.__
In certain cases, we have replaced Mastodon's vanilla components with our own.

You'll find a number of subfolders inside the `mastodon` folder with various scripts and components.
This folder follows the same basic structure as our own `glitch` folder (see below), but ours is better-organized.

####  :file_folder: The `glitch` folder

The `glitch` folder contains our custom in-house components.
You can change these files as much as you want, since they will never conflict with anything upstream.
If you're creating a new file to add to the frontend, you should create it here.

Inside the `glitch` folder, there are the following subfolders:

 -  <dfn>`actions`</dfn>:
    These are Redux action scripts.

 -  <dfn>`components`</dfn>:
    These are all of the React components.
    The components in this folder __must not__ have direct access to the Redux store, with the exception of files with the name `container`, which __must not__ have render methods of their own.

    Components should be placed into one or more subfolders according to where they appear.
    The name of the component should reflect this structure; for example the component at `components/status/gallery/item` is named `StatusGalleryItem`.

    Ideally, each file should contain (and export) only a single component.

 -  <dfn>`locales`</dfn>:
    Here live Glitchsoc custom translations and overrides to the original mastodon messages.
    We decided to split this off from `mastodon/locales` to avoid merge conflicts.
    We have adjusted the locale script, so messages in `glitch/locales` are added to, and replace if needed, messages with matching keys from `mastodon/locales`.

    **Please try to avoid modifying the original files** (eg. by running `yarn manage:translations` and commiting the
    changes).
    Don't worry about `defaultMessages.json`, it's presently not used for anything—all the important stuff
    goes in `en.json` (or other languages, if you like).

 -  <dfn>`reducers`</dfn>:
    These are Redux reducers, to complement the actions provided by the `actions` folder.

 -  <dfn>`util`</dfn>:
    These are generic scripts which do not fit into any of the categories above.

####  :file_folder: The `styles` folder

The `styles` folder contains all of Mastodon's styles, for both the frontend application and its static pages.
98% of the time the only file you'll be interested in here is `components.scss`.
It's incredibly disorganized but try to make do :bowing_woman:.

###  Documentation

With respect to files in the `mastodon` or `styles` folder, try to document your code, but keep things somewhat minimal so that we don't have conflicts with upstream.
With files in the `glitch` folder, document everything liberally.
I favour Markdown syntax inside of block comments, personally.
If you feel up to it, include a Fediverse username by your code so that people know who to contact if they have any questions :information_desk_person:.

I am of the opinion that someone should be able to figure out more-or-less everything a file does just by reading the comments (ie, without understanding a line of code), and this will make it much easier for others who come along to do [`glitch-soc/docs`](https://github.com/glitch-soc/docs/) documentation work, who might not be fluent programmers.

Open-source is only open to those people who can read the source, and having a well-commented codebase greatly improves accessibility and helps users stay informed about what the application is doing behind their back :100::fire::ok_hand:.

 - - -

<footer>
    Happy coding, and thanks for helping out!<br>
    <strong style="text-decoration: none; font-size: 1.2em; line-height: 1.125;">:heart: kibigo!</strong><br>
    <small><a href="https://glitch.social/@kibi">@kibi@glitch.social</a></small>
</footer>
