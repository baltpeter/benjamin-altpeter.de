---
title: "Scanning the web for ALL available French one-word domains"
date: 2014-10-25T20:51:00+02:00
last_edited: 2018-05-16T21:39:55+02:00
description: In this article I present an approach to generate a list of all available one-word domains in any language. Some filters (like word class) can be applied.
featured_image: /img/domainchecker.png
tags: ["all words", "availability", "domain", "french", "language", "nouns"]
---

A while ago, I set out for quite an ambitious project. I needed a list of _all_ domains containing just one French noun that are available as both `.com` and `.de`. The process seemed easy enough. Basically, I would have to

1. Get a list of all French words
2. Sort that list so it only contains nouns
3. For each noun, check if the `.de` and `.com` domains are available

As it turns out, the project is not too hard once you've found the right tools. So in this article, I am going to share my experiences and the method I used for everyone who is either interested in this process or just likes reading about fun projects.  
Just one more note before I start: Many of the scripts I used are not very nice and clean from a coding perspective, they are mainly quick-and-dirty implementations of what I needed. For my purposes, this was more than enough. Quite frankly, I don't care if the scripts used in this projects are nice and high-performance C++ applications or just quickly hacked together PHP scripts. They both do their jobs just fine and originally, I didn't intend to share them. But as I think this turned out to be quite an interesting project, I changed my mind. Enjoy! :)

## Getting a list of all French words

Of course, obtaining a list of all French (or whatever language you might be interested in) words is the most fundamental step. After searching around for a bit, I found that most UNIX-based distributions have a _/usr/share/dict_ directory that contains word lists. This also applies to my BSD-based Mac but, unfortunately, mine only had English word lists. And, even though, the accompanying _README_ file told me a French word list is also available, the mentioned FTP server apparently seems to be offline:

> Dictionaries for other languages, e.g. Afrikaans, American, Aussie, Chinese, Croatian, Czech, Danish, Dutch, Esperanto, Finnish, French, German, Hindi, Hungarian, Italian, Japanese, Latin, Norwegian, Polish, Russian, Spanish, Swahili, Swedish, Yiddish, are available at ftp://ftp.ox.ac.uk/pub/wordlists.

So, I had to look around a bit more to eventually stumble across the [_wfrench_ Debian package](https://packages.debian.org/wheezy/wfrench "wfrench Debian package"). Obviously, Linux distributions also come with wordlists and as opposed to my Mac, they luckily have a well-managed package system that allows everyone to download the packages and extract the wordlist as a nice plain text file.  
Note: These packages are of course also available for other languages. So, if you're looking for a German wordlist, for example, you can use the _wngerman_ package (a _wogerman_ package is also available but that one follows old spelling rules).

{{< img src="/img/french-wordlist.png" caption="French wordlist" >}}

## Extracting nouns from the wordlist

Now this step seems very hard as it's of course not easy for a computer to know word classes and you don't want to manually sort a list of several hundred thousand French words for nouns. Luckily, there is a tool called [TreeTagger](http://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/ "TreeTagger") that is able to tag sentences is a variety of languages (including French).

Using a [node.js wrapper](https://github.com/nyxtom/treetagger "TreeTagger node.js wrapper"), I wrote the following simple script that takes our wordlist and outputs all nouns in that list to the console:

```js
var Treetagger = require('treetagger');
var tagger = new Treetagger({ language: "french" });

var fs = require('fs'), filename = "french.txt";
fs.readFile(filename, 'utf8', function(err, data) {
    if(err) throw err;
    tagger.tag(data, function (err, results) {
        results.forEach(function(e) {
            if(e.pos == "NOM") {
                console.log(e.t);
            }
        });
  });
});
```

Now, all that was left to do was run the script and print the results to a text file: `node treetagger.js > french_nouns.txt`  
Three things to note on that one:

* The tagging of word classes is different for each language. In my example, I had to use _NOM_ but in English, you would have to use _NN_.
* Automatically doing the tagging is of course not going to be perfectly accurate. You will be missing some nouns while some non-nouns will also slip into your list. It is, however, safe to assume that the results are still going to be a lot better than if we were to manually tag the list.
* The script does not filter out inflected nouns, so e.g. you will have both _abjection_ and _abjections_ on your list.

## Checking for available domains

After all that work, we still have to do the main part: Check whether or not the nouns we've found are actually available for registration. While there are some domain availability APIs offered by domain registrars, you would generally use whois for that purpose. If you query a whois server for a domain that is not registered, you will get a response like that (note that the response is different depending on the server):

```bash
$ whois thisdomainisnotatallregistered.de
Domain: thisdomainisnotatallregistered.de
Status: free
```

This solution would be easy to implement in PHP via a socket connection, but there is one problem. As per our initial requirements, we said that the domain had to be available as `.de` and `.com`. While querying the `.com` whois server appears not to have a limit on the amount of queries in a certain time frame, _whois.denic.de_ most certainly has and that limit is unfortunately quite strict. Luckily, I stumbled across [freedomainapi.com](https://freedomainapi.com/ "freedomainapi.com"). They offer a free API that outputs JSON, so it is easy for us to query that from PHP. Here is the simple script I wrote:

{{< highlight php "startinline=true" >}}
function checkdomain($domain) {
    $api_req = file_get_contents('http://freedomainapi.com/?key=YOURAPIKEY&domain=' . $domain);
    $api_req = json_decode($api_req, true);
    return $api_req['available'] == 'true';
}
{{< / highlight >}}

The final thing left to do was to remove all accents etc. as I didn't want to query for IDNs. For that, I stole a function from WordPress. Conveniently, that function also works for languages other than French, so you can reuse my code more easily. The entire PHP script can be found [here](https://gist.github.com/baltpeter/192e5ed4649db1f72745 "PHP script to check our wordlist for domain availability").

I will have to add two notes on this one as well:

* This approach is _incredibly_ inefficient. Before querying the API (or whois server, whichever method you choose) you should at least run a DNS query. If that returns any results, you can be sure that the domain is registered and can discard it immediately.
* I have since found that some whois servers (like _whois.crsnic.net_ and _whois.nsiregistry.net_) seem to also respond for `.de` domains and not have a limit on the number of requests. Might be worth investigating as an alternative to the API.

And there you have it. That's all you need to get a list of all domains containing just a single French noun that are available as `.com` and `.de`. Unfortunately, there's not many good ones among them but it was still a fun project. :)
