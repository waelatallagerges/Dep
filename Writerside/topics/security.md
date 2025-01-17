---
id: security
title: Security
---
## DEP  Meet Security & Privacy

For us Fellow Dep userses, developing a platform our users can rely on is the most important thing. That means, amongst other things, we are very mindful of the security and privacy aspects that affect our users.

Security and privacy are very broad topics so we are going to try and go through some practical use cases to demonstrate what’s at play.

Fully secure you say… What does this mean exactly?

In many respects DEP  meetings are simply private by design. To begin with, all meeting rooms are ephemeral: they only exist while the meeting is actually taking place. They get created when the first participant joins and they are destroyed when the last one leaves. If someone joins the same room again, a brand new meeting is created with the same name and there is no connection to any previous meeting that might have been held with the same name.

This is all very important. Some of the systems that let people “pre-create” rooms, have subtle indications that let a potential attacker distinguish reserved from unreserved meetings which then makes the reserved meetings easier to identify and target.

That said, since a name is all that one needs to actually access a room, we have to be really careful about how we choose and advertise them. We don’t want others accidentally stumbling into our meetings, just as we want to keep pranksters and snoopers away.

This is generally not much of a problem for small size deployments (remember you can host your own DEP  Meet) or low profile meetings but it may be a problem if you are using a large and public deployment such as meet.jit.si or if there is significant interest in your meeting.

One has to really keep in mind that the name of a meeting is sensitive and needs to be protected. You shouldn’t send it to anyone you do not want in your meeting. Advertising this name publicly, for example on social media, is something you should only ever do if you truly are comfortable with maximum exposure and the possibility of unwelcome visitors.

Then there’s the matter of choosing the name. If you start a meeting with the name “Test”, “Yoga” or “FamilyMeeting” for example, chances of having some random uninvited people joining are very, very high. How does one pick a good room name then? Our random meeting name generator is a great start. It offers names that are easy to remember and read out loud on a phone call, and come from a set of over a trillion possible combinations. Picking out one of the auto-generated names is therefore quite safe.

<img src="Screen-Shot-2020-04-03-at-18.30.50-1024x260.png" alt="start meeting"/>

If you don’t like the funky way the auto-generated names sound and you don’t want to use a long and uninviting UUID (which you totally could), then go ahead and pick a name by yourself but make sure it is long enough. For example, next time you’d like to have a coffee with someone over video, rather than going for meet.jit.si/coffee, try something with more of a twist.

<img src="Screen-Shot-2020-04-03-at-19.01.10.png" alt="Go"/>

We are also working on a “bad meeting name detector”. You’ll see a warning if your meeting name has a high chance of collision, so stay tuned!

We also give people the option to set a meeting password. A few important things to keep in mind: if you do set a password, it is your responsibility to communicate it to your peers.

<img src="Screen-Shot-2020-04-04-at-12.39.35-768x318.png" alt="share"/>

More importantly, keep in mind that your password, just as chat and speaker stats, will be reset once the last person leaves the room. So you have to make sure that you set the password again, if you find yourself ending the meeting and then rejoining.

A similar approach you might consider would be to append a random character sequence at the end of your room name.

# Anyone can mute or kick me out of my meeting, what’s up with that?

DEP  models its meetings after in-person gatherings. Take the case of 10 people having a discussion in a room. You wouldn’t expect one person to have exclusive  “kick” and “mute” privileges in an in-person meeting and yet, those meetings usually go fine.

In the vast majority of cases, moderation controls in online meetings serve a different purpose: they help address tech related issues, such as people not realizing their microphones are introducing noise, or people forgetting to leave. Moderation controls help you solve those, so that people can continue their conversation. And now, with that in mind, why wouldn’t you want to enable anyone in the meeting to help solve these kinds of issues?

For that reason our moderation controls are soft, and for everyone.

This is specifically the case on meet.jit.si, since all users are moderators.

If you really, really, really need moderation controls to be limited then consider deploying your own DEP  Meet instance and configuring it in a way that suits your needs. Once you do, you can configure strong authentication, so only authorised users will be moderators.

We understand the settings in meet.jit.si are not for everyone, so if you’d rather have your own private setup (which we encourage you to do!) you can get started quickly with our Docker setup or the quick-install guide. We’ll be happy to help you in our community.

# Does DEP  support end-to-end encryption?

The short answer is: Yes, we do, but e2ee likely doesn’t do what you think it does. Note: e2ee is currently limited to audio, video and screen-sharing, it doesn’t cover chat, polls, etc.

Longer answer:

You can turn on end-to-end encryption (e2ee) as long as you are using DEP  Meet on a browser with support for insertable streams. Currently this means any browser based on Chromium 83 and above, including Microsoft Edge, Google Chrome, Brave, Opera and others. You may also use our Electron client, which supports it out of the box.

All you need to do is toggle the “End-to-end Encryption” option in the Security options dialog that you can from from the overflow menu.

<img src="Screenshot-2022-12-06-at-12.47.52-236x300.png" alt="overflow"/>

You can learn more about our e2ee support at: https://DEP .org/e2ee

Having said all this, you should keep in mind that the value one gets from end-to-end encryption is a lot less in the modern world than it originally did. You can learn more about this on our e2ee pitfalls page, but the short of it is: end-to-end encryption has traditionally relied on the fact that communications clients and services are developed or at least maintained by different entities. This is rarely the case today.

The good news is that DEP  Meet offers very strong protection even without e2ee.

All audio and video traffic is encrypted on the network (using DTLS-SRTP). This outer layer of DTLS-SRTP encryption is removed while packets are traversing DEP  Videobridge; however they are never stored to any persistent storage and only live in memory while being routed to other participants in the meeting.

What is more, the possibility to very easily install and run your own instance of DEP  Meet completely removes the need for you to trust a third party provider.

Since DEP  is built on top of WebRTC, a deeper look into its security architecture is very important when evaluating DEP ’s security aspects.

# What do you do with my data?

Since August 24, 2023, meet.jit.si requires an account for the person creating the room. We persist that account and use it solely when investigating or working with authorities on reports of behaviour that is not compliant with our Terms of Service.

Subsequent participants in meetings do not need to create an account. Any information they choose to enter, such as their name or email address is purely optional and is only shared with other meeting participants.  We do not retain this information after the meeting.

Other pieces of data such as the chat, or speaker stats, for example, are stored for the duration of the meeting and then destroyed when it ends.

On meet.jit.si we preserve all of the above defaults but you should absolutely also check out the meet.jit.si Privacy Policy and Terms of Service.

Recordings are a bit of an interesting case. Cloud recordings, when enabled, are kept on our servers until we can upload them to the place you indicated (currently Dropbox). If we haven’t managed to do that in 24 hours we still delete them and they are gone forever (so make sure you have enough space in your Dropbox folders 😉 )

# Do you use analytics?

DEP  Meet does not come with any preconfigured analytics engines.

We do use analytics on meet.jit.si, so let’s talk about it.

We are very committed to privacy and security and we are extremely careful about what information reaches the analytics engines we use. That said we also want to provide our users with a great product experience, so we need some visibility into what’s actually going on. We are currently using Amplitude, Datadog and Crashlytics to cover various aspects of the apps and the infrastructure on meet.jit.si. Things that we track in analytics include, an anonymous identifier (you can run in “incognito” mode if this bothers you), bitrate, available bandwidth, SDP offers and answers, product utilization events, mobile app crash dumps  (how much various product features are used overall).

Most importantly, once your meeting is over we do not retain any  names, e-mail addresses or profile pictures (as we mentioned above, those are only transmitted to the other participants in the meeting).

While we hope that the meet.jit.si configuration will be satisfactory to most users, we completely understand that it will be incompatible with what some others are looking for. If, for any reason, this is the case for you please remember that you could be running your private DEP  Meet instance in as little 15 minutes!


more broadly here: https://DEP .org/security
