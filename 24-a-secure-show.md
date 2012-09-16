24: A Secure Show
===

Panel:

* Daniel Shaw
* Mikeal Rogers
* Charlie Robbins
* Matt Ranney

Table Of Contents:

1. [Introduction](#introduction)
2. [New Node Releases](#new-node-releases)

## Introduction

**Mikeal Rogers**: Hello, welcome to NodeUp, episode 24. I'm Mikael Rogers. We've
 got Daniel Shaw on the line, Matt Ranney on the line, we got Charlie Robbins
 on the line, and we got mixmax (craig) on the background, checking out the
 levels. This is our first show on Google Hangouts. We wanted to thank ... and
 google for making it work right. Alright, let's get started with the show! Oh
 yeah, and we got some great sponsors: We've got Geeklist coming in for the
 first time today and Clock will stand by, we'll talk more about them later.
 Let's go on with the show. There were some Node releases. Do you guys want to
 tell me about that?

## New Node Releases

**Daniel Shaw**: So, there are plenty of new Node releases out. 0.8.3, 9.0, and a
 maintenance release for 0.6.20. Lots of good stuff. If you're holding off on
 upgrading to Node 0.8, now is definitely the point where you should be
 upgrading your systems to 0.8.3. Mikeal, have you upgraded to 0.8 yet?

**Mikeal Rogers**: Yeah. All of our production stuff is on 0.8. In fact, a bunch
 of deployment stuff fell over and a lot of things are hand-rolled again
 because of that. I really needed Domains, really bad. I really needed
 exceptions to not bring down the process that would just 500 the taco request
 for that. I tooled those in and we're testing them now. They're working pretty
 well.

**Daniel Shaw**: So Mikeal, what broke? What in 0.8 did not work right?

**Mikeal Rogers**: I think what it is, something in either propogate or pushover
 isn't working. I talked with Isaac and Substack about it. What we think it is,
 is that there's a lot of different subprocess calls. There was a subprocess
 event called 'exit' that used to happen, it used to be ensured that it would
 happen after stdout and stderr were done, and now it's not. So that could fire
 shortly before all of the output has ended. What you actually need to listen
 to is 'close' now. Hopefully, that's a bug and we can get it fixed.

**Daniel Shaw**: Charlie, are you guys on Node 0.8 yet?

**Charlie Robbins**: That's a good question. We are 0.8 in installations. Our
 production stuff, the stuff that's actually running the other node processes
 is still 0.6. Beginning on August 1st, when the second part of our transition
 to Joyent happens, we're dropping Node 0.4. This is just my fault for listening
 to Ryan [Dahl] when he told me that IPC would be a stable API, which,
 apparently, it's never going to be. We use IPC to monitor your application
 and to deterministically find out when the server has actually started. So,
 we sort of monkey-punch net.server.\_doListen and we say "oh, well if that
 port isn't available, listen on the next port. and when you actually get a
 port and you're bound to it then just inform your parent that you have a port."
 This has been the bane of our existence, really. Because everyone else,
 every other platform will say "Hey, listen on this port, we're gonna tell you
 what your port is, listen on this port", where as we say "Hey, you tell us
 what your port is and we'll let you listen on it. Listen on any port." We're
 going around this, so having a 0.6 process talk to a 0.4 process, having a
 \0.8 process talk to a 0.6 process, so on and so forth. So, 0.8 [talking to]
 \0.4 is just not happening. We're just cutting that altogether. We're going
 sort of a different route with IPTables that will eliminate the need for that
 bit of code altogether. But, until that happens, we're temporarily dropping
 \0.4.

**Daniel Shaw**: What percentage of your users are still on 0.4?

**Charlie Robbins**: Very small. But to openly say "We don't support this thing" is
 a non-trivial thing for us to do as a company.

**Matt Ranney**: At some point you will get too large where you can never say
 this.

**Charlie Robbins**: Right. We're trying to get [away from 0.4] early. 0.4 [and]
 0.6 was a nightmare because the 0.4 stuff actually added C stuff to node, so
 we had this other library that brought in a macro called NodeFork, which was
 basically that C stuff pulled out into a module that compiled for 0.4 or 0.6.

**Daniel Shaw**: Wait so, when you say that the IPC stuff changed, you mean that
 the child process API stuff changed?

**Charlie Robbins**: The .fork APIs, yeah. In 0.4, .fork didn't exist. In 0.6,
 .fork existed, and in 0.8 there's some internals in libuv that are unhappy
 with that. Having a 0.8 process talk to a 0.6 process doesn't really work. And
 this is outside of the test scope for most people because they're like "Oh,
 well it talks to itself so that's fine." Right? But the backwards compatibility
 of IPC is actually-- I think it's a more serious problem than other people do.
 But.. what can you do?

**Matt Ranney**: It's arguable that it's only serious if you're a Node service
 provider.

**Charlie Robbins**: Think about it this way. If you have... I guess IPC doesn't
 happen over the network. But if it happened over the network, you could think
 that would have that service written in 0.6 and another service is written in
 0.8, but at the point we're using the network anyway, so.

**Daniel Shaw**: And that API has been pretty good.

**Charlie Robbins**: So the short answer is we're dropping 0.4 next week and
 0.8 is going to come along with it. Along with all of the rest of our users
 who are still on Rackspace.

**Daniel Shaw**: Cool. We have not upgraded to 0.8 yet, in spite of all of us
 wanting very much to do so. We have just gotten too big and too complex. Making
 a major move like this requires a lot more testing and validation of our
 infrastructure. Any time now, we're gonna pull the trigger on that, but it's
 probably at least a week or two out.

**Charlie Robbins:**: I'm really curious how you guys do that. Do you guys set
 up like a forward proxy and then test a subset of your traffic along new
 infrastructure to make those changes, or do you just hope to God it works and
 press the button?

**Daniel Shaw**: Well, it's funny you mention that. We, until recently, we
 pretty much did the second one, which is just like try it out on one, see what
 happens, and then slowly roll it out on more and more. Look at the graphs,
 look at the logs, make sure it seems like it's working. Then, roll it out to
 the rest of the system. It causes too many fire drills, and too many surprise
 emergencies on weekends. It's too stress-inducing of a way. We're building a
 more elaborate validation framework that will sort of exercise the system
 constantly. Kind of like, run all the things that all clients would do,
 and try to poke around at the edge cases, and just kind of leave that running
 24/7.

**Charlie Robbins**: So it's your own, what do they call it at Netflix? The evil
 monkey or something?

**Matt Ranney**: It's not chaos monkey, it's order monkey. It's like, just do
 normal things and see if they still work. And yeah, maybe eventually we'll
 get to chaos monkey where we can actively break things until we know they work.
 We have a ways to go until that though.

**Daniel Shaw**: It's not throwing food yet, just throwing nice things.. and us.

**Mikeal Rogers**: So there were some other releases too. We had a maintenance
 release of 0.6. For everybody who's still on 0.6, this is probably really nice.

**Daniel Shaw**: Actually, we totally ignored it. (*laughts*)

**Charlie Robbins**: I'm sure that was, again, also for us. We had a bunch of
 users who were still on 0.6 that, the latest version of npm that gets installed
 with 0.6 was crashing because if you didn't include a README in your package.
 Which applications often don't do. Isaac had already fixed the bug in one of
 the libraries NPM depends on, but because we were still on 0.6.19, and we
 weren't running the newest NPM with it, that was kind of the impodence for
 that release as well.

<!-- Continue at 9:30! -->

