---
title: "Encrypting Email"
date: 2013-11-30T18:29:43+02:00
last_edited: 2017-09-21T00:58:55+02:00
description: This article describes how and why to encrypt email. It contains my public key so you can exchange encrypted mail with me.
featured_image: /img/encrypting_mail.png
tags: ["email", "encryption", "gnupg", "gpg", "openpgp", "pgp"]
unlisted: true
---

## Introduction

Hi there! You are probably reading this because of one of the following options:

* You received an email from me and the signature contained a notice about encrypting email. You are interested in this and would like to find out more. Great! Just keep reading.
* You googled (other search engines are available) for information on encrypting email. Congrats! You found the right place. Just keep reading to learn more.
* You stumbled upon this page while browsing through my website and this article seemed interesting. Obviously, I advise you to keep reading as well. :)

No matter how you came across this page, you are here now and this page is likely to contain information relevant to you if you care about your privacy.

## Why would I encrypt email?

As you may have heard in the news recently, Edward Snowden has leaked information about intelligence services (like the NSA or the GCHQ)
spying on everyone of us. But it doesn't stop there. Companies (like Google, Yahoo or Microsoft) can also read your email, e.g. to use it
for personalized ads. And I haven't even mentioned hackers yet.  
This is possible due to the limitations underlying our email protocols. Back in the day, when "email" was designed, it wasn't intended to
be used on such a large scale as today. It was designed mainly for scientists to be able to share their discoveries. In many cases, early
SMTP servers were only accessible from within a specific organization. Therefore, not a lot of attention was put into security. A popular
example is the ability to set the `FROM` header to any email address (including of course ones from other people).<sup>[[1]](https://en.wikipedia.org/wiki/Email_spoofing)</sup>

Now, you may ask yourself: Well, there may be quite a few entities that _can_
potentially intercept my emails. But why would they choose _me_? Also, even if they did, I wouldn't care. If they really want to read those
"interesting" mails of mine, they are free to do so. I have nothing to hide…  
This is (unfortunately) how many people think. But however much I would like them to be right, they just aren't. Let me give you some examples
to think about.  
Do you really want literally _anyone_ to be able to read the private mails you sent to your friend? Do you want big companies to know _exactly_
what you do, like or think? Do you want these companies to sell this information to others, making **you** the product?  
It is an open secret that companies do make profiles of their users. We have known for many years that Google tracks the pages their users visit
and a lot more, claiming to only use this information to enhance the user's experience. But they aren't the only ones doing this. In fact, many
companies even admit to spying on their users in their terms of service (even though hidden inside of many pages of legal stuff).

## How do I actually encrypt my mails?

I hope by now I have convinced you and you agree that you should at least encrypt some of your mails. Now the question is how to actually do
this. Many people think it is a hard thing to do and requires a lot of knowledge about computers. However, in reality it is really easy to do.
There is just one thing to keep in mind: In order to be able to exchange encrypted mails with someone, both sides need to have a so-called public
and private key. Furthermore, they should, of course, both know how to read and send encrypted mails (which, again, is really simple).

While there are technically quite a few standards on email encryption out there, most of them are build upon PGP (Pretty Good Privacy). Almost
everyone uses a program called GnuPG (Gnu Privacy Guard) which is an Open Source implementation of the OpenPGP standard based on the original
PGP. By using this program, you will be able to exchange encrypted mails with virtually anyone who is also encrypting mails.

In this article, I am not going to go into how you actually set up GnuPG on your computer. This article is only intended to be a starting point.
I really recommend the "[Email Self-Defense](https://emailselfdefense.fsf.org/en/)" guide published by the Free Software Foundation (FSF). Here
are some other great links that will get you started with GnuPG:

* [Gpg4win (GnuPG for Windows) Documentation](https://gpg4win.org/doc/en/gpg4win-compendium.html)
* [How to get started using GnuPG on the Mac](https://gpgtools.tenderapp.com/kb/how-to/first-steps-where-do-i-start-where-do-i-begin-setup-gpgtools-create-a-new-key-your-first-encrypted-mail)
* [Using GnuPG on Ubuntu/Linux](https://help.ubuntu.com/community/GnuPrivacyGuardHowto)
* [Enigmail Quick Start Guide; Using GnuPG with Thunderbird](https://www.enigmail.net/documentation/enigmail-quickstart.pdf)

## Exchanging encrypted mail with me

If you are here because of the first reason I mentioned at the beginning of the article, this is probably what you care about the most.
I encourage anyone who wants to send me and email to encrypt (and sign) it. Here you will find my public key that is needed in order to do so.

You can download it right here: [https://benjamin-altpeter.de/00EB2372.asc](https://benjamin-altpeter.de/00EB2372.asc "My public key") As the
main reason of email encryption is to make sure that only the desired recipient (in this case me) can read an email, it is important that the
public key you downloaded is not compromised. For example, a hacker might gain access to this website and upload another key, therefore being
able to read the emails you encrypt for that key.

There are several ways of verify the integrity of my public key. One of them is just sending me an email. I will then provide you with further
information on how to prove you actually have the right way. ~~If you are looking for a quick and easy way and are willing to trust a third-party,
you can take a look at my [Keybase profile](https://keybase.io/baltpeter).~~

As a last thing, I would like to note that neither of these methods is entirely secure, either. If you really want to make sure you have my
key, you will, unfortunately, have to talk to me in person…

## Conclusion

As you see, encrypting mails is not a hard task, but it does most certainly provide a lot of value to you. Anyone who is concerned about their
privacy on the internet should look into that.

If you want to, please feel free to share this article with your friends and family to inform them about email encryption and start exchanging
encrypted email with them!
