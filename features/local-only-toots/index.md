---
title: Local-only toots
---

##  Local-only toots  ##

`glitch-soc` adds a feature called "local-only" or "non-federated" toots. Toots marked as such do not automatically federate to other instances, making them ideal for example for local server announcements and meta-discussion. Currently, local-only toots may still federate in certain circumstances, described below.

### Compose UI

A toot is marked as local-only using a dropdown in the compose UI:

![compose](compose.png)

Additionally, this can be done by appending the eye (:eye:) emoji at the very end of the toot.

In the timeline, it then looks like this:

![ltl](in-timeline.png)

### Local-only toots may still federate

Although a Mastodon instance running `glitch-soc` will not automatically publish local-only toots to the poster's followers on other instances or to public timelines on other instances, the toots can still be retrieved by other instances in certain cases, which may result in them appearing in the Home timelines of the poster's followers on the retrieving instance as well as, for public posts, in the Federated Timeline of the retrieving instance. This will happen in the following cases, and may happen in some other situations:

1. If a user on another instance searches for a local-only toot by URL, their instance will retrieve the toot.
2. If a reply to a local-only toot federates to an instance, the receiving instance may retrieve the replied-to local-only toot.
