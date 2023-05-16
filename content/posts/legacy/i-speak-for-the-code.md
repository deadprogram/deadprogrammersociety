---
title: 'I Speak For The Code'
date: 2007-03-14T15:14:00.000-07:00
draft: false
url: /2007/03/i-speak-for-code.html
tags: 
- software architecture
- agile development
---

[![](http://3.bp.blogspot.com/_SgxaAaUGqzY/RfjBjNYIkgI/AAAAAAAAAAk/34WaJhSA0SI/s200/lorax.gif)](http://3.bp.blogspot.com/_SgxaAaUGqzY/RfjBjNYIkgI/AAAAAAAAAAk/34WaJhSA0SI/s1600-h/lorax.gif)

Recently I was in a client meeting with a bunch of managers to discuss some very complex changes that were being proposed for an existing system. I was invited to the meeting so I could "speak for the code", which to them meant that I could validate the ideas of the group based on my knowledge of the code base.  
  
After the meeting ended, I kept mulling over that phrase "speaking for the code". The more I did, the more I realized the parallels between "speaking for the code" as an architect or lead developer, and the Lorax "speaking for the trees" in the [Dr. Seuss story of the same name](http://en.wikipedia.org/wiki/The_Lorax).  
  
So here goes my attempt to illustrate some lessons about best practices in software development, inspired by the story of the Lorax...  
  

>   
> At the far end of town where the Grickle-grass grows and the wind smells slow-and sour when it blows and no birds ever sing excepting old crows...is the Street of the Lifted Lorax.  
> And deep in the Grickle-grass, some people say, if you look deep enough you can still see, today, where the Lorax once stood just as long as it could before somebody lifted the Lorax away.  

  
Our story begins looking at what remains of a once thriving software application, now gone to ruin. What went wrong?  

>   
> What was the Lorax?  
> Any why was it there?  
> And why was it lifted and taken somewhere from the far end of town where the Grickle-grass grows?  
> The old Once-ler still lives here.  
> Ask him. He knows.  

  
Perhaps the Lorax was the original system architect. But he is gone now, leaving behind Once-ler who is now in charge of the project.  

>   
> You won´t see the Once-ler.  
> Don´t knock at his door.  
> He stays in his Lerkim on top of his store.  
> He stays in his Lerkim, cold under the roof,  
> where he makes his own clothes  
> out of miff-muffered moof.  
> And on special dank midnights in August,  
> he peeks out of the shutters  
> and sometimes he speaks  
> and tells how the Lorax was lifted away.  
> He´ll tell you, perhaps... if you´re willing to pay.  
> Then he hides what you paid him away in his Snuvv,  
> his secret strange hole in his gruvvulous glove.  
> Then he grunts, I will call you by Whisper-ma-Phone,  
> for the secrets I tell you are for your ears alone.  

  
The Once-ler is the [swamp guide](http://www.laputan.org/mud/) project manager or developer who remains behind, holding on tightly to the secrets of the system.  

>   
> Now I´ll tell you, he says, with his teeth sounding gray,  
> how the Lorax got lifted and taken away...  
> It all started way back... such a long, long time back...  
>   
> Way back in the days when the grass was still green  
> and the pond was still wet  
> and the clouds were still clean,  
> and the song of the Swomee-Swans rang out in space...  
> one morning, I came to this glorious place.  
> And I first saw the trees! The Truffula Trees!  
> The bright-colored tufts of the Truffula Trees!  
> Mile after mile in the fresh morning breeze.  
>   
> And under the trees, I saw Brown Bar-ba-loots  
> frisking about in their Bar-ba-loot suits  
> as they played in the shade and ate Truffula Fruits.  
>   
> From the rippulous pond came the comfortable sound  
> of the Humming-Fish humming while splashing around.  

  
The original system was a fine merger of art and science. It provided for all of the inhabitants of its [software ecosystem](http://codebetter.com/blogs/jeremy.miller/archive/2006/08/13/148258.aspx) (users, developers, testers, etc.) by using practices that conserved the ecology of the system. It was able to successfully grow from its origin to a useful level of functionality while preserving the environment of the code base.  

>   
> In no time at all, I had built a small shop.  
> Then I chopped down a Truffula Tree with one chop.  
> And with great skillful skill and with great speedy speed,  
> I took the soft tuft. And I knitted a Thneed!  
>   
> The instand I´d finished, I heard a ga-Zump!  
> I looked.  
> I saw something pop out of the stump  
> of the tree I´d chopped down. It was sort of a man.  
> Describe him?...That´s hard. I don´t know if I can.  
>   
> He was shortish. And oldish.  
> And brownish. And mossy.  
> And he spoke with a voice  
> that was sharpish and bossy.  
>   
> Mister! he said with a sawdusty sneeze,  
> I am the Lorax. I speak for the trees.  
> I speak for the trees, for the trees have no tongues.  
> And I´m asking you, sir, at the top of my lungs--  
> he was very upset as he shouted and puffed--  
> What´s that THING you´ve made out of my Truffula tuft?  

  
The Once-ler took the original application in a direction that it was not architected to take, in a way that disturbed the equilibrium enough to attract the ire of the Lorax, who is the guardian for the system's logical integrity.  

>   
> Look, Lorax, I said. There´s no cause for alarm.  
> I chopped just one tree. I am doing no harm.  
> I´m being quite useful. This thing is a Thneed.  
> A Thneed´s a Fine-Something-That-All-People-Need!  
> It´s a shirt. It´s a sock. It´s a glove. It´s a hat.  
> But it has other uses. Yes, far beyond that.  
> You can use it for carpets. For pillows! For sheets!  
> Or curtains! Or covers for bicycle seats!  
> The Lorax said,  
> Sir! You are crazy with greed.  
> There is no one on earth  
> who would buy that fool Thneed!  

  
The Once-ler is utterly convinced of his own ideas regarding the directions for the system, and is not interested in listening to the warnings of the Lorax. He thinks he knows what the users need, and how to make the system fill that need. Or perhaps he is using the wrong design patterns, or too many different patterns, or some classic [anti-patterns](http://www.agilemodeling.com/essays/enterpriseModelingAntiPatterns.htm).  

>   
> And, in no time at all,  
> in the factory I built,  
> the whole Once-ler Family  
> was working full tilt.  
> We were all knitting Thneeds  
> just as busy as bees,  
> to the sound of the chopping  
> of Truffula Trees.  
>   
> Then...  
> Oh! Baby! Oh!  
> How my business did grow!  
> Now, chopping one tree  
> at a time  
> was too slow.  
>   
> So I quickly invented my Super-Axe-Hacker  
> which whacked off four Truffula Trees at one smacker.  
> We were making Thneeds  
> four times as fast as before!  
> And that Lorax?... He didn´t show up any more.  

  
Now the Once-ler is scaling up the project, using all of his old buddies. Now four times [more staffing](http://en.wikipedia.org/wiki/The_Mythical_Man-Month) than before. Not only that, but with such confidence in his vision that he doesn't miss the fact that the crucial architectural knowledge of the Lorax is no longer guiding the project.  

>   
> But the next week he knocked on my new office door.  
> He snapped, I´m the Lorax who speaks for the trees  
> which you seem to be chopping as fast as you please.  
> But I´m also in charge of the Brown Bar-ba-loots  
> who played in the shade in their Bar-ba-loot suits  
> and happily lived, eating Truffula Fruits.  
> NOW...thanks to your hacking my trees to the ground,  
> there´s not enough Truffula Fruit to go ´round.  
> And my poor Bar-ba-loots are all getting the crummies  
> because they have gas, and no food, in their tummies!  
>   
> They loved living here. But I can´t let them stay.  
> They´ll have to find food. And I hope that they may.  
> Good luck, boys, he cried. And he sent them away.  
>   
> I, the Once-ler, felt sad as I watched them all go.  
> BUT... business is business! And business must grow  
> regardless of crummies in tummies, you know.  

  
The Once-ler is willing to do anything at all to the code base, including losing the architectural consistency of the system, in order to implement his new vision for the project. Or lose anyone at all on the project team, for that matter, to maintain control over the project. Too bad Once-ler doesn't realize that once the tipping point of architectural instability is reached, a system can become unreliable and unmaintainable very quickly.  

>   
> And then I got mad. I got terribly mad.  
> I yelled at the Lorax, Now listen here, Dad!  
> All you do is yap-yap and say, Bad! Bad! Bad! Bad!  
> Well, I have my rights, sir, and I´m telling you  
> I intend to go on doing just what I do!  
> And, for your information, you Lorax, I´m figgering on biggering  
> and BIGGERING and BIGGERING and BIGGERING,  
> turning MORE Truffula Trees into Thneeds  
> which everyone, EVERYONE, EVERYONE needs!  
>   
> And at that very moment, we heard a loud whack!  
> From outside in the fields came a sickening smack  
> of an axe on a tree. Then we heard the tree fall.  
> The very last Truffula Tree of them all!  

  
Did you see THAT coming? Of course you did! Once the [technical debt](http://www.martinfowler.com/bliki/TechnicalDebt.html) of the system exceeded the available resources, the application went bankrupt.  

>   
> No more trees. No more Thneeds. No more work to be done.  
> So, in no time, my uncles and aunts, every one,  
> all waved me good-bye. They jumped into my cars  
> and drove away under the smoke-smuggered stars.  
>   
> Now all that was left ´neath the bad-smelling sky  
> was my big empty factory... the Lorax... and I.  

  
Once the project's future prospects are bleak, project funding or company revenues dry up. As a result, key resources leave. When this vicious cycle begins, there may be no stopping it.  

>   
> The Lorax said nothing. Just gave me a glance...  
> just gave me a very sad, sad backward glance...  
> as he lifted himself by the seat of his pants.  
> And I´ll never forget the grim look on his face  
> when he heisted himself and took leave of this place,  
> through a hole in the smog, without leaving a trace.  
>   
> And all that the Lorax left here in this mess  
> was a small pile of rocks, with one word...  
> UNLESS.  

  
If you are an architect or dev lead, you are probably sympathizing with the Lorax as you sometimes feel like you are "defending" your system. If you are a hiring manager or recruiter reading this blog, perhaps at this point in the story you are getting a idea about why it is hard to recruit and retain the best system architects and developers to work on toxic projects.  

>   
> But now, says the Once-ler,  
> Now that you´re here, the word of the Lorax seems perfectly clear.  
> UNLESS someone like you cares a whole awful lot,  
> nothing is going to get better. It´s not. SO...  
> Catch! calls the Once-ler. He lets something fall.  
> It´s a Truffula Seed. It´s the last one of all!  
> You´re in charge of the last of the Truffula Seeds.  
> And Truffula Trees are what everyone needs.  
> Plant a new Truffula. Treat it with care.  
> Give it clean water. And feed it fresh air.  
> Grow a forest. Protect it from axes that hack.  
> Then the Lorax and all of his friends may come back.  

  
System architects, let a thousand flowers bloom. Fight for your systems.  
  
RIP, Dr. Seuss. We miss your wisdom.