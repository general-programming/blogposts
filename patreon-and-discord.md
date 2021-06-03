---
title: Patreon's Discord integration is bad and Patreon should feel bad
author: obw
discord: 97707213690249216
date: 2020-08-06
---

I recently started supporting a few people on Patreon. The experience overall
has been... not that great; the UI is slow and bloated, and the search feature
isn't very good (and I really remember it not existing for a little bit, but hey).

One of the creators I support offers access to a Discord server as a reward, so I
hooked up my Discord account, noting the scopes Patreon asks for (access your identity,
know what servers you're in, and join servers) and promptly discovered that Patreon
just auto-joins you to all available Discord servers with no prompting.

It was at roughly this point that I went "uhh... hmm", and a day or two later I
saw [a toot](https://cybre.space/@iliana/104595153489682886) from [iliana](https://linuxwit.ch)
noting that it happens *upon each payment cycle*, and there's no way to avoid it - you will be
force-joined to every server available to you.

This seems a little bizzare to me - surely you should be able to choose which servers
to join. So, in the interest of sharing ideas freely, or something, I propose...

## The Simple Fix: Literally just add a button

Why does this have to be an automatic process? All Patreon needs to do is add a button to the
creator page which says "Join the Discord server", and then trigger the exact same
flow that they use anyway - joining the server using Discord's 'Add Guild Member' endpoint.

It can just be as simple as this (fake mockup) example:

![An edited example with Hbomb's patreon](https://i.witch.press/TtwaB6As.png)

This way, you can choose to join and leave servers at your leisure; none of this
auto-joining business. The flow is barely different from the automatic system;
all Patreon has to do is add a new endpoint.

Actually, as an aside: under the current automatic system, can you even manually
rejoin a server if you leave?
Or do you have to wait until the next payment cycle?

## Some technical bits

Patreon's integration requires adding a bot to your server and giving it the "Create Instant Invite"
permission, to allow them to use Discord's 'Add Guild Member' endpoint:

[![Screenshot of Discord Developer Docs](https://i.witch.press/B345RPxM.png)](https://discord.com/developers/docs/resources/guild#add-guild-member)

So this endpoint is currently just called automatically for every patron upon
every payment cycle. It should not be particularly difficult to put this behind
a button instead.

## Wrapping up

It's baffling to me that the integration is this bad - given that Patreon gives
creators the option to place a "Includes Discord rewards" banner on their pledge
tiers. Clearly Patreon doesn't mind placing another company's logo quite visibly on
creator pages, so why didn't they spend any more time implementing this feature?

If you're interested more in Patreon's design and business failings, I'd suggest
reading [Plaidophile's write up on why they stopped using Patreon](https://beesbuzz.biz/blog/3222-In-which-I-finally-stop-using-Patreon).

*EDIT 2021-06-03: Removed some bits about invites that proved outdated, and made that section better*
