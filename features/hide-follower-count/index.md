---
title: Hiding follower count
---

In `glitch-soc`, it is possible to hide followers counts, either instance-wide
as an admin, or as a user setting.

### Hiding followers count as an admin

As an instance administrator, you can hide followers count for the whole instance,
by enabling the corresponding option in Site settings.

![Screenshot of the server-wide “Hide followers count” option](site-settings.png)

In doing so, the client API will return `-1` instead of the actual count for every
request, for both local and remote accounts, which, in glitch-soc flavor, will
result in displaying “-” instead of the actual count:

![Screenshot of user statistics with hidden followers count](hidden-count.png)

Furthermore, it will not export followers count over ActivityPub for any local user.

### Hiding followers count as a user

If the instance has not opted to hide followers count instance-wide, you can still
opt in to hide your own followers count from “Preferences > Other” settings.

![Screenshot of user-wide “Hide followers count” option](user-settings.png)

This will hide your own followers count from the client API and ActivityPub, but
it will still display other people's followers count.
