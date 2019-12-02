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
- [efdn.club](https://efdn.club)
- [falafel.clic2000.net](https://falafel.clic2000.fr)
- [glaceon.social](https://glaceon.social)
- [hackers.town](https://hackers.town)
- [im-in.space](https://im-in.space)
- [imaginair.es](https://imaginair.es)
- [monsterpit.net](https://monsterpit.net)
- [muensterland.social](https://muensterland.social)
- [ostatus.lardbucket.org](https://ostatus.lardbucket.org/)
- [playvicious.social](https://playvicious.social)
- [scifi.fyi](https://scifi.fyi/)
- [sdfn-01.ninjawedding.org](https://sdfn-01.ninjawedding.org/)
- [soc.ialis.me](https://soc.ialis.me)
- [social.dev-wiki.de](https://social.dev-wiki.de)
- [social.wxcafe.net](https://social.wxcafe.net)
- [sprite.land](https://sprite.land)
- [toot-lab.reclaim.technology](https://toot-lab.reclaim.technology/)


>   (Instance not on the list? Let us know!)
>
>   (The contents, availability, or behavior of the listed instances are not actively monitored. If you think any of this instances goes against our [Code of Conduct](https://github.com/glitch-soc/mastodon/blob/master/CODE_OF_CONDUCT.md), you are encouraged to report it to the project team)

###  What's different?

`glitch-soc` adds a number of experimental features to Mastodon, such as:

- [Media improvements](./features/media/)<br>
  - Images inside the CW spoiler
  - fullwidth images
  - scaling options
- [Reply selection in lists](./features/list-show-replies-to/)
- [Filter improvements](./features/filter-improvements/)
- [Highlighting of misleading links](./features/misleading-link-highlighting/)
- [An app settings modal](./features/app-settings/)
- [Collapsible toots](./features/collapsible-toots/)
- [Toot visibility icons](./features/visibility-icons/)
- [Local-only toots](./features/local-only-toots/)
- [Threaded mode](./features/threaded-mode/)
- [`data-*` attributes on statuses](./features/status-data-attributes/) for custom CSS targeting
- [Advanced theming via flavours+skins](./features/themes/)
- [Doodle](./features/doodle/)

### Features that have made their way upstream

Some of the features originally implemented in glitch-soc have been adopted in
Mastodon:

- [Optional boost hiding](./upstreamed-features/optional-boost-hiding/)
- [Optional notification muting](./upstreamed-features/optional-notification-muting/)
- [Custom profile metadata](./upstreamed-features/profile-metadata/)
- [Bookmarks](./upstreamed-features/bookmarks/)

### How to install and update `glitch-soc`?

`glitch-soc` is based on Mastodon's master branch. The installation steps are thus
the same as [described in the Mastodon documentation](https://docs.joinmastodon.org/administration/installation/).

Updating from Mastodon (or from an earlier `glitch-soc` version) is exactly like updating from one Mastodon version
to another, and will in general require the following steps:

0. Switch to glitch-soc, for instance by:
    - adding a new remote `git remote add glitch-soc https://github.com/glitch-soc/mastodon`
    - fetching it (`git fetch glitch-soc`)
    - switching to the `master` branch from that repo (`git checkout glitch-soc/master`)   
1. Fetch the source code (typically, `git pull`)
2. Install dependencies: `bundle install && yarn install`
3. Run the pre-deployment database migrations: `RAILS_ENV=production SKIP_POST_DEPLOYMENT_MIGRATIONS=true bundle exec rails db:migrate`
4. Pre-compile static assets: `RAILS_ENV=production bundle exec rails assets:precompile`

   Due to glitch-soc shipping with two front-end flavours, this step requires more resources than it does on mainline Mastodon.
5. Restart the services: `systemctl reload mastodon-web && systemctl restart mastodon-{sidekiq,streaming}`
6. Clean Rails' cache: `RAILS_ENV=production bin/tootctl cache clear`
7. Run the post-deployment database migrations: `RAILS_ENV=production bundle exec rails db:migrate`

### How to migrate back to upstream Mastodon?

Should you wish to migrate back to upstream Mastodon for any reason, this is possible, at the cost of
every glitch-specific feature, of course. There are a few things that you need to be aware of:
- Toots written in HTML or Markdown will not render as such anymore and will display the raw source instead.
- Local-only toots will not be local-only anymore, remote instances and users will be able to see them and
  interact with them, should they be mentionned in any way.
- If you have migrated to glitch-soc before Mastodon implemented bookmarks, migrations from Mastodon's source
  code will fail to execute until you edit `db/migrate/20180831171112_create_bookmarks.rb` to remove
  everything between `def change` and the corresponding `end`.

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
