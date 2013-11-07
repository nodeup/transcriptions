[53: A Very Meta Show](http://nodeup.com/fiftythree)
===

Panel:

* [Daniel Shaw](https://twitter.com/dshaw)
* [Nizar Khalife](https://twitter.com/khalifenizar)
* [Erik Isaksen](https://twitter.com/eisaksen)
* [Cliffano Subagio](https://twitter.com/cliffano)
* [Matt Creager](https://twitter.com/matt_creager)

Table of Contents:

1. [Introduction](#introduction)
2. [NodeUp Stories](#nodeup-stories)
3. [Favorite Episodes](#favorite-episodes)
4. [A CoffeeScript Show](a-coffeescript-show)
5. [Experimental Stuff](experimental-studd)
6. [Plugs](plugs)

## Introduction

00:17 - **Daniel Shaw**: Hello and welcome to NodeUp. This is dshaw and today NodeUp Episode 53 is a very very meta NodeUp. Today I'm joined by Erik Isaksen from West Virginia, Cliff Subagio all the way from Australia, and Nizar Khalife from Miami Florida. We're going to do a very meta NodeUp and talk about NodeUp and the NodeUp experience. I had a great chat with Nizar at Realtimeconf, and there's some reasons why I'm doing NodeUp that I feel are important, and that same conduct is shared with a lot of other people. So I wanted to chat about that; it's a fun conversion.

Our sponsors today are [&yet](http://andyet.com), [Modulus](http://modulus.io), and [Clock](http://clock.co.uk). Thanks so much for supporting NodeUp and supporting the Node community. So let's go around the horn and introduce ourselves. Erick, you want to tell us who you are and what you do?

01:38 - **Erik Isaksen**: Sure, I'm a UX Engineer at [3Pillar Global](http://www.3pillarglobal.com/). That's sort of a new title for me. I've been kind of inventing this job. Basically, what I've been doing is I've been using node to do rapid prototyping for applications we're building. I'm also using AngularJS. My background is mostly in frontend technologies: JavaScript, CSS, HTML. And I've worked with Bloomberg doing some Ruby work the last three years.

02:05 - **Daniel Shaw**: Fantastic. Cliff?

02:07 - **Cliff Subagio**: I'm a software developer from Melbourne, Australia. It's 4 A.M. here, it's lovely. I've been a [node.js](http://nodejs.org/) user since 0.2 when promises were still there. I had a fun experience with taking promises out and replacing it with callbacks back then, when it was taken out of core. I've been a NodeUp listener since Episode One.

02:32 - **Daniel Shaw**: Wow. Nizar?

02:33 - **Nizar Khalife**: I'm a web developer at [Nobox](https://www.facebook.com/Nobox), a digital marketing agency in Miami. They have offices in Puerto Rico too, where I'm originally from. I started listening to NodeUp this year, when I got into node heavily.

02:47 - **Daniel Shaw**: Excellent, cool. So, a broad spectrum. Before I kick off the NodeUp stories, I want to give a shout out to our first sponsor, [&yet](http://www.andyet.com/). I want to give a special shout out for all they've done to support the node community. Nizar and I were just at [Realtimeconf](http://realtimeconf.com) -- and this is the last year of realtimeconf. The amount of heart and soul that they've poured into realtimeconf over the years and how much they've contributed to the community, making it special for everybody. We have the warmest of appreciation for everything that they do. I can't say enough good about what Adam Brault and his team brings to the world.

They put that same effort and dedication into everything that they build. I invite you to take a look at their chat, IRC, teams management product for the web. It's called [And Bang](https://andbang.com/) and it's a fantastic tool. They have dedicated themselves to building these world-class experiences and do that same work for clients like AT&T. They've become real leaders in the webRTC space, so if your company is looking to build anything in the spectrum of realtime JavaScript / webRTC, I invite you to reach out to &Yet. And even if you aren't going to reach out to them as a company, reach out and say thank you for all that they're doing, as a listener to NodeUp. I would appreciate it if you personally reach out to &yet and thank them because they've done so much. So thanks guys, for supporting NodeUp.

## Nodeup Stories

05:05 - **Daniel Shaw**: Alright, the NodeUp stories. I want to kick this off and share a little bit of why I'm here. I started fairly on in NodeUp, wasn't on the first few episodes. Last year we were a bit differently organized and had more random hosts and as we came into 2013, everyone got a little more busy and I stepped up and have been the main host for the show since then. The reason why I did that was, during conference season 2012, I spoke to a lot of people while I was in Europe at LXJS and Node Dublin and there were individuals and groups -- for example, a team of two out of Lithuania who were dedicated to developing with node -- and NodeUp was the only contact that they had with the larger node community. I really empathized with this. Before coming out to San Francisco, my wife and I were living in West Virginia I'd gone to school after the dot com, and prior to that I was living in the middle of nowhere in Italy, (in Umbria, Perugia if you know the area). I just had to go out of my way to hang out with any other developers who gave a shit at the level that I did. Same thing in West Virginia; I drove an hour and a half a couple evenings a month to go hang out with a Closure development group. I wasn't into Closure, I just wanted to hang out with JavaScript developers even if it wasn't anything I could possibly do. At a pair programming event, I met with the leader of that Closure group and really connected with his passion for programming and sharing. So I would hack with them fairly indirectly. So that's why I put so much into NodeUp. It means a lot to me. Going to conferences and having people come up and thank me for doing NodeUp really means a lot. I really appreciate it and thank everybody for powering through the "Ums" and various verbal ticks I have to make this something that allows everyone in the community all over the world to connect.

Nizar, we had the most recent chat. Why don't you fill everybody in and share a little about your experience with NodeUp. You're the new guy on the block.

08:30 - **Nizar Khalife**: I started earlier this year to really get into node thanks to a buddy of mine who I work with. When I first started I hacked on my own, silly little things like rearranging folder structures and things like that. The more I tried to solve problems the more I was hungry for information. I was like, "how do you do this, how to do you that?", so I started listening to NodeUp. I don't remember which episode I listed to first, but after that I went back and listed to all of 2013's episodes. And I actually listened to a couple episodes yesterday to freshen my memory. I've loved it so far -- it's been awesome. And I might even go back to 2012 and check those out at some point.

09:26 - **Daniel Shaw**: Yeah, I'm wondering how well those hold up! I haven't gone back. There was a particular rant, I believe in NodeUp 6, where I was in a work scenario where I was the [socket.io](http://socket.io/) guy. I was actually the only node guy on the team at a primarily Rails shop and the service had fallen over in private beta at 100 connections. It was like "No! This is not any sort of scale level that should be crippling the service!" So that was a particular nice rant that I refer to. I'd love to hear about it, as you dive back in. Most of it will be node 0.8, maybe there's some 0.6 back there. It feels like an eternity for me. I'm really curious to hear if those early NodeUps still have a lot of information that's great. There's a lot of technical meat in there. We've been trying to get a good transcription service set up. We've made a few stabs at it but we haven't really found the right solution. To get NodeUp professionally transcribed is $400-$500 an episode to do it right. It's something we keep iterating on. If someone is really interested in owning transcription of NodeUp, I think that would be a wonderful contribution.

Erik, would you like to share your experience?

11:34 - **Erik Isaksen**: A few years back I was working with some guys from the ThoughtWorks company. We were working on Ruby projects. Prior to that I worked mostly with JavaScript and CSS. If you got a bug in IE6, you sent it my way. I was that guy. Which was cool. It was really a great experience with them because I had a chance to learn TDD, working with XP-type of practices, and it was really enjoyable. So I started to ask what are some other technologies out there, and I saw a video on YUI Theatre Ryan Dahl that got me interested first. I was looking for resources and everywhere I went they said just load up express and here are these cookie cutter pieces. I was like "well I'm not going to learn a lot this way so I need to find some more materials." And that's when I found NodeUp. I looked at the podcasts that were around and you guys were pretty much it. I was really happy when I started listening - this is really good material because you guys have people who are working in code, first of all, and you guys are also heavy users of this stuff. So it was really great - every time a new podcast would come out I'd be jogging through DC and listening to you guys.

Now that I'm working at 3Pillar, I'm prototyping and I get to choose whatever I want to use. So I decided I'm going to throw in Express and do that cookie cutter piece but I'm not going to build any scaffolding. I'm going to take this and see what I can do from the metal. And kind of build out my own controllers, build out my own models, and see what happens. I've been having a really great time. I've been doing it since July, full time.

14:17 - **Daniel Shaw**: I'd love to hear an update as that evolves. That's been my evolution; pushing back away from frameworks has been an increasing thing, especially as you're trying to grind out the raw performance. You can go far with that. I'm glad to see you adopting that and would love to see how that plays out.

So, Cliff. Cliff has a special story. And he's a big fan of kangaroos.

15:00 - **Cliff Subagio**: Second-best after Isaac and Mikeal, I guess. And your story, really. You guys really drum up about Australian Kangaroos. Back then, I think it was around 2011, the first NodeUp, well even before that I was on a Java/EE project. And for parts of the application we were looking for something that's more productive as a platform. We saw Ryan's talk introducing node and async I/O, and we thought "Hey, this is really making sense." And we started looking at node in really early days. When I found out about NodeUp, back then and even now I still listen to other podcasts, but I thought you guys are really relaxed when you recorded all the episodes. Really! When I listened to the first few episodes, I imagined all the hosts were drinking beer while talking about node, and this was so relaxing. Well, beer or tea, depending on your taste I guess.

Isaac, Mikeal, yourself, and all the others, you were going off about Australia for [Bislr](http://bislr.com), and talking about kangaroos. Actually, I got questions from friends outside Australia asking "are there lots of kangaroos in Australia" and I said "No, unless you go to the bush land or to the zoo." But the funny thing is, just last weekend -- and this is real, you can check it on BBC's website -- a kangaroo actually hopped into the airport terminal in Melbourne. They had to seal off part of the airport, I think it was the pharmacy, and they had to tranquilize the kangaroo and take it out. It's a funny coincidence but you might be able to see a kangaroo at the airport.  

(17:21 - 17:28 ... and I also keep notes about all the Australia ??? on my blog.)

Back then we had an application running with node 0.2 and it was actually in production until a few months ago. Which is quite interesting. It was stable on 0.2. It's really different on 0.4 and onward, but stable enough. My recent project with node involved trying a microservice architecture with node. It works quite nicely because each app can become a module and one way to bundle everything all together is to have each as a dependency in package.json. I think it fits really nicely with the idea of having one service doing one thing well and then node's idea of one tool doing one thing well. And we just pack them up all together. So that's my node and NodeUp experience.

18:40 - **Erik Isaksen**: Are you using anything specifically to mount those together?

18:42 - **Cliff Subagio**: No, just npm.

18:47 - **Daniel Shaw**: Great! You guys touched on a little bit of the impact on the node community. And we talked about NodeUp as individuals. I guess you could extend that as how you've seen NodeUp impact your friends. have you found that NodeUp has been at all helpful in orienting your friends or colleagues who are looking to embrace node? You've gone through that process as individuals, but what is the greater impact of NodeUp?

19:24 - **Nizar Khalife**: My buddy Joel, he definitely goes back and listens to the Performance Show, for example, if he's having his own performance pain. For starters, it's a great source of reference, to see how the leaders of the community have been solving their problems.

19:48 - **Erik Isaksen**: I agree with that, too. I find myself I have another former colleague who worked with node as well. I find myself going back to the API Episode. That was really useful for me. When I was a Bloomberg, we had a lot of services - we didn't use Active Record as much in Rails, so it was mostly smaller stuff for that. We had a lot of services running so I wanted to set up my own services and find out what would be the best thing for that, and [Restify](http://mcavage.me/node-restify/) seems really interesting to me.

20:30 - **Nizar Khalife**: Restify is awesome. I think the other thing that's really important compared to other tech podcasts I've listened to is what I mentioned before: having the people actually working on node coming up and giving their schpeel about what's coming up in the next version, or the next two versions, even. Early in the year, when you were talking about not even having released 0.10 yet, I think Isaac some things about 0.12. There's a lot of good knowledge and good insight, just having them come on a talk about the past, present, and future of node.

21:16 - **Erik Isaksen**: Yeah, you get so much more hearing it from the source, rather than having to sift through the docs, for sure.

21:21 - **Daniel Shaw**: Absolutely. Living in San Francisco and hanging out with some node core people like that, in casual conversations I have the opportunity to tune into some of that stuff. My goal is just to share that with the rest of the node community. But some of that core stuff is not going to apply to everybody. We all interact at different levels of the stack. The internal implementations of buffers and stuff like that might not be directly relevant, but two things: (1) it might not be directly relevant until it is; you may be operating at the express level of the stack and then as Erik said, you strip that out and begin to go lower level as you need more performance. The biggest take-away from the experience at Voxer is exactly that: when you're really trying to maximize the I/O throughput you want to minimize your call chain and reduce the surface area of your computation. (2) The most efficient code is the code that isn't run, right? Not doing anything is the most efficient computation. Obviously that's not useful in most contexts, but it is useful as you're trying to maximize throughtput. And if you can minimize that surface area then you can really tune that down. 

23:29 - **Erik Isaksen**: Not just for performance, though. Having to build stuff from scratch really teaches you what's possible. After hearing [substack](https://github.com/substack) and some of the other guys talk, I would go to their githubs and look at the code to get an idea of what's going on. And then that was like "Okay, why are they doing this rather than the style I'm used to?" I'm used to JavaScript in the browser, before this. It definitely helps with learning, stripping away those layers. 

24:02 - **Nizar Khalife**: Yeah, in the browser in general, it's a lot less structured. There's not a right way to do things in the browser, necessarily. And even if you use a framework, there's different frameworks to choose from. There's not a consensus really on how you should do things. But I know there are -- even if not 100% of people agree -- some patterns that converge.

24:28 - **Erik Isaksen**: There's definitely more consistency. It's getting better, but we still have to deal with earlier browsers so there is a little bit of inconsistency there for sure.

24:38 - **Nizar Khalife**: And on that subject of the core stuff, it's not always about the nitty gritty under the hood things. It's also "Hey, in 0.10 the major thing is we have new streams". You may not be 100% on top of those changes to know what's going on. I think in 0.12 there's going to be some generator stuff coming in and that's nice to know that things are coming that you can play with.

25:10 - **Daniel Shaw**: I'm going to take a quick break and we'll talk about our next sponsor, [Modulus](http://modulus.io/). Modulus is a node.js hosting platform -- they have a great platform with built-in mongodb hosting so if you're building a MEAN stack (Mongo, Express, Angular, Node) app with mongodb as a key component of your they have fantastic instrumentation of how the database backs up to mongo and the performance statistics of your mongodb backend is very nicely integrated. There is built-in analytics for your app to see how things are performing. They offer free custom SSL in their packages, full websockets support, and you can run nearly every node.js version available. Those of you still running 0.4, I'd you to see if you guys can reach out to them and see if they'll run that for you. That would be fun. When you reach out to Modulus, use the promo code nodeup1 and you can get started with them for free. They are [modulus.io](https://modulus.io/) on the web and [@OnModulus](https://twitter.com/OnModulus) on Twitter. Thanks so much for the support, guys, and keep doing great things with creating a really dynamic hosting platform.

27:11 - **Daniel Shaw**: We've slipstreamed someone else into the show. All the way from Canada, Matt Creager is joining us. Matt, why don't you tell us a little about yourself. Matt's coming all the way from Halifax, Novia Scotia. Why don't you go ahead and fill in the blanks and add in your NodeUp story.

27:44 - **Matt Creager**: Hey folks, nice to you. This is my first ride in the slipstream, so that's exciting. Yeah so I'm from Halifax, Novia Scotia and we don't have a huge node community here -- that might come as a surprise, or maybe not. I'm a member of a software engineering team at [GoInstant](https://goinstant.com/). We're building a platform for realtime apps on top of node, to make it a bit more accessible to primarily client-side developers. Before GoInstant I was with Blackberry, and a few of you might be sighing with relief for me at that statement. But that's where I actually encountered NodeUp. I was trying to convince the engineering team there that we should use node to build this really cool dashboard with all kinds of realtime analytics. I managed to convince zero people that it made sense, which raised my hackles and left me with a lot of concern about that team. So I started reaching out to people around me that I thought might be interested in node and there really wasn't anyone at that point in time. So let's back up and say that NodeUp is the reason I currently work at GoInstant. It's the reason that I'm working on the project I'm working on, and the people that I'm working with. That is a big statement but it's absolutely the truth. I was part of a team at Blackberry that was working on these realtime dashboards and developing these realtime dashboards with the stack that we were using was basically impossible (PHP). I'd attempted to introduce them to node and met so much resistance and pushback that I just started using node for my own projects. That lead me to this hackathon that was hosted in Halifax by GoInstant and I actually ended up striking up a conversation with one of the founders and the VP of engineering about, of all things, NodeUp. I think it was the [Community Episode](http://nodeup.com/twentysix) and that conversation lead to having a couple of drinks and six months later I'm currently working at GoInstant with a bunch of guys that just hack on node all day. And I'm super excited about it. 

30:34 - **Erik Isaksen**: That's awesome.

30:36 - **Daniel Shaw**: I had a chance to meet the team at realtimeconf and it seems like you guys have a really great team and a wonderful contributions out there. Outside of the team, do you have anyone else to create community with up there?

30:55 - **Matt Creager**: That's a good question. In a way, what NodeUp really is to me is an example -- and obviously it's fundamental to the community and the community centers around it -- but really what is does is it teaches us how to build our own communities. And GoInstant is at the center of the node community in Halifax. As I speak I'm actually sitting in a startup hibernator [incubator] in Halifax and we've come over to do a presentation on node. So we're really trying to get into the community and introduce node to the other people here who could use it to improve their tech stack.

31:34 - **Erik Isaksen**: you guys do local meetups up there?

31:39 - **Matt Creager**: Basically, hackathons at this point are the primary way that people get together. When I was at realtimeconf last week with dshaw I met Jason, the guy organizes [LXJS](http://lxjs.org/) and I really picked over his brain and got some ideas. So I'm seriously interested in trying to bring something like that to the Maritimes.

32:05 - **Daniel Shaw**: Fantastic. I couldn't be happier that that's NodeUp's contribution to the world: helping other communities develop. I guess most everybody tuned into International Nodebots Day this Summer. A really fun event, or a loosely affiliated anarchy of events across the world. The great thing about that is those turned out to be seed events and other things have happened beyond that. I've gone on to start Nodebots SF. The Nodebots as a concept and a meetup experience is one that I particularly love because it's a fairly low barrier to entry to participation and it's extremely participatory. So rather than having a format that's discussion and talk, it's everybody getting together and talking and hacking on hardware. I've tried to extend that into a broader context and support that in new ways.

## Favorite Episodes

33:53 - **Daniel Shaw**: Let's chat real quick about some of the our favorite shows that have gone through NodeUp. I will kick that off with my favorite show, coming out of the realtime community, and that being my connection with node and why I got started with node -- building backends for websockets. The [Realtime Show](http://nodeup.com/thirtyfive) really shared a lot of the production challenges of creating effective realtime systems. We've done so well as a community to create a low barrier to entry for the codebases, socket.io especially, but actually running at scale in production is extremely challenging. Using websockets on modern Chrome if you have a great Internet connection? Awesome. But if you have a crappy Internet connection or God forbid you're on mobile, it's really a house of pain. That was absolutely my favorite episode that I've done and listened to. Lots of resources there.

35:44 - **Nizar Khalife**: I have two favorites. I really liked the [Module Authoring Show](http://nodeup.com/forty) where Isaac and substack and Mikeal discuss how you guys approach writing modules and designing the interface and all that. I got a lot out of that. They talked about the small module philosophy, which you've talked about in other podcasts. And also I really like the idea they owned up to having written modules that no longer match up to the standards of the modules they write now. It was cool to hear about the pain they went though to figure out and learn what they know now. So I really like that one. Another I like is [a leveldb show](http://nodeup.com/fortyone), where Max Ogden and Rod Vagg and Paolo Fragomeni were talking about [leveldb](https://code.google.com/p/leveldb/). They went deep into it. I'd never been exposed to it before but the way systematic way they approached it really helped me understand it, and what it can be used for, and why you would use it over something like mongo. So those are two really good ones for me.

37:12 - **Erik Isaksen**: Ditto on the leveldb episode - I thought that was fantastic. Just listening to Rod was awesome. His voice was just great, too. I had never heard to leveldb before that. I just Rod put up on [nodeschool.io](http://nodeschool.io/) he has a commandline lessons for leveldb, which I plan on trying. Don't know if you guys have seen that.

37:47 - **Daniel Shaw**: Yeah, nodeschool.io is becoming a phenomenal resource. There's Learn You Node, there's leveldb, there's a new functional programming one -- I haven't had a chance to check that out -- and then of course there's the seminal work of substack and Max Ogden: Streams Adventure, which put that out as a format. It's been great to see all the support that it has provided.

38:30 - **Matt Creager**: I downloaded that one and was using it on the plane all the way back. Plus one on that. It's awesome.

38:40 - **Nizar Khalife**: I leveled up after completing the stream adventure, for sure.

38:41 - **Erik Isaksen**: The last episode you guys have Isaac's talking about streams and the different changes in the API. Prior to node, I hadn't really used streaming in anything. It's really cool stuff. You can get some really good performance.

39:03 - **Cliff Subagio**: There are places where Isaac's talking about streams. Talking about streams 1, streams 2, and streams 3. I think that gives a sense of direction of where node's moving and the core guys are really open about it. That's quite different from other podcasts in a way, and it's really useful to the users, knowing what's coming up and why, what's the reasoning.

39:37 - **Daniel Shaw**: That's right, this is an open-contribution platform. It's a of technical effort to dive into core because you'll quickly get out of JavaScript land and get into C++, so there's a little bit of a challenge there. But everybody is welcome to contribute on whatever level they feel comfortable. If you want to get started with just improving the docs, that's a great place to start. The entire stack is open to contribution. You'll need to sign the contributor's license agreement, but that's basically the barrier. That, and the amount of work that you'd have to put into understanding it enough to meaningfully make changes. You'll have to work on code that was written by people who've spent a couple of years deep into it. But even if you don't get your contribution landed, I would guess that the process would grow your understanding of node -- and potentially leveldb -- so much that the benefit to you and your career would be phenomenal.

All through the node community it's one of the strongest things that is a hallmark this sense of contribution. If you want to make an impact, if you want to change the way something's done. The best way to do it is by rolling up your sleeves and making a difference.

42:11 - **Matt Creager**: One thing this community really gets right is this focus on progression. I think Mikeal said in the community show, which is one of my favorites, that this feeling is anything can happen and anything is possible. That's what it feels like when you first start using node. You have these people who are really smart solving these really hard problems. And you're able to use this thing and build amazing stuff with it, and then the community onboards you and suddenly you're looking through core and then you're contributing to core. And people are encouraging you the whole way along. It's that progression that makes the node community so special. 

42:58 - **Cliff Subagio**: Can I add another favorite show? [Episode 19: our favorite modules](http://nodeup.com/nineteen). Where you guys talk about favorite modules on NPM. That helps with visibility of some of the modules. At the moment, I'm checking [npmjs.org](https://npmjs.org/) and there are almost 45,000 modules. That can be a bit overwhelming at times. You search npmjs and it comes up with ten recommendations and they look equally good, so you spend a lot of time figuring out which one really fills your need. But the modules recommended on that episode may not have an official blessing but at least it's a place to start. There's probably the trade-off of --- I've heard developers say a module is probably small enough that it's faster to build it themselves, rather than finding one module that serves their need. So it's a trade-off. But at the same time, reinventing the wheel is not necessarily bad if it can encourage people to experiment and come up with different ways to solve something. That's been really great within the node community -- you can find problems being solved in multiple ways.

44:45 - **Daniel Shaw**: That's a great point. If you look at the most-depended-on modules, that list is such a small surface area of what's going on. Express is a great platform and is used up and down by so many people but it really doesn't represent how to solve the more creative problems that node really excels at doing. That's an episode that would be really great to reprise.

45:35 - **Nizar Khalife**: But also I think if you get recommended a good module it will refine your eye for good modules. If you get exposed to a couple modules with great readme files and code examples, then you get better at recognizing them when you're doing random searches on npm. 

45:53 - and you learn to write them yourself

45:56 - **Daniel Shaw**: Speaking of really great readme files, Rod Vagg, again, my God. He is the master of the readme. 

46:04 - **Nizar Khalife**: I think he's the only one who's admitted on air that he likes writing documentation. 

46:09 - Look at his test folder, too. His test folder has just, so many tests in there!

46:17 - You can tell he really cares about the details and getting it right.

## Experimental Stuff

46:20 - **Daniel Shaw**: Okay, so did we get everybody? Alright, I want to talk real quick about some of the more experimental stuff that we've done. And really try to grind down some feedback. You know: things that work, things that don't.

But before that I want to thank our third sponsor: [Clock](http://clock.co.uk). Clock is a digital development agency based in the outskirts of London. They make beautiful websites and web-based applications. A special shout out to Clock for being such a great citizen that they gave up their [jsfest.com](http://jsfest.com/) domain and contributed that to Mikeal's latest conference project, JSFest. A huge shout out to them for that. Clock is great at integrating legacy systems and devices, and all these things that, in their own way, don't really want to be integrated. They have been excellent in the publishing, customer insight, and customer loyalty spaces.

They have developed a set of hardware devices for retailers to put in stores and venues that is built 100% on node. You can find out about that at [swipestation.co.uk](http://swipestation.co.uk/). Clock has been around since 1997 and have been building large-scale production node since 0.4. Since then, they've gone all-in on node and really have pushed to build almost everything they've been producing in node. So they're deep into development.

The front-end team works with Jade and Stylus, and I believe the entire team has to stop at 4:00 P.M. and participate in formal tea with crumpets. They are the creators of the incredible node bowler -- and bowler hat with an integrated Raspberry Pi that is node-based. So, absolutely fantastic. Their clients include the BBC, Newscorp, Nielson, Joyent, Eddie Izzard, Shortlist Media, and Hearst Media. They are a really fantastic company. The are on the lookout for developers, so if you're looking to work fulltime on node and contribute to open source, they are a great choice and I hope you reach out to them. You can find more about Clock at [www.clock.co.uk](http://clock.co.uk), you can reach out to them at [hello@clock.co.uk](mailto:hello@clock.co.uk), and be sure to follow them at [@clock](https://twitter.com/clock) on Twitter. Thanks again, guys.

50:16 - **Daniel Shaw**: So, we talked about a lot of the shows that worked. It is important to get out a lot of different voices. One of the show that I enjoyed doing most was [the promises show](http://nodeup.com/fortysix). That was something completely different and I think right before that, there was a bit of negativity around that. And we did that show and I think it contributed to dampening that sense that the people who are into promises were being ostracized and they didn't belong. And I really wanted to pull back away from that.

51:26 - It was really interesting at the time because I have this argument all the time. I'm pro promises -- I'll put that out there and say that publicly. But a lot of the guys at the office aren't. And we're building this product for client-side developers so I've really been preaching promises. When I first heard that episode I thought "Okay, so the node community as a whole rejects promises, I see." And then the next episode, when you brought them in, I thought that was an awesome example of what the community's all about.

51:56 - **Nizar Khalife**: Yeah, I enjoyed that show a lot. And I have a lot of respect for Domenic Denicola because he gets a lot of flack for the whole promises thing, with him being quote-unquote "the promises guy." It's nice to see a different side of the coin. Not everyone in the node community agrees 100% about what the APIs should be. So it's nice to see some people doing one thing and then the other perspective, too. 

52:26 - Yeah, that's what I loved about that show. It was a lot of religious battles back and forth. It was good to hear both sides of it, definitely. 

## A CoffeeScript Show

52:36 - **Daniel Shaw**: I've had -- for about the same amount of time -- a show that I've wanted to do similarly with CoffeeScript. But some of the contributors seem to fall down into proselytizing. What I want to highlight is the individual experiences and what works and what doesn't. The last thing I want to hear is why I should use CoffeeScript. I have evaluated that and I've made my own decisions. Anyone telling me about why I should do anything, e.g. pop the stack on that and get out of CoffeeScript and substitute anything in there. I want to do this show but I haven't found a group of people where we can really talk. I talked to Dominic a lot so I knew when we did that promises show that we'd really have a constructive discussion about the promises experience. You know: why Dominic believes it improves his experience and the developers there have found it useful. If anyone feels that they can help me make that CoffeeScript show a reality, I'd love to do it. I just haven't gotten the right feel on it yet.

54:27 - I had this experience. I started using CoffeeScript last year. And I heard you talk about it on the show a few times. I was like "You know what? Let's see what it outputs." So I look and it's pretty good. But I have to say, it's been pissing me off. It's so frustrating. It's like "This looks really pretty, but why are you breaking?" Especially in Rails, it doesn't even through an error, it takes you right to the haml where the erb says "Hey! Whatever." At least in my experience. So I'd rather just run the command line and do a watcher or something.

55:07 - That's interesting. Did you go from JavaScript to CoffeeScript?

55:10 - Yes. CoffeeScript for me? Right now? If I have to use it on a project, sure, whatever. But I'd rather only use it for tests, because my biggest win with that is getting rid of that `function`, and I can use that little arrow function now. In [Jasmine](http://pivotal.github.io/jasmine/), everywhere. But I hate using CoffeeScript on production now.

55:35 - I know at Trello they use CoffeeScript for their node stuff, so maybe those would be some good guys to get on there.

55:47 - **Daniel Shaw**: Right on. Yeah, we had --- from the Trello team on [the realtime show](http://nodeup.com/thirtyone) and his contribution was fantastic. My apologies for spacing on your name. I really enjoyed having them on the show. And if you are familiar with the contribute repo at [github.com/nodeup/contribute/](https://github.com/nodeup/contribute/). It's the area where a lot of shows are under development, and you can see some of the concepts we're working on. I invite everybody to also add new shows there. That would be fantastic. I always like adding new perspectives.

Speaking of new perspectives, I added a couple new concept shows this year and one of my favorites is [NodeUp Teams](http://nodeup.com/fortynine). We kicked it off with Andrew Sliwinski and the team at [diy.org](https://diy.org). They really get openness and sharing as part of their DNA. It was great to kick off with them. Getting that insight into what a large scale production app looks like: what are some of the challenges, what are some of the tools that work. An amazing tidbit that came out of that was the Restify and Bunion serializers that the diy team was able to set up to give them API playback in instances where they had problems under load. So if you haven't had the opportunity to listen to that show, go back and listen to it, there's lots of great things that came out of it. What do you guys think about NodeUp Teams and what other team would you like to hear about?

58:29 - **Nizar Khalife**: What really impressed me about the diy show was that it seemed like they were getting a lot shipped with a really small team. Not a lot of development resources, I would say. So it was really interesting to hear them talk about what they do to keep themselves productive, the makeup of the team itself. I think they take on some students and things like that. That was pretty awesome. It's tough, from the perspective of my team, to do internships but it seems like a weight we'd have to take on. Wed have to assume the front-loaded investment in time to bring people up to speed and all that, so I definitely respect them from doing something like that.

59:25 - **Daniel Shaw**: Cool! If you ever want to talk about running an internship program, I ran the one at Voxer, Summer of Node. It is a lot of investment in time, but what comes out of that? I really forces you to evaluate your onboarding process. It's a great time to do internships as you're ramping up hiring because you're going to need to do that anyway, so you can iterate with that and make it part of the competency of that team to build those resources. That seems to be the right timing. If you're really early in your startup experience, just five guys, it could be challenging. I've heard a lot of people say that at that point in their startups it was just too much. There was the attractiveness of the cost savings there (with interns) which is a bunch of bullshit. If you don't know what the mythical man month is, it's a bit of software engineering lore that is still valid today, from very early engineering at IBM. It still 100% applies.

Anyone else want to talk about NodeUp Teams? I'd love to hear which teams you'd like to hear from.

1:01:48 - **Cliff Subagio**: Sometimes I see articles on the net about "Hey, this company successfully migrated to node from some other stack." I think recently, Groupon did a rewrite and migrated to node. And Facebook Photos, as well, from F+. I think it would be great if those companies came and talked about it on NodeUp Teams. I think I had a similar experience to what Matt was saying, when he was getting pushback on adopting node. It's really one thing to pass along a link about someone saying they migrated to node but having the teams actually discuss their experience on a format like NodeUp Teams, I think it would really put some serious reasoning behind the argument. 

1:02:52 - Yeah, the evolution of the product, for sure.

1:02:55 - **Cliff Subagio**: Definitely. It's not just about the result, the success at the end. But the pain points, as well, along the way. So it's really real.

1:03:08 - **Nizar Khalife**: And just hearing what their recurrent workflow is in terms of the toolchain they use and all that. That's always really useful. I'm always on the lookout for little things like a module or command line thing that might make me more efficient or make me more productive. 

1:03:23 - I think it's interesting some of the companies that have adopted node, like Microsoft has its own open source out there, and Adobe is doing Photoshop plugins and I think Adobe Brackets uses it, too. 

1:03:36 - **Daniel Shaw**: Yep.

1:03:37 - That what I was going to suggest, to have the Adobe Brackets team. That would be an unbelievable team for the show.

1:03:44 - ditto on that one.

1:03:45 - **Nizar Khalife**: The open source side of those companies is relatively small. It might be cool to see their perspective from within a giant corporation.

1:04:00 - And how they moved from whatever their original stack was to their new stack. What that looks like. What were the benefits of their old stack compared to their new one? What were the advantages to using something like Python Tornado versus node? What did they like about that that we might be able to bring back into the node community and adopt.

1:04:20 - Yeah, what problems did node solve for them? 

1:04:24 - **Cliff Subagio**: Excellent! [The Node Firm](http://thenodefirm.com/) has been helping with the technical vetting of the node talks at the [Node Summit](http://nodesummit2013.eventbrite.com/) at the beginning of December. It's a very business-oriented conference. The most exciting part of what's happening there is the sheer number of companies of companies coming forward and sharing their experience. Groupon's a highlight. After the beginning of December, there will be many more and I look forward to tapping them and getting insight from those teams.

1:05:23 - Also the [Ghost project](https://ghost.org/). They would be nice to hear from.

1:05:28 - **Daniel Shaw**: Excellent. That's a great idea. I'm really excited about ghost. I haven't been greenlit yet, but I signed up and reserved my "dshaw" handle.

1:05:50 - I'll go on [Pair With Me](http://pairprogramwith.me) and see who's pairing online and there's hardly anyone there but Ruby is packed and all these other groups. And it doesn't have to be just there, but I haven't found a lot of pair programming resources for node. So I don't know if maybe we could promote that some more.

1:06:17 - **Daniel Shaw**: Excellent. We'll do that right now! 


---


1:07:31 - **Cliff Subagio**: I was going to ask if I can add some ideas on potential segments and concepts. First up I'm thinking of NodeUp X --- like TED X, where they have communities all over the world. And I'm totally interesting to know what's happening with all these different communities. The other thing is the non-English-speaking countries. I think a few months or maybe a few years ago there were some events in Korea or Japan  

1:08:42 - **Daniel Shaw**: Let me riff on that real quick. If you do start a podcast and the core group also speaks English, I would like to help kick that off by having your podcast jump meta, and we'll talk about that on NodeUp.

1:09:07 - **Cliff Subagio**: The other thing I liked about the [binary compatibility episode](http://nodeup.com/fiftytwo) is when Rod was talking about whether to put something in core or in user land. That made me think of a "NodeUp Smackdown" segment, like a friendly competitive discussion on why you did this or why you did that. It doesn't have to be a right or wrong thing, but to know the reasoning behind the speaker's perspective really helps us learn a lot about all these different approaches. That will encourage more and more good things in the end. 

1:09:49 - First one will be CoffeeScript, right?

1:09:56 - **Daniel Shaw**: Ha! But no, I want to do CoffeeScript by CoffeeScripters, first. Maybe after we do that, then we can go back into the smackdown.

1:10:09 - **Nizar Khalife**: You can make those into a drinking game.

1:10:13 - **Name**: Point for CoffeeScript! Take a shot.

1:10:20 - **Cliff Subagio**: The third idea I was to raise is some sort of a NodeUp community public service announcement. Maybe the podcast can take suggestions from the community on things that will benefit the community overall. If I can start with the first one: I would like the raise the fact that there are actually hundreds of modules in npm with github as a dependency. That in turn causes lots of problems when github is down and it's been down a couple times recently. I have a local npm registry where I work and the --- it's supposed to be useful when, say, central is down --- central is stable, my local npm is stable but when github is down there is nothing I can do, really. Lots of modules still depend on github.com. To be clear, that's when someone specifies a github.com URL in the json dependencies. I ran some scripts to analyze the existing registry and there are about 700 modules where the latest version still depends on github.com. --- encourage if possible -- I think we should publish those modules to the npm registry, o at least beg the authors to. Because there are all the other modules that depend on those 700 modules and on and on and on. So that change would be awesome, if it's possible.

1:12:19 - **Daniel Shaw**: Frequently those are forks of other codebases that are blocked upstream because the upstream author hasn't updated, or it can't be updated. That's really fantastic feedback. Especially coming from Australia, where the Internet is slow. I know Dominic and Rod have been doing creative things to make that better. But yeah, the dependency on github and the impact of having those module references in github trickles down. That's amazing.

1:13:13 - **Nizar Khalife**: On that idea of the public service announcement, what I think would be really cool would be more ways to that the community can get directly involved. I've heard that in specific projects that need some love, or need a maintainer, or whatever. It could be things like that but also just different ways that we could help you out with the show. If you want to single out a specific show -- like the CoffeeScript for CoffeeScripters show -- if you need help finding people or suggestions for that. Sometimes it's difficult for me to look at the entire world of open source and see what I can do to help, but if somebody were to directly ask me for help, then it would be a lot easier.

1:14:10 - **Daniel Shaw**: Yeah! I've been looking for the best way to address this. Something that I'd really like to do is set up an intern kind of a thing. Someone who would help me with doing that. You know, queuing up the shows and getting everybody on board. Making sure everyone's still available and having a show go off is a considerable amount of my time. If anyone's interested in doing that -- if you're interested in doing that. Yeah! Yes! Realize what you're getting into, though: it's a fair amount of work.

1:15:13 - **Nizar Khalife**: I'm not sure if I want to be the --- in this case. 

1:15:22 - Did you just sign up to become a personal assistant?

1:15:26 - That sounds horrible, doesn't it?

1:15:29 - We can definitely crowdsource a lot of this stuff and help them individually, wherever we can, for sure.

1:15:35 - **Nizar Khalife**: And not just on the show. There are a lot of community leaders that are just overwhelmed with things to do. And maybe a package that everybody uses, suddenly there's no time to maintain it. In those cases, the community's there and a lot of people listen to this. Whether or not they say so, there's a lot of people exposed to NodeUp and they follow everybody on Twitter, so they're responsive to cries for help.

1:16:10 - **Daniel Shaw**: My concern with the pure crowdsource is that it would still require a fair amount of curation, right? 

1:16:24 - **Name**: Yeah, someone has to take ownership, for sure.

1:16:27 - **Daniel Shaw**: Someone has to take ownership of that, so I think if we want to go beyond the NodeUp intern and find someone who's interested in kicking off that community crowd curation. That's something. And you'd have lots of contact with the node community. To pitch this, it's really an incredible opportunity to get in touch and to meet and personally get to know members throughout the node community. So if you're interested, hit me up and let's talk. 

So, I think Erik has to dash soon, and we're about ready to wrap it up. Guys, if you haven't had an opportunity to prep your plug, we're going to do that in a moment. Final shout outs: both Nizar and Matt want to reemphasize realtimeconf and the realtime experience. I'll let you guys say it in your own words.

1:18:03 - **Nizar Khalife**: Yeah, I really want to thank everyone at &yet and everyone else not at &yet who contributed to the whole experience. It was absolutely amazing, it blew me away. It was my first conference and I really liked how it's not just pedal to the metal. It was definitely something greater than just tech, just coding, just a conference. It was something much larger than life in that sense. I met a lot of the &yet team - they're really awesome. And the actors, the musicians, everyone who helped make that happen deserves some praise because it was amazing. Matt?

1:18:59 - **Matt Creager**: I just wanted to say that &yet and realtimeconf were absolutely incredible and I just kind of wanted to -- she'll never hear this, but -- there was a moment where a person did a solo cello performance and she sang this a song that she'd written herself -- this is Oletta Henderson who played Ross in the play that played out. And three people at my table were in tears. I won't tell you if I was one of them or not, I was just at a development conference. 

1:19:40 - **Nizar Khalife**: And she's quite the looker, too, by the way.

1:19:43 - **Daniel Shaw**: Yeah, a beautiful song that she composed just for realitimeconf. Go back to the realtimeconf stream and have a look at that. A phenomenal artist and has quickly become a participant in the node community. And we're really grateful for her involvement there. 

## Plugs

Alright! So, it's that time. Time for plugs. Erik, you want to go first?

1:20:44 - **Erik Isaksen**: At [3Pillar Global](http://www.3pillarglobal.com/), we're hiring for a lot of UX positions. A lot of different positions. We're growing offices in India and Romania, so if you're looking to work on really cool stuff like node, web components, Angular, then definitely Skype me or get me on Twitter at [@eisaksen](https://twitter.com/eisaksen). And I'll see if I can set you guys up. Definitely for any UX design, also. Anyone who'd like to pair, I've recently been inspired by a local developer here, Brian McGreary and his company. Every day he does an open source commit. It's crazy! So I'm trying to do more work on github. I just started that recently, working on some Angular stuff with this other developer, Chris Smith. We're doing ng-dropbox and ng- as the main repositories. If you want to join let me know.

1:21:50 - **Daniel Shaw**: Fantastic, thank you! Nizar?

1:21:56 - **Nizar Khalife**: I'd like to plug the company I work for, [Nobox](https://www.facebook.com/Nobox). We're also hiring. We're always looking for developers. We're based in Miami and we also have office in Puerto Rico. So if that sounds like something you'd be interested in working with big brands in Latin America like Playstation. If you're interested in that definitely hit me up on the Twitters @[khalifenizar](https://twitter.com/khalifenizar). Another thing I really want to plug is I'm helping organize a node meetup here in South Florida. It's called [NodeJS Enthusiasts of SouthEast Florida](http://www.meetup.com/NodeJS-Enthusiasts-SE-Florida/). If you're interested, I'd say we're in formation. It's me and this great guy Juan Lopez, and we're organizing this thing. So if you want to head up to that or you want to talk about whatever you're working on that would be wonderful, so please let me know if you're interested.

1:22:54 - **Daniel Shaw**: Fantastic! Matt?

1:22:55 - **Matt Creager**: I should start by giving a shout out to the startup incubator for letting me take over their offices for this podcast. And to GoInstant for giving me a place to play with node all day and pretending it's work. I'd like to plug a recent open source Angular project that I've just launched. It's called [GoAngular](https://developers.goinstant.com/v1/GoAngular/index.html). It's a GoInstant and AngularJS integration, so if you're into building multiuser realtime applications with Angular then you should check that out. And GoInstant is of course hiring, so if you're in the Halifax area and you're a node developer, I'll be pretty surprised if I don't know you, but hit me up at [@matt_creager](https://twitter.com/matt_creager). And also I'd like to plug NodeUp for just generally kicking ass all the time. And if you're not listening to NodeUp then you should be.

1:23:48 - **Daniel Shaw**: And you probably are if you're hearing this right now! 

1:23:53 - **Matt Creager**: Go back and listen to all the NodeUp episodes right from the beginning, if you haven't.

1:24:00 - **Daniel Shaw**: Cliff?

1:24:02 - **Cliff Subagio**: I'd like to plug the [Melbourne NodeJS Meetup](http://www.meetup.com/MelbNodeJS/). The next meetup is actually in thirteen hours. I don't know if there is any Australian listening live at the moment. Another one I'd like to plug is the Australian Polyhack crew - we're #polyhack on Freenode. We're talking about mostly node but there are other things like Go, Erlang, and other good stuff. 

1:24:37 - **Daniel Shaw**: Cliff was up at 4 A.M. He was up late so if you're at the meetup and see him, give him a hug because he's representing the community. I'm going to my plug for [The Node Firm](http://thenodefirm.com/). They provide strategic consulting, training, and support for business, enterprise, and Fortune 1000 companies. They've been instrumental in saving some very large high-profile projects and getting them back on track through strategy, code review, and execution planning. So if you're building node and your business or team needs help, then please reach out to The Node Firm.

Alright, thanks guys. Thanks to Erik, Nizar, Matt, Cliff. Thank you all for joining us for [a very meta NodeUp](http://nodeup.com/fiftythree). I hope everyone enjoyed this show and this chance to reflect on where we are, what we've gone through, and talk about how we can do better in the future. I invite everyone to leave a review on [iTunes](https://itunes.apple.com/us/podcast/nodeup/id447667314?mt=2). It helps bump up our relevance, and people searching for node on iTunes will find us through that. Even if you don't listen to NodeUp on iTunes, we'd appreciate it if you click through there and subscribe. It's an important ingest point. Follow [@nodeup](https://twitter.com/nodeup) on Twitter. Right now, our sponsor slots are full, but please reach out to [nodeup@gmail.com](mailto:nodeup@gmail.com) if you want some more information about sponsoring NodeUp in the future. Thanks again, guys, it was a great show and great to have you. 



