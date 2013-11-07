46: A Promises by Promisers Show
===

Panel:

* Daniel Shaw
* Domenic Denicola
* Jeremy Stanley
* Andy Wingo

## Introduction

Hello, welcome to NoedeUp, this is Dshaw.  Today I'm joined by Domenic Denicola, Jeremy Standley and Andy Wingo.

We're going to be talking about promises and practice in the real world.  It's a bit of a promises redemption podcast.  The first podcast to which Michael Rodgers was actually not invited.  Our sponsor today is &yet;

So, Domenic is a Promises/A+ co-editor and the adoptoer of all lost npm pupies in the world.  If you need someone to maintain your npm module, please ask domenic.  

Gets stretched thin, but sometimes it's irresistable.

He needs a new project.

Jeremy is the author of sheppard and obvious medium is a fully promised shop and excited to hear more about how that's working at medium and what's been the real world experience in rolling out a significant production service using promises.

Finally, andy wingo is a compiler/hacker and he's going to be playing the role of Slavour today.  V8 committer and schemer and going to raise the technical level significantly.

## Node Core Promisees

At JSConf I asked Domenic to go in and fill in the blanks between what Ryan did in node core with promises and where we are today with Promises/A+ and how it's evolved since then.

I was not arround for node 0.1 when promises were in node.  I guess that really should be "promises" in scare quotes because what I've really were, from what I've gathered in the API docs and talking to people is event emitters with two events, success and fail.  I think there was also some crazy thing that was in there for a while where you can call "wait" and it would synchronously wait for the success event or the error event to fire, and that was wierd.  Nobody like it from all I hear.  I don't know when Dshaw or any of you got involed in node.

Yeh, I never worked with it.

An event emitter is not a promise.  An event emitter has a lot of properties that are way too much power for a promsie.  A promise is supposed to just supposed represent an asynchronous function call or an asynhchronous operation.  So it has properties like you can only call it once and it can only either return or throw an error, it can't do both.  Things like the producer gets to return the control value and the error but the consumer doesn't get to say "oh, I'm gonna emit an error event".  All this flexibility that event emitters have is perfect for events, but it's a really bad match when you want to do a single asynchronous operation.

So the pattern that has been standardised over the last few years under the name of promises in user space has been organised under Promises/A+ which is this spec that I co-edit.  That really nails down what it means to be a promise in JavaScript at a level that isn't just an event emitter with two events.  It's more like an object that follows certian rules and has a way of registering callbacks, but behaves in a very predicatable way.

In your oppinion, if node had continued down that path, would we have gotten to A+.  It's matured a lot since then, and so have promies.

I don't think so, I think the desire to build on the event emitter technoloyg would've been a trap.  At the time that node 0.1 came out, there was a lot of work on CommonJS Promises/A which was a predecessor to A+.  It was well understood how promises should work.  Talking with Kriskowal who was one of the early promise implementers.  It's just a matter of which communities understood which technologies and node understood event emitters but they didn't really understand promises so when they were like "hey a promise is just something that succeeds or fails, lets do that in terms of event emitters."  I think it would've been painful and nobody would've liked it ever.

Possibly worse than where we are now.

Definitely worse I would say.

Conceptually filling in the blanks.  If core were to be more promise friendly, what would that look like.

There's actually a really easy way to introduce this.  As with all promise funcitons, instead of passing in a callback that recieves an error or result.

## 5:30
