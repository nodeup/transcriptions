24: A Secure Show
===

Panel:

* Daniel Shaw
* Mikeal Rogers
* Charlie Robbins
* Matt Ranney

Table Of Contents:

1.[Introduction](#introduction)
2.[New Node Releases](#new-node-releases)

## Introduction

Mikeal Rogers: Hello, welcome to NodeUp, episode 24. I'm Mikael Rogers. We've
 got Daniel Shaw on the line, Matt Ranney on the line, we got Charlie Robbins
 on the line, and we got mixmax (craig) on the background, checking out the
 levels. This is our first show on Google Hangouts. We wanted to thank ... and
 google for making it work right. Alright, let's get started with the show! Oh
 yeah, and we got some great sponsors: We've got Geeklist coming in for the
 first time today and Clock will stand by, we'll talk more about them later.
 Let's go on with the show. There were some Node releases. Do you guys want to
 tell me about that?

## New Node Releases

Daniel Shaw: So, there are plenty of new Node releases out. 0.8.3, 9.0, and a
 maintenance release for 0.6.20. Lots of good stuff. If you're holding off on
 upgrading to Node 0.8, now is definitely the point where you should be
 upgrading your systems to 0.8.3. Mikeal, have you upgraded to 0.8 yet?

Mikeal Rogers: Yeah. All of our production stuff is on 0.8. In fact, a bunch
 of deployment stuff fell over and a lot of things are hand-rolled again
 because of that. I really needed Domains, really bad. I really needed
 exceptions to not bring down the process that would just 500 the taco request
 for that. I tooled those in and we're testing them now. They're working pretty
 well.

Daniel Shaw: So Mikeal, what broke? What in 0.8 did not work right?

Mikeal Rogers: I think what it is, something in either propogate or pushover
 isn't working. I talked with Isaac and Substack about it. What we think it is,
 is that there's a lot of different subprocess calls. There was a subprocess
 event called 'exit' that used to happen, it used to be ensured that it would
 happen after stdout and stderr were done, and now it's not. So that could fire
 shortly before all of the output has ended. What you actually need to listen
 to is 'close' now. Hopefully, that's a bug and we can get it fixed.

Daniel Shaw: Charlie, are you guys on Node 0.8 yet?

Charlie Robbins: That's a good question. We are 0.8 in installations. Our
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

Daniel Shaw: What percentage of your users are still on 0.4?

Charlie Robbins: Very small. But to openly say "We don't support this thing" is
 a non-trivial thing for us to do as a company.
