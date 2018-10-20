---
title : Introduction
...

Welcome to the documentation site for `glitch-soc`!
`glitch-soc` is a friendly [fork][] of the open-source social media software [Mastodon][], with the aim of providing additional features at the risk of potentially less stable software.
You can browse our source code and contribute to the project [on Github][glitch-soc].

###  Who is running `glitch-soc`?

`glitch-soc` is currently in use on the following instances:

- [aleph.land](https://aleph.land)
- [awoo.space](https://awoo.space)
- [chomp.life](https://chomp.life/)
- [crazynoisybizarre.town](https://crazynoisybizarre.town)
- [dev.glitch.social](https://dev.glitch.social/)
- [donphan.social](https://donphan.social)
- [glaceon.social](https://glaceon.social)
- [im-in.space](https://im-in.space)
- [imaginair.es](https://imaginair.es)
- [monsterpit.net](https://monsterpit.net)
- [ostatus.lardbucket.org](https://ostatus.lardbucket.org/)
- [playvicious.social](https://playvicious.social)
- [scifi.fyi](https://scifi.fyi/)
- [sdfn-01.ninjawedding.org](https://sdfn-01.ninjawedding.org/)
- [soc.ialis.me](https://soc.ialis.me)
- [social.wxcafe.net](https://social.wxcafe.net)
- [sprite.land](https://sprite.land)
- [toot-lab.reclaim.technology](https://toot-lab.reclaim.technology/)


>   (Instance not on the list? Let us know!)

###  What's different?

`glitch-soc` adds a number of experimental features to Mastodon, such as:

- [Media improvements](./features/media/)<br>
  - Images inside the CW spoiler
  - fullwidth images
  - scaling options
- [An app settings modal](./features/app-settings/)
- [Collapsible toots](./features/collapsible-toots/)
- [Toot visibility icons](./features/visibility-icons/)
- [Local-only toots](./features/local-only-toots/)
- [Threaded mode](./features/threaded-mode/)
- [`data-*` attributes on statuses](./features/status-data-attributes/) for custom CSS targeting
- [Advanced theming via flavours+skins](./features/themes/)
- [Bookmarks](./features/bookmarks/)
- [Doodle](./features/doodle/)

### Features that have made their way upstream

Some of the features originally implemented in glitch-soc have been adopted in
Mastodon:

- [Optional boost hiding](./upstreamed-features/optional-boost-hiding/)
- [Optional notification muting](./upstreamed-features/optional-notification-muting/)
- [Custom profile metadata](./upstreamed-features/profile-metadata/)

###  How can I help?

You can get information on contributing [here][Contributing].

###  Disclaimer

`glitch-soc` is beta software, and under active development.
Use at your own risk!

[Contributing]: ./contributing/
[Features]: ./features/
[fork]: https://en.wikipedia.org/wiki/Fork_(software_development)
[glitch-soc]: https://github.com/glitch-soc/mastodon/
[Mastodon]: https://joinmastodon.org/
