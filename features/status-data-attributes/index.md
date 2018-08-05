---
title: Data-* attributes on statuses and notifications for custom CSS targeting
---

`glitch-soc` adds the following HTML attributes to all statuses, boosts and favourites:

- `data-status-by="@alice@example.com"`
- `data-boosted-by="@bob@example.com"`
- `data-favourited-by="@charlie@example.com"`

The domain part is left out for users on the same server (eg. `@eve@example.com` will be just
`@eve` for `example.com` users).

Those attributes can be used for writing custom CSS via UserStyle. To use UserStyle, you need
a browser extension/add-on, such as Stylish:

- [Stylus for Firefox][StyFF]
- [Stylus for Chrome][StyGC]

### Example styles

**Changing user avatars**

Have you ever unfollowed or muted a user just because of their HORRIBLE avatar? No more!
Now you can replace them with any image of your choosing with a style like this:

```css
[data-status-by="@alice@example.com"] .account__avatar,
[data-favourited-by="@alice@example.com"] .account__avatar-overlay-overlay,
[data-boosted-by="@alice@example.com"] .account__avatar-overlay-overlay {
    background-image: url(______) !important;
}
```

`.account__avatar` is the regular full-sized avatar, whereas `.account__avatar-overlay-overlay` is the
tiny avatar overlay in boosts or favourites.

We may add a better way to do avatar replacement in the future, but for now this is the way to go.

**Hiding boosts by a user**

With this, you can hide boosts by any user you follow or see in the timelines. The `:not()` piece
is to stop it from hiding notifications about that user boosting your own toots.

```css
[data-boosted-by="@alice@example.com"]:not([data-status-by="@YourName"]) {
	display: none !important;
}
```

There are sure to be other fun uses for those data attributes, let us know if you find anything worth
sharing so we can add it here!

[StyFF]: https://addons.mozilla.org/en-US/firefox/addon/styl-us/
[StyGC]: https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne
