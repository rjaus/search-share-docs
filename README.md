# Welcome to Search Share

### What is it?
SearchShare is a PoC for sharing verified search engine results between users.

It enables a user to submit a copy of the search result they've received from a search engine, in a manner which does not enable the user to tamper or manipulate the results received.  In doing so, it enables at trustless relationship between users.

Once search results have been submitted, users visit the website to compare results between users, between queries & between search engines.

The use case builds upon the concepts of notarisation which enables the creation of signed copies of web pages, which are provably authentic & independently verifiable.  Signed pages can not be modified, manipulated or tampered with by the user who created them, or any parties who received them.  The signed page is authenticate in that it is represents the web page (web resource, or dom) as requested by the user, and delivered by the server.

![Search Share Example](https://github.com/rjaus/search-share-docs/raw/master/attachments/search-share-compare-results.png)


### Important Links
- SearchShare: https://searchshare.proofs.sh
- SearchShare Extension: https://github.com/rjaus/search-share-extension


## TLDR
## Problem
Lets say one day you ponder the question:
> How are the search results I receive different to those that my friends receive?

How would you solve this problem?

Screenshots is an obvious solution, but lets add a complication, **you don't trust your friends to provide accurate results**.  

Either through malicious intent, or technical incompetence, you can not rely on your friends to provide accurate results. Technical incompetence could include an inability to take a screenshots, taking screenshots which miss vital details, full length screenshots vs visible area of browser, screenshots which include sensitive details outside the browser window.

##### Some problems with screenshots:
- Not easily machine readable (requires OCR or machine learning to extract data)
- Do not verify any details of the data source
- Can be manipulated after they've been taken
- Websites can be manipulated prior to screenshots being taken

## Solution
Search Share solves this problem by having users submit signed (notarised) copies of their search results, which can then be parsed and compared.

Example: https://searchshare.proofs.sh/compare/6/8

![Search Share Example](https://github.com/rjaus/search-share-docs/raw/master/attachments/search-share-compare-results.png)

/TLDR

## Getting started
To explore search results that have been submitted by users, simply visit the website: https://searchshare.proofs.sh/compare/6/8

The process for submitting your own search results requires a few setup steps, see this doc: [How to submit search results](https://github.com/rjaus/search-share-docs/blob/master/How-to-submit.md)


## How does it work?
The PoC utilises [TLS Notary](https://tlsnotary.org/) as the mechanism for signing (notarising) web pages.  Signed web pages are then submitted to a centralised service, which parses & presents the ranking data to users.

The PoC works with:
- Duckduckgo
- Google
- Brave Search
- Bing

From the users perspective, the process of signing & submitting search results consists of:
1. Install the 'Search Share' chrome extension.
2. Visit a search engine and submit a query (eg: https://duckduckgo.com/?q=hacker+news)
3. Use the chrome extension to generate a signed/notarised copy of the page
4. Submit (share) the signed copy of the web page to the SearchShare API/website so that other users can see their search results

On the server side, the signed page is verified against the notary, to ensure it has not been tampered with.  The signed copy is then converted to plaintext, and the search engine rankings are parsed from the plaintext.

A visitor to SearchShare has access only to the parsed search engine rankings, they can not access the plaintext nor the signed page.

Using this architecture, the visitor can is assured that the search engine rankings presented are accurate, as delivered by the source (search engine).  They can be assured that the user who submitted them has not modified or manipulated the results.

As a centralised service, the visitor does need to trust that the centralised service (Search Share) has not modified the rankings / results, and they have competently verified the authenticity of the signed pages submitted by the user.  

The decision for a centralised vs decentralised architecture for this PoC was made primarily with the intent of releasing the PoC quickly and continue iterating.  See later section for discussion for further explanation.

## I don't believe you, this sounds like BS
No offence taken, happy for you to prove me wrong.  But if that's "just like your opinion, man", well...

**But if you want to actually dig deeper, I'll give you some starting points here: [Digging Deeper](https://github.com/rjaus/search-share-docs/blob/master/digging-deeper.md)**

![Thats just your opinion man](attachments/thats-just-like-your-opinion-man-the-dude.gif)

["That's just like your opinion, man" - The Dude (watch on youtube)](https://www.youtube.com/watch?v=Z-xI1384Ry4)




## Other Possible Solutions
### Screenshots
Users could take screenshots of their search results and submit them.

Issues:
- easily manipulated (modify image via photoshop)
- easily manipulated (modify dom prior to taking screenshot)
- image does not verify source (image has no relation to source)
- not machine readable (requires OCR or image recognition to extract data)

### Bots / Screen scraping
You could scrape search results via scripts/bots, utilising proxies for geo-location purposes.

Issues:
- Not real users, questionable accuracy of results compared to real user audience
- Bot protection / defence mechanisms, lowers efficiency and longevity of dev effort, and could further poising of results (if bot protection results in modified / filtered results, which goes unnoticed)

#### Proxy / Network Level Intercept
You could provide a proxy to the users and collect search data through the proxy.

Problems:
- Quite invasive from a user/privacy perspective
- Modifies / manipulates some aspects of the interactions, potentially poisoning data (location, ip address, grouping of users).  Although cookies and tracking data attribution would remain in tact.


