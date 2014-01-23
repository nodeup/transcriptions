[57: A Docker Show](http://nodeup.com/fiftyseven)
===

Panel:

* [Daniel Shaw](https://twitter.com/dshaw)
* [Nuno Job](https://twitter.com/dscape)
* [Mike Brevoort](https://twitter.com/mbrevoort)
* [Niall O'Higgins](https://twitter.com/niallohiggins)
* [Jacob Groundwater](https://twitter.com/0x604)

Table of Contents:

1. [Introduction](#introduction)
2. [Why Docker is Meaningful](#why-docker-is-meaningful)
3. [Docker in Open Source](#docker-in-open-source)
4. [Testing with Docker](#testing-with-docker)
5. [Orchestration and Docker Linking](#orchestration-and-docker-linking)
6. [Docker Concepts and Terminology](#docker-concepts-and-terminology)
7. [Docker in 6 to 12 Months](#docker-in-6-to-12-months)
8. [Plugs](#plugs)

## Introduction

00:17 - **Daniel Shaw**: Hi, welcome to 2014! Welcome to NodeUp 57: A Docker All The Things Show. I am joined today by Nuno Job, Mike Brevoort, Niall O'Higgins on the craziest setup in the world -- he is connected on a telephone through Nuno's laptop in London and Niall is in Mexico -- it's nuts, but we're gonna do it anyway. And Jacob Goldwater, last but not least.

00:52 - **Jacob Groundwater**: Groundwater, buddy!

[Laughter]

00:53 - **Daniel Shaw**: Oh shit, alright! 

00:57 - **Nuno Job**: What did you call Jacob?

01:01 - **Jacob Groundwater**: Goldwater!?

01:03 - **Nuno Job**: "I like goooooold!"

01:06 - **Jacob Groundwater**: That's not too bad.

01:09 - **Daniel Shaw**: Thank you, Jacob!

01:11 - **Jacob Groundwater**: Yeah, no problem!

[Laughter]

01:12 - **Daniel Shaw**: So, today's sponsors are [Clock](http://clock.co.uk), [&yet](http://andyet.com), and [Modulus](http://modulus.io). And I'm Dan Shaw, I run [The Node Firm](http://thenodefirm.com/). Let's go around the horn and let everyone introduce themselves before we get into dockering all the things. Mike, you want to kick off the blurbs?

01:32 - **Mike Brevoort**: I'm Mike Brevoort. I work at Pearson. Working to innovate and create and deploy our next-gen products globally. We've been using node for a little over three years there. 

01:43 - **Daniel Shaw**: Awesome! Niall?

01:44 - **Niall O'Higgins**: Hey, I'm Niall. I'm the founder of [FrozenRidge.co](http://frozenridge.co/). We do node software development. I'm also the primary author of [StriderCD.com](http://stridercd.com/), an opensource continuous deployment platform written in node. And if I don't sound very good on this call it's because I'm currently continuously deploying myself around Mexico. 

02:06 - **Daniel Shaw**: Jacob? Mr. Groundwater.

02:10 - **Jacob Groundwater**: Yes, Jacob Goldwater here. I work at New Relic. I work on the node agent there. Also, in my spare time, I work on [NodeOS](http://node-os.com/blog/get-involved).

02:20 - **Daniel Shaw**: Nice.

02:21 - **Nuno Job**: Hey, Nuno Job here. I used to work for Nodejitsu, where I built the first continuous deployment there, actually. I wrote some of the stuff that you might have read on docker. And I'm currently working on a super-stealth startup called percent, which you can see online so it's not very stealth. I'm the creator of LXJS and financing myself through consulting. 

02:40 - **Daniel Shaw**: Awesome. So let's fill in a little bit of context around docker. But before that, let me give a shout out to our awesome sponsor Clock. Clock is a digital development agency based in the outskirts of London. They make beautiful websites and web-based applications. They're great at integrating legacy systems, devices, and all the things that really don't want to be integrated. They are experts in publishing, customer insight, and customer loyalty. They have developed hardware devices that retailers have put into stores and venues. It 100% runs on node.js, it's called SwipeStation -- you can learn more about that at [swipestation.co.uk](http://swipestation.co.uk/). They've been making websites since 1997, they've been building node since 0.4, and since then they've fallen in love and gone all-in on node.

Their clients include BBC, Newscorp, Nielson, Joyent, Eddie Izzard, Hearst Media. Fantastic company. A couple of their projects are [NeverUnderdressed.com](http://www.neverunderdressed.com/) -- a high-end online fashion magazine. SunPlus is a access-controlled loyalty platform for the Sun newspaper -- that's at [perks.thesun.co.uk](http://perks.thesun.co.uk). And Sunday World, Ireland's biggest tabloid at [SundayWorld.com](http://sundayworld.com). They are the developers of the Node Bowler, a bowler hat with some really cool hardware hacks. Have a look at [clock.co.uk](http://clock.co.uk). Get in touch with them at [hello@clock.co.uk](mailto:hello@clock.co.uk). Be sure to follow [@clock](https://twitter.com/clock) on Twitter. Send them a message and say you heard them on NodeUp, and thank them for supporting node.

## Why Docker is Meaningful

04:33 - **Daniel Shaw**: So let's fill in the context of what docker is and why it's meaningful. And why it's transforming deployment, not only in node, but across the developer ecosystem. Niall, you want to start us off there?

04:54 - **Niall O'Higgins**: Sure, I can talk about docker and why it's important. I guess the key thing, first of all, is that it's built on [LXC](http://en.wikipedia.org/wiki/LXC) or Linux lightweight containers. It's kind of like a chroot -- if you're familiar with Linux system calls -- on steroids. It's used most notably at Heroku and by the guys at DotCloud, who became docker. They built their Platform as a Service on top of this stuff. And one of the big advantages of it over, say, traditional VM-based heavy-weight virtualization is that it's all done by the kernel itself. So you're not running multiple kernels, it's not using a ton of memory, it's all a single kernel image.

One of the advantages that gives you, actually, is that you can run it in most cloud providers. So you can run docker inside of EC2 or Rackspace or Joyent or whatever. And you can slice up those virtual instances using Linux containers quite easily. So that's LXC in a nutshell.

And you could describe docker as a very nice interface around LXC. I think you could say LXC is pretty rough around the edges; the userland tools have been known to contain bugs and so on. And docker, at a high level, encapsulates that very nicely. The docker folks, from all their experience at DotCloud, figured out a lot of those gotchas and work around them for you. So at a high level, docker is some really nice tooling around Linux containers. 

06:47 - **Daniel Shaw**: So how does that compare to a SmartOS zone or something like that? Is it conceptually similar?

06:53 - **Niall O'Higgins**: I think you could say it's analogous to a SmartOS zone. LXC is probably not as cleanly architected, maybe, as SmartOS zones, but I think conceptually it's very similar. And indeed there's no technical reason I know of why you couldn't also have docker backed by SmartOS and ZFS, rather than LXC and aufs or whatever other filesystems you're using in Linux. So I think in theory docker could run on both SmartOS and Linux. Although right now it's just Linux. 

07:35 - **Daniel Shaw**: So right now is it primarily just the API? And LXC is the real meat of what's happening, or is it conventions? Why is docker exploding?

07:48 - **Niall O'Higgins**: Well, one of the really nice ideas behind docker is it uses aufs, which is a copy-on-write filesystem. Which essentially means that you can build up images as a series of layers. So you can layer images on top of one another. For example, you can take a base image, which might be Ubuntu LTS or something like that. You can use that as your base, build whatever userspace tooling you need on top of that, say just an nginx server or node. And essentially this ends of being a series of diffs. It's pretty cheap to maintain diffs to the base image because of the copy-on-write filesystem. And there's a bunch of nice conventions around that.

For example: sharing these images in kind of a graph-like way similar to a version control system such as git -- there are a bunch of similarities there. So it's a really nice system for building portable binary images which can run on other docker systems. You can ship them around as if they were a shipping container. That's kind of the metaphor or analogy the docker folks use.

09:05 - **Daniel Shaw**: So what's the difference between a container and a VM?

09:10 - **Niall O'Higgins**: A container is lightweight virtualization with a shared kernel with a shared kernel. Whereas, a VM typically has a hypervisor at a level above the operating system. So in a VM system you're actually going to have multiple instances of the kernel running and they're completely separate systems, which also means there's a lack of transparency. There's a bunch of memory overhead there, also. Whereas with the docker or LXC lightweight container approach you only have one OS kernel running and the kernel is performing the virtualization for you. So really, a docker container is just unix processes with a bunch of what's called namespacing around it, essentially. They're just like any other unix processes, but the OS is adding some additional security and isolation there.

10:11 - **Daniel Shaw**: How robust is that security? If you're running that in your system, do you have strong security or some lightweight security that's easy to subvert? If we gave Adam Baldwin a docker container, is he gonna get out of that container? Or is he going to be well-contained in that?

10:40 - **Niall O'Higgins**: With the one caveat that I believe it is not safe to give people root access within your containers, I believe it's safe. That is the security model used by Heroku and others. So I think it's pretty battle-tested in production. But wit the caveat that you don't want to be running stuff as root or giving people access to root processes within docker containers. But I think otherwise you're pretty safe. 

## Docker in Open Source

11:08 - **Daniel Shaw**: Excellent! So, Nuno, Mike, and Jacob? Do you guys want to add any additional information about your digesting of what docker is and why it's meaningful?

11:22 - **Jacob Groundwater**: Sure. This is Jacob, here. I tried LXC containers for a bit, before trying docker. The biggest thing that I liked as something that was going to be open source was that I could push my docker images to the docker index. Which I think is a very important part of the project. So if I build something up in docker, I can push the layers -- kind of like doing a `git push`, where it sends your objects -- I can send those to the docker index and then someone can do a `docker pull` and pull down the exact container as I made it. And run it. 

12:00 - **Mike Brevoort**: To add to that, when you build up a docker image you may install some packages and some dependencies, right? So for example, if you need to build node and want node running in your container, you would pull that down and build it. Since your container has isolation, that's running in isolation within the container that's spawned from that image. That means you don't have to worry about running conflicting versions of node and how to handle that with something like nvm or something else. You just need to install node and it runs in your container. When you want to upgrade your application you would build a new image with a new version of node and you'd just run that container. And that goes for all other packages as well. You have these docker files where you define all these dependencies that get bundled up when you build the image. It eliminates some of the need for using tools like Puppet and Chef because you've got this image that's all self-contained and doesn't impact anything else. So that isolation, in and of itself, makes things much more portable and able to be run with other containers on larger docker hosts. Or to be able to be run Vagrant locally or anywhere else.

And like Goldwater said, you can publish those to the registry. There's a public docker registry. When you push something to the registry it's very similar to when you push something with git, as well as when you pull. You do it on a diff basis, so if you make a change at the bottom of your docker file and you pull that, you only pull the diff from the last diff place that was cached. So if you're deploying the same application on a docker version that all uses the same base, you're not copying around this giant VM file like you might if it included a snapshot of a VM or like an Amazon AMI. It's just the diff, which makes it really efficient. 

14:12 - **Daniel Shaw**: That is compelling. Having that entire virtual environment is fantastic, but the sheer size of those things just makes it prohibitive, especially if you're bringing up a brand new instance. There's the spin-up time and there's the time to get that in place. So this is definitely compelling. You mentioned, Mike, that there's a public registry, which is awesome. But you also have an internal one, right? So you can have the images that you're not only sharing with the world, but you can have this library of internal "private cloud" instances as well, right?

14:54 - **Mike Brevoort**: Yeah, the docker registry project is open source and the production version is meant to be backed by an S3 bucket. Which makes it really easy to run, really easy to scale. It's just sort of turn-key. Because your instances that run the registry themselves are basically stateless and if they disappear and you spin a new one up you just bind it to the same S3 container. As well as if you want redundancy. And in some cases we have this strange case where we have different environments -- like a dev and staging and prod environment in different VPCs at Amazon. They can't cross-talk to each other; they're on totally separate networks but they can talk to the same S3 bucket. So to get around that at the moment we have registries running in each, that are bound to the same S3 bucket so you can publish to one and pull from another.

It's really easy to run that project, super easy to set up, and even to run locally as well. The only challenge is that the index itself is isn't open source; the actual docker index where you can search for packages isn't. So we don't have a great solution right now in terms of searching for what images have been published to that registry. We're working on something internal for that. 

16:17 - **Nuno Job**: I think something that has not been covered so far is the fact that one problem we have with VMs is that they take a while to start up. So it's fairly hard to do things like testing. If you're running a testing cloud you have to wait for a VM to come up or provision a pool of resources up ahead just to run the test. Then if you actually want to clean it up, it takes a lot of time. Docker is really meant for things where you can run very quickly, be isolated, and just have the result. I think Joyent used it as an example when they were talking about zones, that in Manta could actually run a command on a database on a zone and then get it back. So the virtualization takes milliseconds, not minutes. And that opens up a whole new set of use cases that people didn't think about before. 

17:05 - **Daniel Shaw**: So that is the key to the architecture of Manta: every query is running in a new, isolated zone. That is the magic that is Manta. That's a real key technical accomplishment. Sounds a bit like the dream of isolates before we had domains. That was going to be something in node. It never really materialized, but it was interesting.

17:33 - **Jacob Groundwater**: There's one more feature when you're deploying docker, that is an advantage over using, say, VMs. When you're booting a bunch of VMs you have to boot the whole system right through init and maybe an ssh daemon or something. But docker, when you run it as a process, if you attach it to the foreground at least, your outside process is talking to the std in and std out of the process which is running inside the docker container. So a lot of people, if they're running for example a node app, whatever was centralizing these apps, which were all isolated, each running in their own docker container, there'd be some piece outside that's running the app inside the container. So you can coordinate it from the outside. And you actually skip booting init on all of these systems. You just boot right into the actual process.

18:25 - **Daniel Shaw**: Interesting. Cool. So we'll go into a bit more detail with how docker's being used. Everyone on the call is doing some really cool things with docker. So Nuno, do you want to queue up our beloved friends at &yet?

18:47 - **Nuno Job**: Right, okay! This show is possible due to the generosity of our sponsors. One fantastic sponsor that we have is called &yet. &yet is a consulting firm and a product shop. That builds all its stuff in node. They are renowned for having some really good members of our community that enable node to be what it is. They work a lot on security for node. You might have heard of the lift security project that enables companies like GitHub and 37Signals to have really proper security. They really focus on security with the node security project. 

They also have this really cool baby monitor that I've been using, which is called [talky.io](https://talky.io/). So what you do is this. You get your Android phone because it has the latests Chrome -- I don't know, don't ask -- and you go to talky.io/yourbabysname and you put it on the crib. And then you get your iPhone and you do the exact same URL. Then while your eating with your wife, instead of being with the kid, you can be talking with him and seeing that he's sleeping properly. So this is a great thing. They have been leading the efforts in WebRTC. Talky work with WebRTC underneath, which is fascinating. My wife has no idea why I'm so fascinated that I have a baby monitor on the phone. She's like "just buy on off the shelf." But it's awesome. And I probably shouldn't recommend you do it for security purposes because they didn't think up the use case, but I think it's great.

And finally, they have a product for realtime chat and team collaboration called [And Bang](https://andbang.com/). Which we used a little at Nodejitsu and you should try it out. And Bang will allow you to really collaborate well with remote teams. &yet has a lot of remote employees and they really focused on that. You'll have a lot of fun working with your teams with And Bang.

21:05 - **Daniel Shaw**: Awesome. Thank you, Nuno. So let's introduce some of the real world projects that are using docker. How's our connection to Niall?

21:19 - **Nuno Job**: The connection is good, just a little delayed.

21:21 - **Daniel Shaw**: Okay, so Mike is gonna have to take off in ten minutes, so why don't when throw Mike in here first and let him talk about what he's doing at Pearson?

21:34 - **Mike Brevoort**: Yeah, so one of the things that has excited me about docker is how lightweight it is. And how fast you can spin up containers. And the efficiency with which you can run containers with small differences, without requiring a lot of disk space or disk copy, as long as you clean up after yourself. So we're looking at this use case and continuing to iterate on our continuous deployment process. And really starting to look at using a feature branch approach with git. To be able to for every feature create a new branch, typical feature branching. But the requirement for our applications to be able to do end-to-end and run our full test automation against any one of those branches at any time, which means that they have to be deployed somewhere. And in our case they're deployed somewhere behind a firewall, which makes using something like Travis difficult or some of these other public tools. They need to be deployed somewhere so that you can do some discovery testing against those, you need to be able to access and log into them, you might run selenium tests against them. You want to do the full gamut of testing and full automated testing against these feature branches.

So what we did is we decided to use docker. So on every push to any branch to any of these projects: it kicks off building a docker image, then replaces the container -- or pushes a new one if it's a new branch -- to one of multiple docker hosts. That then has that particular commit point of that particular branch deployed and then to a central dashboard place you could go and see every branch that exists and that's deployed and what the URL to that branch is. You can attach the logs to it. We tag the images in docker with the short git SHA commit point and the version if it's actually versioned when it's ready to go. So what you end up having is this near-realtime state of deployment for every single branch that's pushed and a new one that gets pushed for any new branch that's created that then kicks off all of our test automation. So as we report back build status that gets pumped up through there as well so we can see full automation for builds happen. That's been amazing and revolutionary.

We hooked it into our hipchat robot called bender, so you have bender commands to get the URLs to the versions of the branches that are deployed from there. You can see build status and stuff from there. We're building off of that. So at the point that we do a merge into master that means it's done, tested, and ready to go. And when we do, that triggers a production deploy in a continuous deployment way. And right now we're researching whether or not we're going to do those in docker containers themselves. For this new project we're on I think we are. We're trying to be pretty aggressive with it. So we have those, and we're going to use our internal docker registry as our package repository for that. So deployment actually becomes much simpler because we just need to do a `docker pull` and then start a container up. 

25:18 - **Daniel Shaw**: So do you envision a Facebook cells kind of approach? If you don't know what Facebook cells are, they're isolated clusters of functionality that they deploy and they'll have those in production at the same time. Is production a contiguous thing that's only that point in time, or do you see that as multiple points in time that you're evaluating under real production load?

25:55 - **Mike Brevoort**: It could certainly be that way. And we do some of that today, even on individual we deploy on Amazon on the projects that I'm on. We have automation to do that and we roll new instances on every deploy. And we use this project that we open sourced called [Thalasa](https://github.com/PearsonEducation/thalassa) to do orchestration of load balancers based on app name and version. So this fits right into that -- you may have different versions of your app running at the same time in production. Maybe of sharded or zoned, or maybe A/B-style or hashring-type routing, depending on how you orchestrate that for you application. The benefit that it brings is that it's much faster to start up these containers versus starting up whole new instances. And it's faster to roll back when you don't have existing instances. Because your previous versions on that host actually has the full cache of the images. So it becomes really fast to do that as well.

26:51 - **Daniel Shaw**: Awesome. Be sure to throw in a link to Thalasa in the show notes so people can go check that out. It's a really interesting project. So Mike has to take off. Did you want to get a plug in before you take off, Mike? 

27:04 - **Mike Brevoort**: Sure. So I work at Pearson, we've been doing node for along time. We're in the Denver Front Range area in Colorado so if anyone's interested in that, hit me up. And also I organize the local [DenverJS](http://nodeup.com/www.meetup.com/Denver-JS) meetup, which is a node and JavaScript meetup. And we're looking for both speakers and sponsorship in getting together our 2014 plans. So if you're in the Front Range area come check us out on meetup.com. We'd love to see you there.

27:29 - **Daniel Shaw**: Thanks, Mike. Appreciate it. Let's hear about what Niall's been doing. He's probably gone the deepest down this rabbit hole. He's been doing some really fantastic stuff. Let's see if you have enough connectivity through Portugal to Mexico. 

27:47 - **Niall O'Higgins**: Mike really talked about some great stuff in terms of the possibilities of what you can do in production with docker. Something I'd like to talk about that might be cool, too, is just using docker as a kind of a platform to distribute open source applications. So I think if you look at a lot of open source web applications, node or otherwise, you're likely going to have some sort of dependency on a database. Maybe it's redis. In my own case with StriderCD, we have a MongoDB dependency. And what we're able to do with docker is package up the application itself with the source code from GitHub, plus the npm dependencies already installed, plus the node version that you need, and also an already-configured MongoDB. We put that all into a single docker container and push that up as an image to the public docker registry. So if you very quickly want to pull down the latest version of StriderCD without having to configure node, without having to configure and install Mongo, you can just run `docker pull strider/strider` and you should pretty much have it running on your system. So I think there's a lot of potential there.

I know other folks are already doing this. I've seen a very popular Jenkins image on the docker registry. I know now with container linking, which is a new feature in docker 0.7, this makes it even more interesting where you can start to have, say, an officially-maintained Postgres image. So any application which depends on Postgres can simply link against the officially-maintained docker image. And just link these things together with dependencies. So I see it as a great way for authors of open source software to make it easy for people to get their stuff out there and make it easy to configure. Especially for the more complicated applications.

Another one I can give an example of is Peter Braden -- my co-founder -- has the [node-opencv](https://github.com/peterbraden/node-opencv) project. node-opencv has a binding to the computer vision library but the binary dependency on opencv is very heavyweight. It's pretty complicated and difficult to build opencv on your machine. There's an enormous amount of dependencies. So I know he's worked to create a docker image which has opencv and node and his binding installed. So I think docker is really interesting for open source people, too. I'll just kind of throw that out there.

## Testing with Docker

30:53 - **Daniel Shaw**: Cool! Jacob, do you want to share some of what you've been doing with docker?

30:59 - **Jacob Groundwater**: So I have two very unrelated projects, but they're both using docker. Let's start with the practical one. Boo! But we'll get to the impractical one. I work at [New Relic](https://newrelic.com/) and we work on the node agent, which is what we use to instrument node apps. So if you're running something like a node web application you can install our agent as a module and it will report all of the New Relic goodness. You can look and see what are the slowest parts of your app and speed it up. Now, part of that is supporting the wide array of module configurations that people are using to run their node applications.

And what we wanted to do was have a very solid testing framework. So we had the tests, but we wanted to run the tests against multiple versions of node, and when we did that on the same machine, we were getting a little bit of leaking between tests. We spin up MySQL, Redis, and Mongo instances because we instrument those database connections. And what better way than to just test it for real? But sometimes a MySQL instance wouldn't terminate after the first test and it would leak into the second. And we had issues if I did an `npm install` and I changed the version, sometimes there were slight differences. So what I did is I took the [DNT](https://github.com/rvagg/dnt) module by [Rod Vagg](http://r.va.gg/) and heavily modified it and built a CI tool that runs the unit and integration tests for each version of node that we support in a separate docker container. And then it aggregates all the results and posts them to the web. And it does that based off of when we do a pull request on GitHub.

When one of us wants to add a feature, GitHub will send a post-back notification to our CI server and it pulls the changes and it will run those changes in a suite of docker containers. We know they're isolated. And then it posts the results back. The other thing it does is it saves all of the test runs so if one of them fails and I'm curious what the state of the machine was, I can log right into that docker container and re-run the tests, I can look at the log output, I can look at whatever the state of the machine is. Before I jump into the impractical part, did you have any questions about the CI?

34:01 - **Daniel Shaw**: That's really cool: being able to go back and post-mortem the state. Is one of the most essential things that you need in debugging. So that's fantastic.

34:13 - **Jacob Groundwater**: Yeah I'm looking into some more things I can add to it, like the possibility of core dumping, now that TJ has gotten Linux core dumps to work on the SmartOS tools. And MDB. I'm also looking at parallelizing it a little more because we support different versions of node on there but I actually want to run it on the 40-plus versions of node that we support. Including all the unstable 0.11 changes that are coming out. You know, just so I know. You never know!

So the other project that I've been working on -- which is totally un-related but also uses docker -- is NodeOS. Which is taking a Linux distribution, stripping everything out other than the kernel, including `init` and all the userland, `ls`, `bash`, getting rid of all of it. Then putting node on there, getting `npm` working, and then just using `npm` as the entire operating system's package manager. So if you want an executable like `pwd`, `ls`, or `vim` or something, you have to stick it on npm. It's complicated, and it's probably a topic unto itself as to why someone would do this. I wanted to start the project and get people involved very early, like when we're just duct tape and banana peels and things like that.

Originally I had it booting into a VirtualBox instance. I would mount the filesystem on some other Linux box, mess around with it, close it, then boot that image separately and see if it worked. And I found it was slow to do that, and it also wasn't that fun. I mean, the fun part of doing this was quickly building higher-level tools. And while -- if you're going to build an OS that starts from bare metal, you absolutely need to do the lower bits -- I decided I wanted to work from the top down, instead of from the bottom up. So I started using docker. And docker does a few things: the machine's already booted, the kernel's loaded so you don't have to worry about making sure you know how to load on the hardware that you're running. It will actually configure the external network interface for you, which is nice because other than that you're writing a lot of system calls that node doesn't natively support. And I did get that stuff working eventually.

But the main thing is I just wanted to have a pipeline where I could make a change, hit a build script, push that change out in a matter of minutes and someone else could be using it. So docker has really filled the gap there. So I have a build script that -- if you check out the GitHub project -- you have a checked out version of node and some other stuff, and it will build the docker container, and it will build the NodeOS image. You can just push it and pull it and people can play with it. I have a available so I'll put that in the show notes. It's been great -- it's a great pipeline and I think that's It's a really strong piece to have in your deploy pipeline. 

37:50 - **Daniel Shaw**: Fantastic. Nuno, you have probably one of the most important blog posts up on medium right now about docker. I know a lot of people are referring to that. We'll be sure to include that in the show notes. What are you doing with docker and why are you so excited about it?

38:10 - **Nuno Job**: I'm involved in some projects that are using docker. One of them was actually started by Niall, which is called BrowserStorm. Another one that I've been following very closely is [NodeChecker](http://nodechecker.com/) which is basically a center to test all npm modules. Are you familiar with it, Daniel?

38:30 - **Daniel Shaw**: Yes! I am, but tell everybody else about it.

38:34 - **Nuno Job**: [NodeChecker](http://nodechecker.com/) is a place where, every time you puslish a new npm package, it runs the tests for you. so if you go to nodechecker.com right now, which I am attempting to do, you can see: how many npm packages have tests that time out, have no tests, failed or passed tests. You'll find that over 50% have no tests. That's a big no-no.

39:04 - **Daniel Shaw**: That Nuno says "no-no."

[Laughter]

## Orchestration and Docker Linking

39:08 - **Nuno Job**: Yeah, that's my type of humor. So one thing I think is very exciting about docker -- that is really not very well understood yet -- is the linking part that Niall was speaking about. And the reason why it's interesting is, as Niall said, the way we deploy Strider right now is it puts Mongo inside the container, it puts all the dependencies inside the container, and is like "voila, here's a product." But there's limitations to this, of course, because as we know from npm, it's really good to have something that manages dependencies really, really well. There are a bunch of legacy systems -- I'm probably going to be the first person to call Puppet and Chef legacy -- Niall is not laughing, so it's okay.

But how do you do that in this docker era, right? How do you orchestrate all these containers? And for instance if you're running multiple servers, you can be running different OS's and different virtualization layers, and it's still not very well understood how you can still ship with the same ease of use that docker gives you. You can just put Mongo, put node, put Strider, and give it to an end user just with one command. How do you do that while maintaining the integrity of the relationships? That's super-interesting. I think there will be a lot of space to go and do work on that. One, there's new stacks coming up you'll find as a service things like [Orchard](https://orchardup.com/) that try to bundle up the docker experience for you. New stacks like [Salt Stack](http://www.saltstack.com/) etcetra I think are attempting to go on the docker route.

But the way I see it that is there is a lot of space for people to actually write their own scripts and to build new tools with node and with docker. That said, the guy that did [NodeChecker](http://nodechecker.com/), [Pedro Dias](https://github.com/apocas), he also did a project called [dockerode](https://github.com/apocas/dockerode) which is a really cool abstraction to use docker from node. You can check it out at [github.com/apocas/dockerode](https://github.com/apocas/dockerode). But I'm pretty sure that if you Google "dockerode" you'll only find this. And I think it's really an exciting time to create this glue, right? How does it work? Another example that Niall gave was, well, when you're running Mongo and the node Strider version, if Mongo goes down then you probably should restart both. One thing that I've been using is the excellent [node-mongroup](https://github.com/visionmedia/node-mongroup) by [TJ Holowychuck](https://github.com/visionmedia). So doing all this, it's not even orchestration but all this layering just to manage the dependencies right, and have docker containers be independent and work across different servers and even, potentially, different architectures. That's really the part that is interesting for me right now, in docker. So that's it. 

42:12 - **Daniel Shaw**: Awesome! Does anyone want to talk about [Rod Vagg](http://r.va.gg/)'s [DNT](https://github.com/rvagg/dnt)?

42:20 - **Jacob Groundwater**: Yeah, I actually use DNT, well, heavily modified to the CI tool. It was a great starting place. I'm not sure of the state right now; I had to modify it a little bit. I think DNT checked for tap-style output rather than, say, checking the exit code of the process. I had to modify that and a few other things but I think it runs pretty quickly if you just want to try something out. So have a look at it, contribute back to it. Give it a shot. 

43:04 - **Daniel Shaw**: So DNT is Docker Node Tester, for those of you who don't know -- sorry about that. And that's [github.com/rvagg/dnt](https://github.com/rvagg/dnt). Go check that out. Alright, so let me fold in our final sponsor. And thanks again for sponsoring NodeUp. If you want to sponsor NodeUp, it's really important so be sure to reach out to NodeUp for that. So our final sponsor, last but certainly not least, is Modulus. They offer reliable node.js hosting. They have a great platform that includes integrated MongoDB hosting with built-in performance statistics with very slick end-to-end analytics that is able to coalesce all that information about your applications and the database. They offer free custom SSL, full websockets support, and they support nearly every node.js version. Use the promo code `nodeup1` at [modulus.io](https://modulus.io/) and you can get started for free. Be sure to visit them.

And, announced at NodeSummit: they have a brand new package, Modulus for Business. Two great products: one's called Curvature, the other's called Inflection. Curvature is basically a private cloud version of their service. Rapid deployments, easy scaling, realtime analytics in an environment that is yours. You control it. It's on-premises and can be run inside your internal network, you can run it in your own cloud, or a hybrid of the two, whatever you choose. Inflection is their robust analytics package to give you insight into the applications using full stack analytics. Again: cloud, on-premises, or hybrid. For more information about Modulus for business, run over to [enterprise.modulus.io](http://enterprise.modulus.io/). They are on Twitter at [@onmodulus](https://twitter.com/OnModulus). Why don't you send them a tweet and thank them for supporting NodeUp. We really appreciate it. 

So, in this final block, what I'd like to do is share some of the more practical portions of working with docker. One of the best things working as a developer that I can get from other people is what are the real pain points and if you've worked through a pain point and can share that with someone else, that's potentially hours or days, if not weeks, that are saved. So I'd like to dive into that. Anyone want to kick us off with that? 

46:03 - **Niall O'Higgins**: I think the thing to remember with docker is that it's a relatively new project. I know that they started working on it approximately a year ago now, and it went public in maybe March or April or something. So the thing to remember is, while it's pretty stable now, it's still a maturing technology. It hasn't hit 1.0 yet or anything like that. So definitely keep that in mind. I would love to hear from Jacob about some of the issues he has encountered. I'd love to learn. Especially with his NodeOS project. He's really using it heavily. He mentioned using the public registry for distribution and stuff like that.

Personally, I have found that the big issues I have run into myself are with heavy utilization of docker layers. First of all, there was a hard limit of 42 layers, which I know has been at least doubled, of possibly even greater than that recently. So there used to be an issue with too many layers. There was basically a hard limit and it was pretty easy to reach that layer limit quickly. So that would be the first thing I'd throw out there is the limit on layers, which is unfortunate because the concept or abstraction of building these layers is very appealing as a sort of normalization potential of your stack. It's very appealing in terms of sharing . But unfortunately I've found that I've run into issues in practice. Jacob, have you run into that or do you have work-arounds? What's the story there?

48:05 - **Jacob Groundwater**: Yeah, so I did run into the layer problem at one point. Luckily I wasn't building up too many layers. And then by the time I actually cared they had upped the maximum limit for layers. But there are a lot of things that I've bumped into along the way. And much to docker's credit, maybe a couple weeks after I bumped into them, they are fixed. And maybe everything that I mention here will be fixed in another couple weeks. But I would say there's a lot of stumbling in the early days. If I were to give advice to another team I would say: don't read the docs and then make a giant plan. Just try it out first and then organically grow towards a dockers setup that works. Because a few things read differently on paper, at least in my mind, than how they execute. I don't know, what did you think?

49:10 - **Niall O'Higgins**: Certainly, I'll give you an example here. I went with the approach initially of building, a lot of stuff with the http API. I found that it has some inconsistencies and some changes of the versions of it. And I've found now that a more stable API, from my point of view, is to actually use the docker command line tool as the API. So use the docker CLI tool and fork a process that runs that. I personally found that worked a bit better for us. But again, that might change: hopefully the http API will improve. There were things with the documentation. Where the reality of it versus saying "hey, let's use the http API for everything" were a little bit different. That was something I ran into for sure. 

50:05 - **Jacob Groundwater**: I use the command line almost exclusively. I have a build script which delegates to the command line. And I use a docker file to build up my images. A few examples of things that I do in the docker file. A docker file is basically a line-by-line recipe for adding new layers to your image. So kind of in the end each layer of your docker file ends up being one layer of your system. And that's a little weird to people sometimes if you run a single command like `mkdir / app`, that's a whole filesystem layer. And if you do another command, which is copy the app or change a permission, that's another layer.

So after you realize that the first time -- and especially with that limit of 42 layers early on -- it's kind of like "oh, I can only run 42 commands." So then what you do is you use the `copy` command which copies in a directory and all its subdirectories and folders and files into the docker image and unpacks them somewhere. But at least when I was using it, I don't think it ever cached that step. So if you had to copy in stuff in your deploy, you couldn't utilize the caching. Normally with commands like a `tar` or a `curl` or a something command and it's already seen that command, when I go to rebuild the docker file it'll just go "oh, I'm going to re-use this layer that I've already seen."

So it's just stuff like that. It's nothing really game-ending. But things that might affect your strategy before you run into them. So it's good to bump into everything quickly, stumbling around and trying to get something together. And then from there work on figuring out how this should fit into your pipeline. 

52:00 - **Nuno Job**: Actually, Jacob, I've found the same problem when I try to build a CouchDB image. It's [dscape/couchdb](https://index.docker.io/u/dscape/couchdb/) on the docker index. So the strategy I did was: first, copy everything that's in the repo to opt and then go from there. And I found that it completely invalidates the cache. If you're new to docker, what that means is in the docker file when you run a command it get cached. Then if you append new commands and when you try to re-run the docker file to re-generate your docker container it will only execute the new commands. So let's say you're doing an `apt-get install` that takes 40 minutes, you're not taking 40 minutes; that's done. However, when you try to copy files from your repo to the docker container with the `add` command -- at least it used to be called the `add` command -- it invalidates the cache completely. That does allow you to run commands like shell scripts. For instance you can run `apt-get update` shell commands that will do all the steps you need. But you lose the cache. So you won't get into the too many layers problem, but you'll get into the problem of waiting for stuff to build that takes forever. Which I think is what Jacob Goldwater is talking about. 

53:22 - **Jacob Groundwater**: Just for the record, if you're tuning in late to the show, "Goldwater" is my joke name. I should just mention that before it spreads throughout the community.

53:30 - **Daniel Shaw**: You've been fully re-baptized, sorry. 

[Laughter]

53:38 - Who is this "Goldwater" guy? He's doing some cool stuff!

53:45 - **Nuno Job**: Another thing that I would like to mention is I found the docker file to be counter-intuitive when it was first introduced. Because it's kind of like a make file, and that makes sense for developers, but containers are not just like programs. But I guess it's the way that the guys from the docker company see it.

Anyway, there's all these layers of other things. For instance, how do you maintain the security of the operating system that is running the containers and how do you update security patches to it? How do you update containers continuously with zero downtime? And how do you do the lifetime management of a container that is running in production? How do you manage the auto-scaling functionality that can be offered by docker? And how do you make sure that your cluster is just seen as a set of programs that are running in containers, so you don't have to worry about how many machines are there, you just auto-scale with Amazon auto-scaling functionality? How do you do that for redundancy? And finally, something that we talked about a little bit more, is how do you orchestrate all of these things: your MongoDB and your Strider?

So for all of these problems: the auto-updating, the lifecycle management of the containers, etcetera, there's this exciting new project called [CoreOS](http://coreos.com/). It's made by [Alex Polvi](https://github.com/polvi). I think he made a company called Cloudkick before. I hope I'm not saying the name wrong. But CoreOS is a really exciting project and it tries to be the SmartOS of Linux. Of course, if you are familiar with SmartOS, and you know that `killall` in SmartOS is not the same as in Linux, well, then you can try zones and you probably will be very pleased with that. 

55:38 - **Niall O'Higgins**: To Nuno's point, the issues with what you can call service discovery and orchestration, there's a lot of tooling left to be built there to make that easier. We've developed for our stuff at Frozen Ridge some ad-hoc node scripts to update the layers to do zero-downtime updates of running containers, and to do workflow for updating existing containers. For security issues or updates for customers and so on. And we're hoping that we'll be able to make this stuff generic and put it out there for others to use.

I think maybe Jacob, too, has some stuff to say there as well, or perhaps Mike. You've put out some interesting stuff. That kind of lifecycle management is very much an unsolved problem. Everyone has to roll their own at this point in time and I do hope with in the next 12 months we'll be seeing some standards there.

One thing I would like to say in terms of standards or pre-existing things that you can use: there's the [dokku](https://github.com/progrium/dokku) project by [Jeff Lindsay](http://progrium.com/blog/). It just runs in a single node at this time but it's sort of a Heroku-like mini PaaS or mini Platform as as Service, which supports all the native Heroku build packs. Which means that it has excellent node support.

So what you can do with dokku. Which is very convenient, especially if you're new to docker and you just want to get up and running with your node application. You can just deploy this thing very easily to, say, a Digital Ocean droplet or an EC2 VM or whatever. And then, just like Heroku, to deploy your app you `git push` to it and dokku actually abstracts all the routing and all the container updating. And it has really nice node support where it's aware of your dependencies and whether any of those need to be updated. So for people just looking for a quick way to get their node web applications up using docker, I'd recommend checking dokku out. It only covers a single node. It's not perfect, but it's a good starting point. But I do think in the next 12 months that's what we're going to see: the emergence of major open source projects that are that infrastructure, basically.

58:30 - **Jacob Groundwater**: You just reminded me that I actually do use docker for yet a third thing, which is dokku. Because I've written a bunch of sample apps that we use the New Relic module on to instrument, just to get a good idea of how it looks for a particular application. And I actually deploy all those applications using dokku. 

58:50 - **Nuno Job**: I've found that at percent when we want to document something, we have a dokku digital ocean image, which is a super-tiny image and we just `git push` it up. And I found that the combination of heart.js and dokku was amazing. Becauseit just write some markdown, `git push`, and then you can share the documentation with all your team. And that's quite amazing. 

## Docker Concepts and Terminology

59:12 - **Jacob Groundwater**: One thing that I've bumped into with docker: a slight pain point since we're on this topic. I found the abstractions to be confusing at first. I think a lot of people might bump into the same thing. There's a concept of a container; there's a concept of an image; there's a concept of a repository; and a concept of a tag. And just to clarify, this is my concept of what those things actually mean.

An image is an actual disk image. It generally doesn't change but you can boot a system off of an image. And generally when you run docker instances you run this particular image. A container is an image after it has been run. So when you run that image, if you were to log in for example, run bash touch a bunch of files, make a dir, and curl something, all those changes that you made are in the container. And if you want to distribute those change, you have to snapshot it to an image. When you snapshot it, and maybe this goes along with images, you have to give them a name, and that name is the repository. And that's the thing you can push and pull to the docker index. You're pushing and pulling repositories. And then there's also a concept of tags, which is a dimension along the repositories, kind of like a version number, but I seem to have kind of messed it up, I'm not sure of the best way to do that stuff, it might be very simple but I'm messing it up. Maybe someone else can fill it in there. 

1:00:55 - **Daniel Shaw**: You almost, word for word, nailed a question we had from Twitter, in the [NodeUp contribute repo](https://github.com/nodeup/contribute/issues/25) from [Jim Kang](https://github.com/jimkang, which is basically that. What do all these things mean? Can you back and forth between them? 

1:01:11 - **Niall O'Higgins**: Yeah, just to make things even more confusing, Jacob, I think now containers can also have names. And of course then you have container IDs and image IDs, which people may also encounter especially when you are changing tags associated with images and containers. So I definitely would agree that the terminology is confusing and the mental model is a little bit confusing, with that distinction between container and image. I'm definitely guilty of kind of using "container" and "image" interchangeably, which really annoys the docker folks if you go into their irc channel and start doing that -- calling images containers and containers images.

But I think you pretty much nailed it with your description, Jacob: an image is a sort of an on-disk binary starting point for execution, is how I'd think of it. And then a container would be like an instance of that, plus any changes. It may or may not be actually running at the time. So those have to be snapshotted -- or the docker term being "committed" -- to make a new image.

And then those containers now can also have names, which can be helpful to identify them over the course of their lifecycle. You could use that to perform zero-downtime updates or other types of upgrades or lifecycle secnarios like the ones that Nuno mentioned earlier. I think now in more recent docker versions you'll see it auto-generates interesting human-readable names for containers, to try to make it a bit easier to remember what's going on.

But the mental model certainly took me a while to get my head around. Especially with these different IDs and names, and what refers to what. You've definitely got to give yourself a little bit of time to be clear on that. One thing which can be confusing, too, is that -- I guess this comes back to the containers images and lifecycle issue -- if you run a single command, like let's say you touch a file inside an image `docker run` from the base ubuntu image of `touch /temp/foo` so that will actually in turn write to disk. And that process will execute very quickly and will be finished. And so if you run a `docker ps`, which will show you the currently running containers, you're not gonna see it in there. However, that container's still on your system even though it's no longer executing. And you can go back and access that new file `/temp/foo` that you created with the `touch` command. And the key there is to supply the `-a` option to `docker ps`.

So `docker ps` is "show all of the historical containers" and if you're new to docker and you're playing around and you're just getting used to stuff and building images and running commands, you might be surprised at how much stuff is actually kept around. I think that's something worth noting. And indeed, this is something Nuno and Jacob, you might have run into and I'm sure Mike will have stuff to say about this, too, in production: you can easily end up utilizing a bunch of disk space without really recognizing it. I think that some sort of garbage collection mechanism is something that we'll see. Because there's definitely need for that. The example I have is a container where you're touching a single zero-byte file. That's no big deal. But if you're running an `apt-get` which is several hundred megabytes and you're just forgetting about those containers you could eat through all your disk space. So if you're looking at this stuff in production you certainly want to have a kind of strategy for cleaning up after yourself as part of your docker lifecycle. There's definitely a garbage collection phase there which is something to keep in mind in production.

1:05:40 - **Nuno Job**: Do you think that garbage collection would be a good idea? Because normally what I do is just whenever I'm finished with the container I do a `docker ps | xargs` kind of thing to clean it up. But I would be kind of wary of an automated garbage collector.

1:05:52 - **Niall O'Higgins**: Yeah, that's what I mean, in that I suppose you have to do your own manual garbage collection with that. But I think maybe being able to set some sort of policy there, I think that the docker tool itself could help you out with that. Maybe you could set a disk-space policy or a time-based retention policy. I don't know exactly, but I think a little bit more would be helpful. 

1:06:16 - **Jacob Groundwater**: So one of the tips I'm gonna give everyone is the `-q` option is great. Because you can go `sudo docker images` or `sudo docker ps -a -q` and it will just give you a list of the IDs with no headers, no extra information and you can just pass that directly to the `sudo docker rmi` or `sudo docker rm`, which will remove the containers and images. So when you're just playing around and you notice that you're getting a low disk space warning or your virtual machine has come to a halt, that's a quick way to nuke everything quickly. I know it's probably not what you'd want to do in production, but in my use case where I'm generating a lot of ephemeral containers -- and lots of them -- it's really handy. `-q`, remember that one. 

1:07:09 - **Nuno Job**: Another thing to help people with this same question is actually the blog post that Daniel referred to. Which is called -- I totally forgot -- something docker couchdb node.js, of course. You can Google for getting stared with docker as a node.js and couchdb programmer. It's actually pretty extensive; it will take you like 20 minutes to do this. But the reason I wrote it was I've worked in infrastructure for a while and I've even built stuff like package cloud, which is an abstraction to try to normalize the naming conventions in the cloud industry. And I can tell you, Jesus Christ, you need to have a dictionary of your own! It's very hard to keep up and there's no amount of talking that's going to make it for you. So the only way you can learn is by doing. If you do this blog post for 20 minutes you will understand exactly how docker works, and even if you don't know the words you will have a clear understanding. I even believe that's how Niall started. I'm not sure, is it?

1:08:18 - **Niall O'Higgins**: I don't think it was through your blog post directly, Nuno. Though I did see that. But I mean, yeah, just playing around with this stuff is the way to go. Definitely just start running stuff and seeing what you can do. 

1:08:30 - **Nuno Job**: Cool, so I'm totally wrong!

[Laughter]

1:08:35 - **Nuno Job**: I know it's someone, maybe it wasn't you. Sorry.

## Docker in 6 to 12 Months

1:08:41 - **Daniel Shaw**: Awesome, awesome. Okay, so we covered Jim's question. So any closing thoughts, guys? Let's go around the horn, and say six months or twelve months from now, is it all docker or is it the thing that we've replaced docker with? I think it's all docker. 

1:09:05 - **Nuno Job**: I would like to start, Daniel, that in six months I hope you are winning the selfie olympics . Not good enough! Not good enough! In six months, that's my expectation. I don't know about docker and SmortOS, etcetera.

[Laughter]

1:09:22 - **Daniel Shaw**: Aim high, alright! Winning the Internet.

1:09:26 - **Jacob Groundwater**: I think it won't be raw docker, I think there will be a layer of indirection right on top of docker. Because all problems in CS can be solved by another layer of indirection. 

[Laughter]

1:09:35 - **Niall O'Higgins**: Exactly. Yeah, I think I'd be with Jacob, there. I think we'll see another layer on top of this. I think [Flynn](https://flynn.io/) -- is that the name? -- is one project that Jeff Lindsay and a bunch of others are working on. There's a bunch of attempts out there. So yeah, I would agree, I think docker's a nice tool at a certain layer but many people -- like application developers who want to get their stuff out there -- will probably be using something else on top of it.

1:10:07 - **Daniel Shaw**: I agree with you but I think we're all in agreement that the primitive below that likely to be docker, and I saw just today that OpehShift is also adopting docker. Silence.

[Laughter]

1:10:28 - **Jacob Groundwater**: Nope. We didn't see that. No comment!

[Laughter]

1:10:31 - **Daniel Shaw**: Sorry for bringing enterprisey things in.

1:10:34 - **Nuno Job**: I'm actually quite interested in -- as Niall said -- docker doesn't really do much. LXC containers is what does most of the things. And they're secure, like Google is using them internally all the time. They're pretty battle-tested. Docker is kind of like git; it gives a git-like command interface.

1:10:59 - **Jacob Groundwater**: Yeah. It feels very similar to using git, and the abstractions are kind of lined up similarly. 

1:11:05 - **Nuno Job**: And right now to use this git of lightweight virtualization you have to use Linux and Linux containers. At Nodejitsu we used SmartOS, and I can tell you that technically it's a brilliant solution. Zones are almost perfect, you've got DTrace, you've got so much cool stuff. So I'm really interested in seeing docker, as Niall said, work in SmartOS too. The same abstraction running across different OSes. I think that could enable a real cloud that is OS-agnostic. At Nodejitsu we just worked our asses off to do that and I'm really excited about that possibility. Finally I'd like to say technically, I don't know if docker is better than zones in anything, possibly not. So there's always this question in my mind, which is "why is it that Solaris is losing?" But the people have spoken: they've chosen Linux. And if people have chosen Linux, docker is the future. 

## Plugs

1:12:07 - **Daniel Shaw**: Cool. Well, we'll wrap it up there. Let's do some quick plugs. Reminder plug from Mike: join Mike at Pearson. There's the Denver area, but Pearson's around the world. They're doing some really great stuff with node.js. So I highly recommend dropping them a note. And DenverJS. Mr. Groundwater, why don't you go ahead?

1:12:25 - **Jacob Groundwater**: I would love it if people would give the NodeOS docker image a try, even if it's just five minutes and then you turn your head in disbelief! Should I say the URL or you going to put that in the show notes?

1:12:37 - **Daniel Shaw**: It'll be in the show notes.

1:12:39 - **Jacob Groundwater**: So I wrote a little blog post on what to do you don't pull the image and then just stare at it. 

1:12:44 - **Daniel Shaw**: So you can go to node-os.com 

1:12:55 - **Jacob Groundwater**: From there you can have just a couple blog posts. I'd love it if people just tried it. I would be thrilled and ecstatic if someone else out there did a docker file and put some different commands in and pushed to the registry. Tweet me back on that. That would be amazing.

There other thing I would like to say is I've been checking out things like [gittip](https://www.gittip.com/). And I do not need this, but there's a lot of devs out there who definitely do a lot for open source, and it seems like a cool way to give back to them. There may be many funding solutions. I don't want to get into the argument about which one is best. But if you are working at a company getting paid well, there's a lot of open source devs who put a lot of work into stuff. I am leveraging and other people are leveraging. So let's see if there's a cool open way we can get funding to these guys. So gittip, or whichever one you want to try. I would just say go for it. 

1:13:52 - **Daniel Shaw**: So if you don't know who to give to. You want to contribute something and don't know. Why don't you just give to Jacob or myself, even, and I bet jacob does the same thing with whatever comes in through gittip. I just share it back out. I shove money over to substack or whatever.

1:14:17 - **Jacob Groundwater**: I don't have any gittips coming in now, but I guarantee if anyone gives me a gittip I'll send it to a good dev. 

1:14:24 - **Daniel Shaw**: Right! That's what I do. So if you don't know who to give to, both Jacob and I do that with our gittip: we send it downstream to those who need it and those who merit it. So go in, explore gittip, it's also a great way to get to know some really great developers who are doing wonderful things for open source. So that's a great recommendation.

1:14:50- **Nuno Job**: Did you say Niall or Nuno?

1:14:54 - **Daniel Shaw**: Uh -- Nu-ai-lo! Naill-o, why don't you go?

[Laughter]

1:14:48 - **Nuno Job**: Niall-o, it's your turn.

1:15:00 - **Niall O'Higgins**: Niallo-o, alright! I'm just going to go with it here. So a quick plug for myself: I'm one of the founders of frozenridge.co. We do node.js, MongoDB, JavaScript software development and training as well. So if you need help with node, docker, continuous deployment, MongoDB, anything like that, get in touch and we'd be more than happy to help. And I'm just going to plug my open source project, StriderCD.com, which is an open source continuous deployment platform. It's very modular, it's all built on npm and node. StriderCD.com. Check it out. I'd love to see your contribution. So thanks, that's my plug.

1:15:49 - **Daniel Shaw**: Awesome. Thank you, Niall. Nuno?

1:15:51 - **Nuno Job**: Cool. I didn't really have a plug. So I tried to make one. One thing I've been seeing in a lot of node.js applications is that you build your node.js app, it's perfect, it's awesome, you don't have segmentation faults because you have the event loop. So everything it good. Until your application becomes really big, until your application reaches critical mass. When that happens, you start having errors where you don't know really what's happening. You start finding small memory leaks. And you start having these really-hard-to-debug production issues. Brian Cantrell from Joyent talks about this all the time. Even Daniel has been covering this quite extensively.

Now, I believe the reason why that is happening is people are taking the wrong approach to doing node programs. And there is the need to have something like DTrace running during every single commit you do on your project. So you can monitor the changes that are happening to your performance; every single time you make a code change you know what the impact is for your application. Now, this is not public but I know that [Pedro Teixeira](https://twitter.com/pgte) created something called nTrace that does exactly this. Every time you do a commit it runs a bunch of benchmarking things: it runs DTrace, it creates a flame graph for you. It allows to see what happens to your program as you change the code. If you want access, if you have a really big deployment of node, and you want to have access to this, or if you have an open source repo that requires extensive performance measurements and monitoring for every single commit -- for instance, [node-mysql](https://github.com/felixge/node-mysql) by [Felix Geisendörfer](http://felixge.de/) would be an example -- get in touch with me and I can try to get you set up. Because we're building the product so we can improve it and you can probably get a lot of value out of it.

1:17:45 - **Daniel Shaw**: Nuno, add something that people can link to because if you search for "ntrace" the first entry is like "high-performance tracing for .NET!"

1:17:56 - **Nuno Job**: Oh, there we go!

1:17:57 - **Daniel Shaw**: Awesome stuff, but yeah, send me an email or a way to get in touch with you. 

1:18:06 - **Nuno Job**: This is super, super under the radar so you have to go to [twitter.com/dscape](https://twitter.com/dscape) which is me, or [twitter.com/pgte](https://twitter.com/pgte), which is Pedro. Just tweet us and we can get you set up. Including you, Daniel, because I'm pretty sure you were like "oh, this sounds exciting." 

1:18:20 - **Daniel Shaw**: Awesome, well I want to also congratulate Nuno for becoming a dad. Nuno and Paula had a baby and he was bitching and moaning about not getting any sleep and Mike and I were like "Ahahahahaha!" Well, congratulations and welcome to fatherhood. 

1:18:40 - **Nuno Job**: Thank you! 

1:18:42 - **Daniel Shaw**: So, quick plug from me. Trevor and I have a online performance analysis training. We just wrapped up the second iteration of that this morning. And, speaking of babies, Trevor's having a baby in February, so we won't be running a session in February -- he'll be out on paternatity leave for all of February. We'll be back in March. Friday, March 14th we'll be back with more performance analysis goodness focused on the Linux platform. So sign up now, it's very limited. Small batches of courses. And you can find more about that at [firm.io/perf-beta](http://firm.io/perf-beta).

And this Summer I'm bringing back the Summer of Node. It's going to be through The Node Firm. And we've got a lot of great internship opportunities. I've got a few other friends and partners that are going to be also having great node internships, so if you are in school or if you're helping students find an internship for the Summer, drop me a note [dshaw@thenodefirm.com](mailto:dshaw@thenodefirm.com) and let's talk about node internships. There are numberous opportunies. You shouldn't be doing anything other than node this Summer. So, don't do bullshit; go write some node and have fun!

We're also gonna do some Summer of Code. So the original Summer of Node had come out in San Francisco. There's gonna be opportunities all across the world. We've even got some stuff on location in India that you're gonna be able to do. So, it's gonna be fantastic. We're really opening up the Summer of Node to a world-wide experience.

Quick note: we have some upcoming events. In March, there's JSFest. Be sure to come out for that. March-April-ish in Melbourne, CampJS is coming. JSConf, I almost don't want to mention it because we don't have anything there yet. It's probably too late, end of May. And then nodeconf: tickets are open for that, so buy a ticket to nodeconf and come out to Walker Creek Ranch and join us there. It's gonna be an amazing time. So thanks a lot. Thanks everybody for joining us and for kicking off 2014 -- the year of node -- in style here on NodeUp. So thanks, guys!

Be sure to leave a review for NodeUp on [iTunes](https://itunes.apple.com/us/podcast/nodeup/id447667314?mt=2) and follow [@NodeUp](https://twitter.com/nodeup) on the Twitters. And I think we have some sponsorship opportunities opening up in the next month or so. So get in while there's still a sponorship slot. So thanks a lot and talk to you soon.
