---
title: 'The FutureRuby Revolution Will Not Be On AOL - Part 2'
date: 2009-07-25T09:37:00.000-07:00
draft: false
url: /2009/07/futureruby-revolution-will-not-be-on.html
tags: 
- futureruby
- ruby
---

[FutureRuby](http://futureruby.com) Day 2 began in a seemingly calm and reflective way. Coffees were sipped, and hangovers nursed. As the self-inflicted wounds from the [Pravda-Vodka-Kalashnikov](http://www.joeydevilla.com/wordpress/wp-content/uploads/2009/07/pravda_vodka_bar_3.jpg) faded, [Pete Forde](http://twitter.com/peteforde), our leader and spiritual adviser, began a short sermon.  
  
His message was simple: Vegas is a horrible place to hold [RailsConf](http://railsconf.com). And we should live in a manner that follows the ["Four Agreements"](http://www.amazon.com/Four-Agreements-Practical-Personal-Freedom/dp/1878424319). Seriously, yes, he said both of these things.  
  
Pete told us of the source of his sudden enlightenment: [Portland's Jupiter Hotel](http://www.jupiterhotel.com/). Instead of a Gideon bible, they have copy of Four Agreements in each room. Pete, being a curious guy, started to read the book. To save us time, he summarized it in nice Twitter-sized chunks.  
  
1\. Use your words for good... do not gossip  
2\. Do not take anything personally  
3\. Do not make assumptions  
4\. Always try your best  
  
With our spiritual bootstrapping complete, we proceeded to have a consciousness-expanding session from Collin Miller presentation called "Transc/Ending Encoding". This was NOT about video encoding.  
  
**[Collin Miller](http://twitter.com/collintmiller) - "Transc/Ending Encoding"**  
  
If the 60's revolt gave the counterculture heroes like [Leary](http://en.wikipedia.org/wiki/Timothy_Leary) and [Hoffman](http://en.wikipedia.org/wiki/Albert_Hofmann), it gave us tech heroes like [Englebart](http://en.wikipedia.org/wiki/Douglas_Engelbart) and [Kay](http://en.wikipedia.org/wiki/Alan_Kay).  
  
When writing software, we edit text files. We use textual encoding is a way to flatten down information to a simpler structure. But what does editing text lack? There are other options to make programs without text.  
  
There is this high priesthood of text, however, programming does not need to be difficult to be useful. The future is the ONLY frontier... so where are we as programmer-monks going?  
[  
Martin Fowler](http://twitter.com/martinfowler) has his concept of "[illustrative programming](http://www.martinfowler.com/bliki/IllustrativeProgramming.html)". As another example, a spreadsheet is non-textual programming.  
  
[Charles Simonyi](http://en.wikipedia.org/wiki/Charles_Simonyi)'s [Intentional Programming](http://en.wikipedia.org/wiki/Intentional_programming) in a different approach. It allows users to change names easily, or even program in two different natural languages. It does this by maintaining a constant set of references to everything in program. By doing this, different users can edit the same source database, without using the same editing style.  
  
Another example is Subtext ([http://www.subtextual.org/](http://www.subtextual.org/)). In Subtext, everything is just a reference. It is like "googling the code". Subtext uses decision tables, and a syntax tree editor.  
  
It was a very interesting talk, and it seems like many people were inspired to think differently about code. I was having [Smalltalk](http://www.smalltalk.org) flashbacks, and my brother [Damen Evans](http://twitter.com/damenevans) was reminiscing about how cool [HyperCard](http://en.wikipedia.org/wiki/HyperCard) used to be.  
  
**[Dr. Nic](http://twitter.com/drnic) - "Living with 1000 Open Source Projects"**  
  
Next up was "Dr. Nic" aka Dr. Nic Williams who is actually a PhD in CS, so not just granting himself an honorarium. His talk was called "Living with 1000 Open Source Projects". I have heard Dr. Nic speak before, and he is a very intelligent and funny speaker.  
  
There are two types of open source project founders:  
Type A. Nurture and converse "Do you care?"  
Type B. People who were previously type A  
  
"Who ever looked at their old code and thought 'that's better than what I write now'?"  
  
If you look after your old projects, you will end up with 500/hr. week of projects  
  
"Open source projects don't scale, but neither does raising pets and children"  
  
The question is which OSS projects to maintain? The pet projects you NEED every day  
  
Goal: ZERO maintenance  
  
How to reduce bad karma from "abandoning" your project:  
\- publish project status  
\- facilitate group therapy  
\- forward emails to mailing list  
  
Put a badge on project home page that says last time someone contributed to the project  
  
Aim for community to be self-sufficient  
  
[Github](http://github.com) makes things easier with centralized patches. The [github gem](http://github.com/defunkt/github-gem/tree/master) is great for laziness.  
  
"Easy to give away commit rights, if you think 'this is not MY project, I just look after it'"  
  
Aim: ZERO process cost  
  
Aim for Zero  
\- don't use it? do not maintain it  
\- manage expectations  
\- community self-sufficient  
\- zero process cost  
\- zero defects  
  
How to use your spare time  
\- find a hobby  
\- talk to your spouse  
\- create more projects  
  
"you can do less"  
  
Dr. Nic's talk really resonated with many of us. I, for one, immediately on getting back from the conference gave commit rights on two of my projects to two worthy individuals. Wow, what a relief!  
  
**[Matt Knox](http://twitter.com/mattknox) - "Crimes Against Humanity, Writ Small"**  
  
After Dr. Nic, was a great talk called "Crimes Against Humanity, Writ Small" from Matt Knox. I have been hanging out for the last couple of years with Matt at various Ruby conferences, but I had no idea how awesome he really is, till he got to show his stuff at FutureRuby.  
  
The message behind his talk was really about taking responsibility for one's own actions. This was a very important recurring theme, starting right from Nathanial Talbott's talk at the very beginning of FutureRuby "you write the software for the nukes, you own responsibility if they are used". In Matt's case, the "nukes" in question were adware. The kind that attaches itself to your machine like a vampire squid, and will not let go.  
  
Like all roads to hell, Matt's started with the best of intentions. His wonderful idea was killing adware on Windows with [Scheme](http://schemers.org/). As in [LISP](http://en.wikipedia.org/wiki/Lisp_(programming_language)). That sounds like a really fun job... and it was, at first.  
  
From an auspicious start "kill this worm", the job progressed to "kill lots of worms/malicious ad clients". Then the job became "somewhat edgy" aka "kill competitors and keep us from being killed... by anything"  
  
As a result of all this, there were major negative repercussions that took down the company. In the aftermath, Matt was able to do some amazing self-exploration. "What just happened? Is this just who I am?"  
  
That brings us around to the famous [Milgram experiments](http://en.wikipedia.org/wiki/Milgram_experiment). The incredible part was that 70% went the distance, and did what they thought was "torturing" another human being. Most human evil lives here.  
  
What does this mean?  
\- The human brain has a remote root exploit in 70% of the installed base  
\- Knowing is 1/2 the battle  
  
Good  
\- don't be evil  
  
Better  
\- recognize that people who do evil may not be evil  
\- this makes it easier to not hate them  
  
Best  
\- set up structures to insure this does not happen  
  
The world forgives. But to provoke forgiveness, one needs to own your actions, and their results.  
  
There is a remote root exploit in human brain, but the world forgives.  
  
Matt, thank you very much for your bravery and honesty, in sharing what was clearly a very painful learning experience.  
  
**[Paul Dowman](http://twitter.com/pauldowman) - "Between the Battleship and the FAILWhale"**  
  
After the raw psychology of Matt's talk, it was not easy for me to switch gears to Paul Dowman's talk "Between the Battleship and the FAILWhale". However, it was full of solid info with why's and how's about scaling. Here are a few highlights:  
  
Scalability != performance  
Performance is faster load time  
Scalability is handling greater load on same hardware  
  
2 kinds of scaling  
Vertical scaling - increase power of a single unit of your architecture  
Horizontal scaling - adding units to your architecture  
  
Why is scaling so hard? It cannot be an afterthought.  
Should I forget about my scaling problem till my app is a hit? It's a biz decision  
  
Developers and shareholders should talk about the tradeoffs, because scaling has costs: it requires more capital, and makes system more complex.  
  
You can do some simple things to prepare to scale, without a major engineering effort. The goal is to be able scale just by adding more servers  
  
HTTP Caching like [squid](http://www.squid-cache.org/), [varnish](http://varnish.projects.linpro.no/) or [Rack::Cache](http://github.com/rtomayko/rack-cache/tree/master)  
  
Use a queue for anything not needed to render the page right then. You will get a faster response, have a more consistent system load, and have less contention for locks.  
[  
Amazon SQS](http://aws.amazon.com/sqs/) is pretty cool. SQS is slow but scalable, simple and requires no maintenance or deployment.  
  
[Memcached](http://www.danga.com/memcached/) is inherently distributed, and you can just add more instance to scale. But it is not a database, so do not treat it like one. Data can/will disappear, since it is not persisted.  
  
For scaling your database, you have various options:  
\- Use an RDBMS like [MySQL](http://www.mysql.com/) or [PostgreSQL](http://www.postgresql.org/)  
\- [SimpleDB](http://aws.amazon.com/simpledb/)  
\- [Tokyo Cabinet](http://tokyocabinet.sourceforge.net/)  
\- [CouchDB](http://couchdb.apache.org/)  
\- something else  
  
Traditional RDBMS cannot scale horizontally forever. However, a lot of data does fit the table paradigm and SQL is powerful. Do not confuse data storage with data management.  
  
**[Joe Wilk](http://http://twitter.com/josephwilk) - "Cucumbered"**  
Next up was Joseph Wilk, all the way from London, to talk about [Cucumber](http://cukes.info/). Joe is a very unassuming but smart and witty fellow. The way he structured his talk was really clever. He used BDD itself to describe BDD... brilliant!  
  
So why use something like Cucumber? So that the customer can use something less syntactically stripped to describe their needs, THEN translate that to Ruby. It is a token of the conversation, and defines the acceptance criteria for the "customer". It is useful as a design tool, and provides executable documentation for the project.  
  
Cucumber has a gateway for different human languages, so that the developer and customer can interact in the customer's own human language. Like Swedish, Spanish, or LOLCATS. In fact there are currently over 30 languages already supported.  
  
Really, that is part of getting the most value out of Cucumber, is getting customers using Cucumber THEMSELVES... you can even just send around the "plaintext" using email, Google Docs, whatever allows you to share the plaintext data.  
  
The Art of "plaintext"  
\- don't force structure  
\- avoid noise  
\- avoid inconsistency  
\- balance abstraction  
\- use Ruby language building blocks to keep things DRY  
  
There are a couple of cool features that have gotten into Cucumber while I was not paying attention. One is Tagging, which allows you to tag a feature, and run only those features.  
  
`  
@any plaintext word  
  
cucumber --tags ~@in-progress  
`  
  
Another is Continuous Integration (Work In Progress) (--wip) which looks very useful since running each and every feature story can be time-consuming and slow down a CI build. Running all of the features as part of a nightly build is a workable compromise, and this look pretty useful to me for Integrity integration etc.  
  
It was a very cool talk from Joe, and if you are not using Cucumber you really should be. It is an amazing source of insight into the needs of the user, and a great way to explain WHY you are doing things, not just WHAT you are doing.  
  
**[Avi Bryant](http://twitter.com/avibryant) - "Failure: An Illustrated Guide"**  
Next up, Avi Bryant gave a fun talk called "Failure: An Illustrated Guide". He basically took us thru 30+ iterations (I lost count) of UI variations trying to create an important part of the functionality for his new site [Trendly](http://trendly.com/).  
  
It was interesting to see all of the different attempts that they made, in finally reaching what is a pretty cool and different UI metaphor for visualizing time-series data from website stats. Once the presentation video is online, it is for sure worth watching, not so much because of what they did, but more from how it will make you revisit your own UI.  
  
**[Jon Dahl](http://twitter.com/jondahl) - "Programming and Minimalism"**  
Jon's talk about "Programming and Minimalism" delved into the comparisons and contrasts of music and programming. He played a number of musical examples that showed stylistic development of musical genres from simple forms, to complex ones, and then evolved to simpler ones as part of a new "branch" of development.  
  
It was interesting to consider these parallels, especially since I happened to be sitting next to friend [Greg Borenstein](http://twitter.com/atduskgreg), who's classical musical vocabulary is much greater than mine, and had interesting side-channel comments. Like Avi's presentation, the video/audio is probably needed to in order to get more than a superficial explanation of his points.  
  
**[Brian Marick](http://twitter.com/marick) - "Artisanal Retro-Futurism and Team-Scale Anarcho-Syndicalism"**  
I was really looking forward to the next talk. Brian Marick is one of the original authors of the "[Agile Manifesto](http://agilemanifesto.org/)" and a very interesting thinker. I had heard him bandy about this phrase "Artisanal Retro-Futurism and Team-Scale Anarcho-Syndicalism" and I was eager to hear what it meant. FutureRuby was about to get radical. The [video of this talk](http://www.infoq.com/presentations/marick-retro-futurism) is now online, so I really suggest you check it out for yourself.  

>   
> "When I say agile, I mean Ruby... the way that Ruby projects are run"  
>   
> "Switching to scrum, at least my job doesn't suck as much as it used to"  
>   
> "I don't want to see on my gravestone, 'he made agile projects suck a little less'"  
>   
> "Even the wage-slave can have joy-in work"  
>   
> "the cubical is the single worst design of people and space to do software development"  

  
What is "anarcho-syndicalism"? It is a political/economic trade-union movement peaked in 1923, crushed in 1924 by the U.S. government.  
  
Here were a few of their tenants:  
\- getting rid of the government, and getting rid of private corporations  
\- worker self management  
\- direct action  
\- worker solidarity  
  
Brian suggests adopting some of the ideas of the anarcho-syndicalists but at Team-scale" meaning within your own team.  
  
Teams should band together more than they do, and we need more power in the hands of team to counterbalance the power in the corporation.  
  
So on to this "Artisanal" thing. Brian used the example of artisanal cheese. The people who make this cheese are very into cheese. They care about the cheese! They do not just do it for profit, profit is the result of their caring.  
  
Lastly back to the "retro-futurism". Recently, the New Yorker magazine did an issue about innovation. However, to capture the idea of innovation, they used images from the past, like the jet pack.  
  
The idea of "retro-futurism" is trying to recapture the spirit of hopefulness from the past. Books like [Freeman Dyson's "Infinite In All Directions"](http://www.amazon.com/Infinite-All-Directions-Freeman-Dyson/dp/0060915692) capture this endless sense of possibility.  
  
Do not let the context drive you, you control the context. Brian calls for a revolution in how software development projects are run, and challenges us to be scrappy, care, and keep our spirit of naive optimism.  
  
Start doing something about this: go to [arxta.net](http://arxta.net/), and talk to your teammates. And yes, I do have a sticker on my MacBook Pro.  
  
**[Jesse Hirsh](http://twitter.com/jessehirsh) - "Fighting the Imperial Californian Ideology"**  
The final presentation, from Jesse Hirsh, was even more radical than Brian Marick. Jesse challenged all of us by taking some of those same principles that we had all just agreed with coming from Brian about software, but extended them further. Much further.  
  
There have already been a couple of good posts that [summarize](http://www.joeydevilla.com/2009/07/15/futureruby-talk-fighting-the-imperial-californian-ideology/) or [comment](http://freelancing-gods.com/posts/future_ruby_and_californian_conflict) on Jesse's talk. Go check them out if you want more detail.  
  
A couple of books that have influenced Jesse are "[Snow Crash](http://en.wikipedia.org/wiki/Snow_Crash)" and "[Imperial San Francisco](http://www.amazon.com/Imperial-San-Francisco-California-Geography/dp/0520229029)". The reason this is important is that ideologies are viral. In the mid 1800's the US sent surveyors into California, and once the mineral wealth there are been established, declared war on Mexico to get mines.  
  
This was only the first of many "gold rushes" to take place in CA, although subsequent ones would develop other resources than mines. San Francisco technology invented the mining shaft to extract greater amounts of resources from the same mine. Taking those same technological achievements, a mining shaft turned upside down was a skyscraper - mining human labor instead of minerals.  
  
The Hearst mining family was the most successful of these robber barons of mining, and the most responsible for many of the negative outcomes that resulted. As an example, Hearst Mining is responsible for 8 of 10 Superfund hazardous waste cleanup sites.  
  
But it did not end there. As is well documented, the Spanish-American War, which resulted in the brutal colonial occupation of the Phillipines, was triggered by the first manufactured war, created by the first media mogul [William Randolph Hearst](http://en.wikipedia.org/wiki/William_Randolph_Hearst).  
  
San Francisco built all arms, and still responsible for all advanced military technology today. One big example is U.S. nuclear weapons, which are designed at the [Lawrence Livermore National Labs](https://www.llnl.gov/).  
  
This all established California as a place where a few small elites could conquer the world. The end of the cold war, was replaced by new imperial project - the California Ideology. The acolytes of this new ideology were [Kevin Kelley](http://www.kk.org/), [Stewart Brand](http://en.wikipedia.org/wiki/Stewart_Brand), and the [Global Business Network](http://www.gbn.com).  
  
Many saw the emergence of magazines like [Wired](http://www.wired.com/) and [Mondo2000](http://en.wikipedia.org/wiki/Mondo_2000) (shout-out to [RUSirius](http://en.wikipedia.org/wiki/R._U._Sirius)!) as the frontier of new techno-utopia. However, not everywhere has the silicon valley infrastructure. This new world was still under the dominance of SF.  
  
The corrupting influence and domination of SF was exemplified by [BALCO](http://en.wikipedia.org/wiki/Bay_Area_Laboratory_Co-operative) - the Bay Area Labratory Co-Operative known for the designer steroids that have altered professional sports irrevocably.  
  
When [Chris Anderson](http://twitter.com/chr1sa) wrote "[The Long Tail](http://www.thelongtail.com/)", Jesse says we all recognized it as brilliant. However, it reinforced the hierarchy to allow the few to get all of the best parts, while relegating everyone else to the skinny end of the long tail.  
  
Jesse goes on to attack Chris's latest manifesto "[Free](http://www.scribd.com/doc/17135767/FREE-full-book-by-Chris-Anderson-Read-in-Fullscreen)". He says there is something fundamentally wrong with his argument, however NOT the free part. Jesse says the fatal flaw is the ethic of waste. Chris says that now that bandwidth is in such abundance, we must waste it, because only then can we reach innovation.  
  
Jesse rails on waste as an ethic in CA (cars, weapons, mining etc). He prefers a revolutionary wholeism. Wholeism is a flip on relativism. Making everything the same, is NOT the answer, according to Jesse. We are in similar time with social tools like as when AOL took over Internet and turned it into total crap.  
  
When you have neighborhoods in the net, you can clean them up. We need to take the best tools available, merge into a coherent vision. Take a page from Barack Obama's playbook and become community activists.  
  
Who can you trust? Not the corporation, only your comrades, which is whoever you have social capital with.  
  
The struggle for human rights never ends, the question is which side are you on? The era of the nation-state is done, it is time for the new rise of the city-state. Get involved.  
  
Jesse had given an intense and fascinating talk. We could not complete the FutureRuby agenda, without some serious rabble-rousing. We surely have to individually take responsibility for what we choose to do with our power as technologists. Agree with Jesse on any individual point, or not, there was a lot of food for further thought.  
  
**Aftermath**  
The conference sessions were now over, but the FutureRuby festivities had not yet ended. After so many ideas compressed into so little time, we needed to hang out and process things together, while allowing it to be unstructured. [Meghann](http://twitter.com/meghatron) had come up with the innovative thought of putting the after-party into 3 different walkable nearby locations: a cool coffeehouse with retro video games, a classic little dive bar with live music, and [HackerspaceTO](http://hackerspaces.org). Not to mention a [hilarious street performance](http://www.vimeo.com/5592994) that could only happen somewhere open-minded like Toronto.  
  
Jamming on harmonica with a cyborg who played the water organ was just part of my personal awesome experience. Where is that video? So was getting to hang out at HackerspaceTO where they have frickin' laser beams. We timed it poorly, and missed the band dressed in Farscape garb, but there was so much to see and do, right up to the end.  
  
FutureRuby was not just a fun conference. And it was not just a chance to learn about a bunch of new things. It opened me up to new possibilities, and helped re-affirm my personal commitment. I thank all of the staff, volunteers, speakers, and attendees for making it an inspirational experience.