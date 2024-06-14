# Zap Trails: A Silver Bullet to Content Curation/Discovery and Neutering Spam

# A Basic Zap Trail Algorithm

How do we show a new user content that is not only good and not spam, but relevant and fresh?

Start with a social media platform with things like notes and zaps, where:
* zaps are cheap/free to execute
* zapping for good content is already in practice by some users
* zapping can reference specific pieces of content
* this zapping history is (at least mostly) public knowledge

I'm new to Nostr, but it seems Nostr checks these boxes.

Assume no prior knowledge of the network, aside from a single account the user trusts which has some nonzero zapping activity - perhaps a friend or well-known public figure. Ask the user to specify this account. Let's call this trusted account AlexJones.

Choose a time window we want to focus on. Let's say a week.

Look at all the zaps sent by AlexJones in the last week. From this build:
* C1: a list of all the piece of content referenced by the zaps, ordered by zap size
* A1: a weighted list of the authors of this content, where the weight of each account in the list is proportional to the total in zaps they received

In our example, C1 and A1 might look like this:

(replace with pie chart, with content on the inner circle, and authors on the outer circle)
* 90%: InfoWars
* 6%: JoeRogan
* 4%: ObamaYoMama

Populate the user's feed C1, showing bigger zaps first. Nothing too special yet; at this point we're just reading zaps as boost/reposts with variable weight.

But now, we repeat the move, looking at zaps originating from A1 instead of AlexJones. Preserve the weight, such that i.e. 90% of both A2's and C2's weight would be made up of recipients of InfoWars' zaps, since 90% of AlexJones' zaps went to InfoWars.

(another pie chart)

Again, populate the user's feed primarily with the content zapped, C2. Note that instead of ordering by raw tip amount, these would be ordered by the inherited weight. (explain further using above pie chart).

Repeat the process to find L3, L4, etc. Each iteration follows zaps outward into more of the network, as seen from the perspective of AlexJones. Or more to the point, as *valued* from the perspective of AlexJones (and thus vicariously by our user).

Now encourage the user to send some zaps for content they like, and instead build L1 from the zaps the *user* has sent, rather than AlexJones. Each time the user zaps, L1 becomes more diverse, and this diversity trickles down to L2, L3, and so on.

Actually, we can now reframe that initial step of "endorsing" AlexJones with asking the user to zap any account any amount. This might more commonly be a friend than a celebrity. We can think of this as "seeding" their zap network. Before they zap, they see nothing; after a single zap, they see the network through that zap recipient's eyes; after every subsequent zap, their feed increases in diversity and becomes more their own.
# Spam, Zap Networks, and Pruning

Let's start talking in terms of Zap Networks. These are directed graphs, and you could imagine them fruitfully as a set of neurons (accounts) and synapses firing (zaps -pun appreciated!). Indeed, this metaphor could run quite deep - see the next section.

Even before introducing pruning tools, spam will have a hard time getting onto a feed built solely from zap networks. If I have only zapped only friends and talented artists, and they have only zapped content they in turn value, and so on, we can safely assume it will be several iterations into the above zap trail algorithm before spam shows up.

This is related to the fact there is no objective feed to hijack or buy your way into. The algorithm never looks at any central, global list of zaps (or upvotes, or follows) to determine what is "objectively good". Instead the algorithm cares only about a sort of organic web of trust (or web of value), with the user as the central, initial node. To get you to see spam, a spammer would have to find an account you've zapped, and somehow get that account to zap their content.

A spammer could of course zap his own content, from any number of accounts. But by itself this does nothing but create a solipsistic eddy of spammy content within the spammer's own set of accounts. No one would even have to go through the trouble of stepping around it - the zaps route around it as if it's not even there.

But maybe the spammer has actually accumulated some trust in the network in the way of zaps to him, and wants to now leverage that to get his spam some attention?

Let's introduce, then, the idea of pruning.

Say you see something on your feed about selling some supplements. Ah! Spam! Clutching your attention-pearls closely, you look at the provenance, so to speak, of the content. What chain of zaps led to this content showing up on your account? Maybe you see: you -> AlexJones -> InfoWars -> LifeStore. Ah yes - zapping AlexJones has come back to haunt us!

So you just blacklist AlexJones, pruning him from your zap network. By now you've built up a much more diverse and organic zap network anyway.

A whole tree of spam, just gone, banished forever, unless AlexJones can get someone else downstream your zap network to zap him. And if that happens, you can just prune the idiot that let him back in.

Further, these prune actions could be published and respected by zap trail algorithms. Then when you remove AlexJones, you're not just doing it for yourself - you're doing it knowing that this will clean up every feed *upstream* of your own - any feed whose user has zapped *you*.

And as a consequence, AlexJones didn't just lose your attention. He lost the attention of everyone who trusts you (or at least, the part of the attention that you were responsible for propagating upstream).

Now this is interesting, huh? The Zap Network as a whole begins to exhibit some higher-level behavior...
# Zap Network Cultivation and Evolution

Let's imagine the behavior of a Nostr community that only discovers content via the above zap trail algorithm as described, along with published prunes. For simplicity let's assume no other mechanisms are used (follows, likes, reposts, etc).

Any given user will be aware, intuitively, of their position as a node in this zap network, this directed graph, this neural net of sorts. Their zaps, sent outward, essentially pull content back to them through these pathways from "downstream" - and this content then travels further upstream, to anyone who has zapped the user. They know that they are not just modifying, and cultivating, their own feed, but that of the network, their audience.

Think of how this changes what it means to zap. It's no longer only a thank you and a financial reward; it's now a direct boost to the content's virality, propagating it further. A zap in this dynamic would be saying: "this content is good, I want you to have this money, and *people who trust me will now see it*". And the impact is proportional to the amount: a large zap would make the creator's reach spread further, because it would carry more "weight" upstream, thus appearing higher in feeds.

The same applies to pruning actions. Pruning is an intriguing third option aside from top-level censorship of a given topic or community, and free-for-all message boards where anyone can smear their shit up for anyone to see. The user is empowered to clean up *their* feed, *their* bit of the network - without imposing this subjective opinion on any part of the network that didn't already buy into the user's discernment.
# The Effect on Content

You sit down and spend a day creating a piece of art. Let's assume it's good. In fact let's assume it's *really good*.

You post it.

Your two friends who've sent zaps to you see it. Or perhaps you reach out in another channel, if you're really starting from zero trust, and ask for modest zaps. They agree to zap it (remember, it's good!). And because it's *really good*, the zaps will be large, relative to these friends' typical zaps.

Being relatively large zaps, they'll appear fairly high up in the nodes immediately upstream (those who have zapped your friends). They'll also appear higher upstream too right away, though with a diluted signal, and thus further down people's feeds.

But a few people who see it zap it themselves. With each zap, your content jumps up to a higher place on the feeds of those upstream of the zaps. You could imagine that the zaps are opening channels for the content to follow.

People keep liking it. People keep zapping it. Why?

* They want you to have the money.
* They want you to know they liked it.
* They want other people to see it.

Your content spreads. As it spreads, the amount you're receiving in zaps grows in proportional to the content.

Within this framework, content that spreads is content that people value, and it is also content that brings in revenue. Viral content brings in *a lot* of revenue.

Think of how this changes how it feels to post content. The game isn't exactly engagement anymore: it's value. The goal - both for content propagation and for the obvious benefit - is to get people to zap your content. I submit that this will purify content curation in a way analogous to how Bitcoin is posed to purify the economic system, and hope to demonstrate this soon.

What could you publish in such a paradigm, and make money on, in hours - even possibly minutes?

A well-written concise paragraph on a novel thought. A funny joke, a meme. A cool tip for using LLMs. A timely comment on recent events.

A nuanced view on an over-politicized topic, spreading through people who are equally tired of the tribal shit. A blueprint for a 3d printed widget among 3d printer enthusiasts. A piece of software. A song.

All, of course, completely outside of the game of copyrights and DRM.
# What Now?

I believe the above is a simple approach to content curation that
* Simplifies and empowers content curation in an elegant way that aligns with the principles of decentalized social networks
* Neuters spam
* Puts zaps center-stage, encouraging a massive uptake in zapping as a regular use of content consumption
* Can be adopted by any client fairly easily - i.e. the concept is not complex and the technical requirements are already met by Nostr itself
* Allows content creators to make money with mindblowing effectiveness and rapidity

So what's next?

Firstly, feedback. If you think I'm wrong about any of this, I'd like to know! This idea has been bouncing around my head for years. Maybe it's crazy! I don't know!

If the feedback is promising, I will approach OpenSats for research funding. If I can get this (or other) support, I'd first prove the concept quickly, perhaps with a minimalist POC, or by modifying some other client, or simply by manually performing the algorithm with well-known accounts and publishing the results.

With the concept proven - specifically, that by following zaps through the network we get very good content curation and avoid spam - the next step would be to design or modify a client such that it relies primarily on the above algorithm, puts zapping at center-stage in the UX, and supports pruning. With such a client, we'd prime the pump for those exciting second-order dynamics described in the last two sections, of a self-cultivating neural net of content, where content creators could make money overnight.
# Other Notes
Thank you for coming to my Ted Talk. Here are some other notes and ideas I'm also happy to discuss and hear responses on.
### C1/C2/C3... As Sections
When a user zaps content, it has the effect of essentially pinning it to their feed, because it comes to be in C1. Thus C1 would contain all the content the user has directly liked (within the time window we're working with).

C2 would contain all the content that came from "the next ring out", the content zapped by the accounts whose content the user has liked. C3 would be a further level "out" into the network.

It would makes sense to visually separate these sections, and while we're at it, put the user in charge of requesting the next iteration with a "load more"-like button.
### Other Algorithms
The algorithm mentioned above should really be thought of as a single instance of a family of algorithms. That algorithm basically asks: "where does my money go, and through what content?"

We could reverse the traversal direction, and instead follow zaps backward. Build a list of accounts who have zapped you, then find out who zapped them, and so on. Then you are asking "where does my money come from?" This is something like a shift from a focus on who your content creators are to who your *audience* is.

Or you could alternate between going forward and backward: who have you zapped? Call it A1. Who *else* has zapped A1? Call it A0. Now where do zaps from A0 go? You start to ask the question "What do people like me value?" Further iteration would broaden the definition of "people like me".
### Algorithms as Customizeable
Given the above, perhaps users could choose from a drop-down menu of such algorithms. Perhaps they could even modify or create their own.

Or we could even empower users to explore real-time, following sets of accounts around, so that we no longer talk of "iterating" over a fixed algorithm, but rather moves we can perform to move from one set of users/content to another.
### What does Alex Jones see?
We could also question the assumption that the algorithm must start always from the user. You could choose to "put on the glasses" of any user in the network. What do they see? Try on different algorithms while you're at it. Where do they get their zaps from?

What are the conservatives valuing? What about the Germans? What about a group of 3 people whose opinions you respect but which are generally quite different in how they call it?
### Zapping (and thus Bitcoin) is Required
For the above algorithm to work (at least naively, without any other content curation techniques), every new user needs some Bitcoin ready to be sent in a zap. Otherwise, their feed remains empty.

They could always operate in a sort of read-only mode, from the perspective of others. They could play around with other algorithms as described above. But to participate in the network dynamic, they'd need zaps.