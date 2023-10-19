---
title: "Beer and Quarantine"
date: 2020-05-23
permalink: /posts/2020/05/quarantine-project
excerpt: "Alcohol-motivated web scraping."
tags:
  - coding_projects
  - python
---

## The premise
About a week ago, I got an email from my uncle Dennis:
> Hi,
>
> I seem to recall you doing some web scraping to do something useful. Do you have any advice as to how to do this? On this site I can see the beers in stock at my local store:
>https://belmont.craftbeercellar.com
>
>Here, I can find ratings of beers:
>https://www.beeradvocate.com
>
>I'd like to see the average Beer Advocate rating for beers available at Craft Beer Cellar. Even better if I can sort by style. Any suggestions on how to do that?
>
>Dennis

This sounded like a fun project to me, so I decided to take it on and build him something.

## The process
The first helpful thing I found was [this reddit post](https://www.reddit.com/r/Python/comments/32b9w7/pybeer_a_solution_to_beeradvocatecoms_lack_of_any/) that linked to [this repo](https://github.com/Jfach/beer-for-python). Unfortunately, that code doesn't work anymore because BeerAdvocate has changed their website formatting, so the patterns it was matching didn't work. But it was a super useful starting point since I'd never *actually* done any web scraping of this kind before (I didn't tell my uncle that).

It didn't take too long to get a working version of the BeerAdvocate query, and then I had to build one to scrape from the Beer Cellar site. That wasn't hard to work out with some trial and error and patterning off the BeerAdvocate one. Soon, I was ready to try to loop through all the results!

## The pickle
(not the Python serialized kind)

After almost instantaneously getting banned from the Beer Cellar website, I quickly realized I needed to drop in some pauses to avoid triggering the websites' protections against DDOS attacks and the like. This made the code take a bit longer to run, but solved the problem handily.

## The product
In the end, I got something together that I'm quite happy with. Some features include:

* In addition to collating the score and style (as well as ABV) from BeerAdvocate, one can customizably categorize the styles into larger clusters (e.g. English and American IPA both categorized as just "IPA") for easier sorting
* If the search on BeerAdvocate yields multiple results, uses fuzzy string matching (via the Levenshtein distance as implemented in the `fuzzywuzzy` and `python-Levenshtein` packages) to choose the best match (if this happens, a remark will be put in the "note" column of output and you can check the included BeerAdvocate link to make sure it's the right brew)
* Since running the script when ~800 beers are available takes ~40 minutes, optionally check previous output file and only query for beers that don't have scores listed there, or only for beers that don't have an entry there at all (this reduces runtime to ~10-15 minutes for a relatively recent output file).

Here's a selection of the output file content:

| name | style | score | brewer | abv | link | note | category |
|:----:|:-----:|-------|:------:|-----|:----:|:----:|:--------:|
| Breakfast Brew | English Oatmeal Stout | 100.0 | Canned Heat Craft Beer Company | 8.3 | [link](https://www.beeradvocate.com/beer/profile/1199/11757/) | multiple results, guessed best match | Stout |
| Softly Spoken Magic Spells | New England IPA| 98.0 | Singlecut Beersmiths | 8.6 | [link](http://www.beeradvocate.com/search/?q=Softly+Spoken+Magic+Spells&qt=beer) | | IPA |
| Samichlaus Helles | German Maibock | 86.0 | Brauerei Schloss Eggenberg | 14.0 | [link](https://www.beeradvocate.com/beer/profile/285/39766/) | multiple results, guessed best match | Other |
| Picnic Sunrise | Berliner Weisse | NaN | Brekeriet Beer Ab | 2.7 | [link](http://www.beeradvocate.com/search/?q=Picnic+Sunrise&qt=beer) | No score yet | Sour |
| All My Best Friends Hop Heads | ? | NaN | Armada Brewing | ? | none | couldn't find BeerAdvocate page | Other|

If you want to check this out for yourself, it's all up on GitHub [here](https://github.com/rkurchin/dennis_beer), so feel free to play around!

Hope you're staying healthy, safe, and sane in quarantine. Apparently my reaction to working from home on my computer all day is to take on evening projects to spend even *more* time at my computer! Don't worry, I'm still getting outdoors too. Most days.
