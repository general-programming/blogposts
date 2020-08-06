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

So, spurred by the promise of innovation, I propose...

## The Simple Fix: Literally just add a button

Why does this have to be an automatic process? All Patreon needs to do is add a button to the
creator page which says "Join the Discord server", and then trigger the exact same
flow that they use anyway - joining the server using Discord's 'Add Guild Member' endpoint.

It can just be as simple as this (fake mockup) example:

![An edited example with Hbomb's patreon](https://i.witch.press/TtwaB6As.png)

This way, you can choose to join and leave servers at your leisure; none of this
auto-joining business.

Actually, under the current automatic system, can you even manually rejoin a server
if you leave? Or do you have to wait until the next payment cycle?

## Musing on alternatives

Patreon's integration requires adding a bot to your server and giving it the "Create Instant Invite"
permission, to allow them to use Discord's 'Add Guild Member' endpoint:

[![Screenshot of Discord Developer Docs](https://i.witch.press/B345RPxM.png)](https://discord.com/developers/docs/resources/guild#add-guild-member)

Using this endpoint honestly makes a lot of sense, because it means the server controls
all the state, but there is an alternative: creating an invite.

[![Screenshot of Discord Developer Docs](https://i.witch.press/3BvSNXL5.png)](https://discord.com/developers/docs/resources/channel#create-channel-invite)

You could generate a temporary invite on-request and give it to the user. Presumably the
`target_user` parameter also locks that invite to a specific user (which would be essential!),
but the documentation is incredibly unclear on what this parameter does. The only `target_user_type`
is `STREAM` with a value of 1, but it's also unclear what this means. Either way, I
think it makes more sense to use the Add Guild Member interface rather than
this.

## Wrapping up

It's baffling to me that the integration is this bad - given that they give
creators the option to place a "Includes Discord rewards" banner on their pledge
tiers. Clearly they don't mind placing another company's logo quite visibly on
creator pages, so why didn't they spend any more time implementing this feature?

If you're interested more in Patreon's design and business failings, I'd suggest
reading [Plaidophile's write up on why they stopped using Patreon](https://beesbuzz.biz/blog/3222-In-which-I-finally-stop-using-Patreon).
