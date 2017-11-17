---
title : Introduction
...

Welcome to the documentation site for `glitch-soc`!
`glitch-soc` is a friendly [fork][] of the open-source social media software [Mastodon][], with the aim of providing additional features at the risk of potentially less stable software.
You can browse our source code and contribute to the project [on Github][glitch-soc].

###  Who is running `glitch-soc`?

`glitch-soc` is currently in use on the following instances:

 - [dev.glitch.social](https://dev.glitch.social/)
 - [toot-lab.reclaim.technology](https://toot-lab.reclaim.technology/)
 - [sdfn-01.ninjawedding.org](https://sdfn-01.ninjawedding.org/)
 - [ostatus.lardbucket.org](https://ostatus.lardbucket.org/)
 - [scifi.fyi](https://scifi.fyi/)
 
>   (Instance not on the list? Let us know!)

###  What's different?

`glitch-soc` adds a number of experimental features to Mastodon, such as:

 -  [Media improvements](./features/media/)<br>
    - Images inside the CW spoiler
    - fullwidth images
    - scaling options
 -  [An app settings modal](./features/app-settings/) 
 -  [Collapsible toots](./features/collapsible-toots/)
 -  [Toot visibility icons](./features/visibility-icons/)
 -  [Local-only toots](./features/local-only-toots/)
 -  [Custom profile metadata](./features/profile-metadata/)
 -  [`data-*` attributes on statuses](./features/status-data-attributes/) for custom CSS targeting
 - [Optional notification muting](./features/optional-notification-muting/)
 - [Optional boost hiding](./features/optional-boost-hiding/)

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
