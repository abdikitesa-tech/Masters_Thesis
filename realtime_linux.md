
good morning everybody thanks for showing up I think this is actually the

biggest stage I ever got for presentation much appreciated so let me

let me quickly introduce myself my name is Jan Edinburgh I'm a trainer and

project manager at Linn atronics which is a service provider for doing embedded

Linux development well you yeah you might have heard of us so we do a lot of mainline development for example we

we've got the x86 maintainer at Len atronics we we do a lot of different mainline development and actually one

thing we do is on behalf of Linux Foundation we're trying to get the

real-time capabilities of linux into mainline and that's basically the topic

of my talk today i would like to give you a brief introduction on using

real-time systems with linux or how to make linux real-time so this is not

going to be a very technical talk this is basically a overview of what you could do what's possible what not and

giving you some historical details about real time in linux so i will talk about
Overview
----------------------------------------------------------------
basically about the definition of real time so first of all before we start to

look into linux in real time we need to get an idea basically what's the definition of real time and and who

needs real-time systems this is how we we're going to start it today well then

we will look into Linux in real time you will see we have several approaches on on making Linux real time we have

several different approaches like we have real time systems with Linux around for more than 15 years right now so we

have a lot of different historical approaches on how to make Linux real time so I will show you the most

important ones and then the ones which are still well developed today in which are used in the industry we will also

look into the app the results and the latencies you could basically achieve

with the real time Linux on a specific platform so basically we will look into

a cortex a9 dual-core system and see which Layton sees could be achieved with the

current real-time Linux approaches so this is basically what I'm going to talk today about so now let's get started now
What is Realtime
----------------------------------------------------------------
let's quickly rethink what real-time is about and and for me this this

definition is pretty important because still when we do presentations or trainings on this we can see that

there's still a lot of confusion about the definition of real-time so basically one definition we get really often is

well real-time is it's just about fast responsiveness it's fast execution well

I don't know is anyone in here who would agree with that no one yeah you experts

already so basically yeah this is not a definition of real-time right but but you get this definition very often real

time is about fast execution it is not well another definition we get quite

often as well it's about performance which is also not true right but well we
What is not Realtime
----------------------------------------------------------------
have to admit that the word real time might be a bit confusing also it's not

fast execution it's not performance but well if we would go outside the hotel

and ask people on the road what's real time they would tell us well maybe it's the real time just the time of the day

basically what we have a clock real time in Linux right but that's the time of the day but this is also not what we are

going to talk about today so real time is kind of confusing so it's this is why

it's that important to get a clear definition of what we're going to talk about today and to get it in the correct

context with Nino's so it's not about it's not about faster responsiveness it's not about performance basically
Timing guarantees
---------------------------------------------------------------
it's all about determinism so when we talk about real time we talk about

timing guarantees so you need to execute something in a specific time frame and

you need a guarantee for that so basically the definition would not be as

fast as possible it would be as fast as specified and this is the thing which

is important about real time so well if 30 seconds is enough for you well it's okay so your definition of real time but

you need a guarantee to meet this so this is really important to get this point when we talk about real time it's

all about determinism so when I talk about Linux in real time today

I am going to talk about deterministic timing behavior with Linux this is

basically the idea of this talk so well

could you help me out here wait a second

let's try that again just let me know if it's making trouble again so well yeah

sorry for that okay thanks thanks for

telling me and so once again we've been talking about determinism so now when we

start about talking about real time Linux the next question would be who needs real time Linux so basically when

we talk about real time we have to think that the correctness of your algorithm you're trying to calculate it's not just

based on the correctness of your algorithm it's also based on the correct execution time which means if you don't

do the calculation within the correct time frame this will lead to an error

condition so this error condition in a real-world example might be the product

you're trying to manufacture is broken your machine will break or something so
Error condition
--------------------------------------------------------   
missing the time slot will lead to some error condition and actually the worst case situation would be if you miss the

time frame usually someone would get hurt right so if you get into that situation that the

machine gets broken or your product or someone gets hurt this is basically the

moment where you need to think about real time requirements so now one last

point on the definition of real time and this is something we hear really often

when it comes to to Linux in real time we get some word like soft real time so
Soft Realtime
----------------------------------------------------------------
I don't want to get really deep into that topic but please please forget

about this word so we don't talk about soft real time let me give an example like if your wife would tell you she's

kind of pregnant would you believe that no you wouldn't right so well she can't

be pregnant or not so same for real time now let me give you another example like if you think about a use case and

missing the time slot will lead to an error condition so basically I'm interested in not getting hurt well not

getting hurt from most of the times wouldn't be acceptable for me so basically that's the same for real time

so you can't be deterministic or not but there's nothing in between right so please forget about this soft

real-time word it's it's just crap right so we can be real-time or not so when

I'm talking about real time today we talk about hard real-time and deterministic timing behavior that's it
Realtime Linux Users

so well when you get into a new technology just first thing you do is

you're trying to check out who else is using this at this very moment so basically you don't want to be the first

one right so what for real-time Linux we actually we have many users around in

this world which are currently already using real-time Linux systems so we have

a lot of industrial applications we have the automation industry actually or AL

automotive industry we've got multimedia systems we even get well aerospace

systems in none safety-critical locations and we actually we have

financial services which is pretty strange but they run it on big server

machines for example for high-speed trading and stuff so they need a real-time operating systems and these

guys are actually using real-time Linux so we already have a lot of users of

this system around so when it comes to
Realtime Linux Requirements
------------------------------------------------
real time in the real time operating system we need to check a couple of

requirements for this so we need deterministic timing behavior and to get

deterministic timing behavior one of the most important features operating system

needs is preemption now basically you need to be preemptable at most of the

parts in the operating system because the high priority task needs always to be able to do preemptive low priority

tasks right so this is the most important requirement for a real-time operating system and well you also have

a couple of special situations you need to deal with one of these is the so
Priority Inversion
----------------------------------------------------------------
called priority inversion so some of you might have attended the real-time summit

yesterday they had a couple of discussions on this so in real-time systems we have this classic error

scenario so basically what could happen is just think about static priorities

we've got three tasks tasks one is the highest priority task task three is the

lowest priority one so basically now these two tasks need to share a resource so we need to some kind of

synchronization so what would happen right here is task one is blocking because task three is holding that

resource which is basically not a problem at all but now what could happen

is task three gets interrupted by something in between before it can

release the lock so the result would be a high priority task is waiting for low

priority tasks and the lock never gets released until task 2 stops running so

this is a clerical classical arrow situation in real time systems and actually a real-time system

needs to deal with that so we have a couple of strategies and actually lay Doc's can already deal with this

situation and you don't even need a real-time extension what Linux does is
Priority Inheritance
----------------------------------------------------------------
in this situation we've got the so called priority inheritance which is

basically to keep it very simple in this situation what we would do is we would

boot boost task 3 to the priority of task 1 until the point it releases the

lock so we can avoid task 3 to get interrupted by someone so it's not just

the preemption we have to deal with a lot of different use cases which are

very specific to to real time applications and we need to think how we can get these features in a general

purpose operating system like Linux so
Dual Kernel
----------------------------------------------------------------
traditionally we have two approaches to make Linux real time capable and well

the oldest approaches are the so called dual kernel approaches which are basically not doing real time in Linux

it's like having real time in Linux on the same system so these guys just introduced a micro coil which is doing

the real time and well the other idea is just to find a way to make Linux itself

real time capable so let me try to explain that so this is the classical
Micro Kernel
----------------------------------------------------------------
blue kernel or microkernel approach so what these people do is they do a simple

real-time curl so this part is just about doing the real-time stuff and the

idea is that Linux is just running on top of this micro kernel as a low priority real time task so if you don't

have any critical real-time applications running well Linux can get some runtime

so this is the basic idea of this micro kernel approaches which looks quite

clever at the first glance but well if you think a bit more about this approach

if you've got two problems you have two to solve right because someone needs to maintain that

microkernel rate and is supported to new hardware so just think about the amount

of arm soch are coming up right now so this is exploding so someone needs to

maintain a microkernel needs to part it to new your hardware this is a huge effort and well basically these

communities are not as big as the community of the lis nosecone so this is basically something you have to deal

with in this situation well and and we've got another point right here well

you can see Linux is run not running on the on the physical Hardware right so

you need some kind of hardware abstraction layer inside Linux just to

make it capable to run on the microcode so basically you have two things to

maintain you need to maintain a micro curl and you need to maintain a hardware

abstraction layer to adjust to the most recent Linux versions so also this is a

big effort and basically this is one reason why most of these approach approaches are usually a step behind of

the Linux development because they just can't keep up with the fast linux development but well these were the

first approaches we had for real time in Linux and and these approaches are still around them I'm going to give you two

examples on these implementations so the other idea would be instead of moving
Realtime Linux
----------------------------------------------------------------
the work to the microcode finding a way to make linux itself real time cable or

which basically looks like a huge task well basically that means you would have

to touch every single file in the curl and I can tell you we had to but

basically you can manage that so at the first glance looks like a big picture but at the end of the day the result you

have right here is well it's just you have to real time in Linux so you have no microkernel to maintain you have no

hardware abstraction layer to maintain and you can just use the standard tools you can just work with Linux so

basically if you would have the choice to make Linux real time capable that

would be the way you would want to go so well let's have a look into some some
RTAI
--------------------------------------------------------------------------------
real implementations of real time Linux

so one of the very first approaches we had for Linux in real time was rtai the

so called real time application interface this comes from Italy from the University of Milano actually I think

actually they used it for a couple of aerospace applications and this was

actually the first real-time Linux I was using right 15 years ago or something so

this this approach is around four years so rtai is a classical dual kernel

approach so basically this this kind of implementation so okay I had a couple of

drawbacks when when using it so basically when you when you write so this is actually still around and

maintained right but the basic idea when using rtai is you write a kernel module

you write a kernel module which is basically scheduled by this micro coil but basically it's well it is like

kernel development so it's not like writing an application so it's really hard to deal with how to debug how to

get into it and basically want one thing we I had to face I had to do this for an

industrial customer well since its most of the parts are kernel space it's GPL code which is not a big deal if you do

open source software but well for an industrial customer you usually also have some closed source parts so you

always had to think about which cards you can put in userland without real time in which parts you can put into the

car with real time approaches so basically doing real time with rtai was pretty hard because most of the stuff is

done in kernel space they had some interface for doing real time in

parallel to use a space tasks this was called Alex RT well I tried it several

times so for me it was not working pretty well so I got told a good more stable these days I have to admit I

haven't I did for a long time but for me never work pretty well so basically usually

for RTA I you you have to stick with the kernel-space another problem we had with

RTA I was one of the design goals is basically not portability it's more or

less for a given number of hardware's to achieve the lowest latencies you could

possibly get this was basically one of the RTA I design goals so this means

that the number of supported platforms it's no it's quite limited yeah it's

basically x86 32-bit 64-bit a couple of armed platforms and that's it so if we

look into the RTA I design basic looks like this and this is the classical dual

kernel approach and basically you can identify that the two problems I mentioned about micro curls you've got

to maintain this real-time curl and actually you can see this real-time kernel is just handling everything which

is related to the timing critical things in the system so you have to maintain this real-time curl and right here you

have to maintain this hardware abstraction layer so these are the two problems I told you about so this is a

classical example and Linux is just completely in a different world the only thing you've got is a simple

communication mechanism to synchronize both roles but that's basically the idea

and you can nicely see in this figure that basically it's not real-time in Linux it's just real-time and Linux in

parallel on the same system that's basically what you do with these approaches well there's another approach
Xenomai
----------------------------------------------------------------
which is called cinema and this is still pretty popular so this is still used in

a lot of industrial system is still around on the market it's also quite old so I think it was founded in 2001 so

it's run about 15 years or in 2000 like it's it's more than 15 years now well

the reason why it's still there popular is that these guys had one advantage

they always had a proper solution to real time in userspace so you didn't

have to do everything in the curl so user landed it's much easier to deal with so this is basically one thing

these guys made pretty good and they had a nice idea for real time in user space

they implemented the so called skins which is basically a emulation layer for

the API of different real-time operating systems so you have a for example a

piece or skin you even have a POSIX skin so if you have a pre-existing code base for some operating system you can reuse

it with the CNMI which is pretty nice so basically these layers are not feature

completed it's a subset usually even the POSIX layers just a subset of POSIX but well you can actually reuse a

pre-existing code base for rapid prototyping porting your application very fast to say no my so that was

basically a nice idea they have a lot of supported platforms way more than RTA

does maybe also reason why it's more widely used in the field than RTI but

it's still a dual kernel approach so also these guys are using a microkernel

for doing the real-time so basically we suffer the same problems we've got the microkernel

to maintain we've got a hardware abstraction layer to maintain and well

even if you can have real-time in user space there's one additional problem you

can't use the standard c library you need special tools and special libraries

to the Overtoun oh my so even for POSIX you need to link your application

against the say know my POSIX skin so it's not standard tree lip see you always need special tools and special

libraries to deal with these microkernel approaches so the handling is way more

more complicated so if we look into the structure of cinema basically looks like
Xenomai Structure
--------------------------------------------------------
this it's actually not that different from rtai you can see it's a classical dual kernel approach we've got that

micro kernel which is dealing with the hardware right here you've got the real-time

tasks running on top of that micro code but you can see a small difference you

can see that part which is called nucleus you get and you can see that code path right so we get real-time into

user space which is much easier to handle and then the kernel part so this is a big advantage but to use this once

again you can't use any standard tools of Linux you need to use special

libraries and stuff so it's much easier but still some special tools are involved so let me summarize the dual
Dual Kernels
------------------------------------------------------------------------
kernel topic for you so well the dual kernel topics the dual kernel approaches

have been the first ones we had around on Linux for a couple of reasons because when these approaches have been invented

we didn't have preemption and stuff in the kernel so implementing real time was pretty hard so basically this was the

obvious approach these approaches are still around on the market but we have a

couple of drawbacks so we've got a special API special libraries you have to link against so this is basically one

one drawback we have special tools and libraries we need to maintain a micro

curl and the hardware abstraction layer so basically you usually step behind of

the Linux development so this is also something the big issue with these approaches and last but not least just

remember we also have high end users like financial services in stuff oil and

Linux so these guys are not running real time on a 2 or 4 core machine arm these

guys are running on a s/390 with I don't know how many CPUs so for these guys we

have with these micro kernel approaches we have a bad scaling problem because basically these micro kernels are known

to to scale pretty bad and big systems so they usually scale up to 8 or 16 CPUs

but if you get more CPUs they actually don't scale pretty well so we have one

approach to make Linux real time basically these approaches have a couple

of issues so for that reason people started to rethink if there just

wouldn't be a way to make Linux itself real-time capable and well actually we
Realtime preemption
----------------------------------------------------------------
have now one approach which is called preempt RT or the so called real-time

preemption patch so the reason for this name is what we basically do is we just introduced a new preemption model to

Linux which is called real-time of full preemption so this is why it's called a real-time preemption pitch this is a

classical single kernel or in kernel approach making Linux itself real-time

capable and well basically this approach is now around for 12 years so it's also

quite old it's widely used in the field it was basically founded by Thomas likes

nur and Ingo Molnar these two guys in 2000 first started a lot of real-time

Linux development they started to coordinate their work and the result was the real-time preemption patch well we

have a huge community for this development right now so basically the

reason for this huge community is that actually most of the parts of this

development are right now already included in the Linux kernel so 80% of

their development already made it into Linux so that's the reason why they have a huge community so basically if you're

using Linux nowadays and look into the timers the interrupt handling tracing

infrastructure pair priority inheritance and all that stuff all these features were basically originally developed for

the real time preemption patch and we're pushed back into mainline so this is the reason why we have so many uses for this

approach basically since this approach

makes Linux real-time itself you don't need anything special to know about it it's just if you write a real-time

application you just do a simple POSIX application which means you can buy a 30-year those

book like about POSIX real-time programming and basically you know how to write a real-time application for

print RT you don't need any special libraries or stuff you just use your standard c library so this is the big

advantage of making linux itself real-time capable so we also have a high

acceptance in the community for the real-time preemption patch so what's the reason for this so basically as i told

you we have a lot of features which came from the real-time development into the

mainline development so basically what we did we added some powerful features

which are not just useful for the real-time users which are useful for everyone so basically these guys made

Linux a better operating system also for all the other users so this factor then

a lot of acceptance in the community and the other reason is that well when they

made Linux real-time everything got preemptable so we found a lot of race conditions and locking problems fix

these and push them back into mainline so actually we improve the stability of Linux a lot and this is also one reason

why these guys have a high acceptance in the community so they're not just not just focused on their work they just get

some more quality into Linux so basically the mainline integration of

real-time started long time ago and actually I just check this these days
mainline integration
----------------------------------------------------------------
the mainline integration started in 2006 so this is now actually 10 years ago we

started to push the first features into mainline so and this is a original statement from Lena stalls from Cohen

summit in 2006 so the reason for this

statement was usually if you want to get a new feature into Linux he wants to

know a use case for this so who the heck is using real time on Linux so actually

one developer was telling him well I've got a customer who's running welding lasers with Linux already with the

real-time extension so well it was the answer of Leno's like well doing a welding laser with Linux is kind

of crazy but well we are all kind of crazy so I'm fine with you doing the real-time stuff so sounds funny but

basically that was the starting point of the main line integration of the of the real-time Linux development run about 10

years ago nowadays you you still need a patch to have the real-time stuff it's

like 20% of the original sites we get most of the stuff in the mainline kernel right now and you can get this patch for

every second kernel version and currently the Linux Foundation is pushing the mainline integration so the

main goal is like having the real-time capabilities within Linux within the next two years so this is basically

we're doing that development on behalf of Linux Foundation so this is basically the idea so how did these guys manage to
how to make Linux realtime
----------------------------------------------------------------
make Linux real time so we need to remember again what's the main

requirement for real-time operating system and the main requirement for real-time operating system was

preemption to achieve deterministic timing behave timing behavior we need

preemption so these guys had to find a way to maximize the preemptable sections

inside the Linux kernel so basically well this is a very simple explanation

but this is basically what they did first of all they had to rework the

locking primitives to well minimize the atomic sections inside the Linux kernel

and to maximize the preemptable sections inside the Linux kernel so basically what they did was reworking the spin

locks and finding another method to deal with these situations one idea yeah just

basically reworking the locking infrastructure basically at some point the real-time preemption patch was also

called the sleeping spin locks patch there was the reason because we had to rework all our locking primitives well

and they had another pretty cool idea another section in the coma where you are not preemptable it's basically the

interrupt context so what these guys did was instead of running the interrupt handlers in hard

interrupt context they moved it to a kernel thread so what you basically do is when an interrupt the wives arrives

you don't run the interrupt handler code you just wake up the corresponding kernel thread and the kernel thread will

run your interrupt handler which is two advantages basically the kernel thread

is interruptible main advantage and well it shows up in the process list with a

PID so you can even put a priority on your on your interrupt which is arriving so well you can give a low priority on

your non important interrupts and give a higher priority on your important userland tasks so running it into a

global thread was a actually pretty nice and pretty cool idea and actually this is also one of the features the threaded

interrupt handlers which are already available in Linux mainline so even in

mainline Linux nowadays you can decide if an interrupt handler can run in hard interrupt context or in threaded context

so actually also one of the features which came from preempt RT so well this
Realtime preemption overview
----------------------------------------------------------------
is just last but not least a quick overview how the real-time preemption

patch the single kernel approach is working so basically well you can't see

any difference to standard Linux it's just standard Linux right just with a new preemption model so there's nothing

special about it so if you do a kernel driver it's just the Linux driver if you

do a real-time application it's just a Linux application so you don't need any

special libraries or special API you just do a Linux driver or POSIX application that's it

so now I promised that I will show you

some results in a real-world example which latencies you could possibly

achieve with these real-time Linux extensions so what we did was we took a

simple arm board with a alturas iclone 5 actually we took the rocket

bored which is a community valuation kid out of that SOC and we did a couple of latency measurements and what we did was

we did the same measurements for Sena my like a dual approach and for pre and RT

a single kernel approach so well there was actually a special reason why I

wanted to do these measurements because well if you could Google for these topics you will find a lot of papers

comparing Sena my paint RT and RT AI and basically most of these papers claim

that the dual cones are way faster when it comes to Layton sees so and actually

for most of these papers well I was able to figure out that yeah the preempt are two systems out most of

the times pretty misconfigured so my idea was to get a fair comparison of

dual core and single kernel approaches and see which latencies could be achieved so we actually took one say no

my expert and one print RT export gave them the same board gave them a task and

then just try to compare the results that's basically what we did so I think that was pretty fair right

so but yeah let's wait for the results so what we did was we did I acute s so

we fired I accuse with a frequency of 10 kilohertz we took the OS a DLL latency box to do

that I'll tell you how this box is working later on and we put the system in a worst case scenario so basically

since you want to guarantee timing behavior you need to guarantee this yeah well even in a worst-case situation

which is usually high CPU load high memory load and a lot of work for the scheduler

well we achieve that with a tool which is called heck bench so this is
Hellbench
---------------------------------------------------------------------
basically how this Tool Works you've got process groups with 20

clients and 20 servers and the idea is that each client sends 100 messages via

a socket to each server so you've got a lot of inter process communication and you can tell heck bench how many groups

to run so for example if you take 40 groups is 40 times 40 processes so you

have 1600 processes doing weird in the process communication so basic

this is a real worst-case situation because yeah the scheduler continuously needs to take decisions you have high

CPU load you have high memory consumption so this is basically the real worst-case situation for your

system and while doing this while running this we just started to fire
Latency box
------------------------------------------------------------------------------------------------
interrupts and measure the latency so this is basically what we measured wipe once again I'm taking myself as a as an

example like we get an external event like this morning the alarm clock was ringing I need to react to that and get

out of the bed basically this is what we what we did on the embedded board we just fired an external event and did a

simple driver who needs to do this reaction and what you can do with the

latency box is this latency box can record all the samples you get and do a nice histogram for you because this is

also quite interesting just not to get the worst case latency also the variety of latencies you could get well

basically once again taking me as an example today it was quite easy but well I might go drinking tonight so tomorrow

it might be quite hard to get out of bed so it's not always the same latency so you have done some variance in it right

so this is the so-called cheater and that that's why one we want to record all the samples and put them into a nice

graphic and this is basically what the was a DLL latency box can do for you so

this box can fire interrupts in a pre-configured frequency so in our case that was 10 kilohertz so it has an

output pin drag in your signal you send this signal to your test system your

test system needs to trigger pin which is connected to an input pin on the latency box and the latency box will

just measure the time in between and record all the samples so we did this

for 12 hours which is not very long but it's the bare minimum to get a good idea

of the real-time behavior of the system so this is really the bare minimum you could take it's not really long but it

can give you a good idea so this is basically the measurement we did firing interrupts with 10 kilohertz getting a

reaction from target system and measure the reaction time the every measurement has been taken

with the latency box so actually what we did was we had to use cases and the most
Use cases
--------------------------------------------------------
important one was the reaction time of a user space task and this is basically

the real-world example if you need to react to an external event basically you

need to synchronize your user space tasks with some interrupter stuff like some field bus interrupt or whatever but

basically you want to do your homework the real calculations in user space so

this is basically the most important example so that was the reason why we took this as the first measurement

measuring the latency from the external event arriving into your application and

triggering the GPIO which goes to the latency box again so what we started

these these measurements on say no my these are basically the results so as
Results
----------------------------------------------------
you can see we did a nice histogram well you can see the latencies on this axis you can see the number of samples right

here so now the average was like 30

microseconds reaction time but basically the average is not the number we are

actually interested in right so we want time in guarantees so if we want to to

look into timing guarantees we need to check for the worst case well you can

see the worst case latency right here this small peak so we had actually one sample which was round about 90 95

microseconds that was the worst case latency we got on that device with the 10 kilohertz interrupt so let's say 95

microseconds worst case latency which is actually not too bad for user space application so now we did the same

measurements on brimmed RT

you can see well the variety so the cheater is a bit bit bigger

yeah right you but you can actually see this is the worst case latency we got

which is pretty much the same we had for the dual curl like it's even slightly

better but I would say it's pretty much the same with less than 100 microseconds

what we could achieve so well basically this can prove that we don't have that big difference you can find in a lot of

measurements which are around in the internet between dual coil and single kernel approaches so in this test case

we had pretty much the same latencies on the dual kernel and single kernel approach and well actually one thing we

try it right here is well since VM tarty it's a standard Linux system so we can

actually use all the standard Linux features so we were wondering what would

happen if each is isolate one CPU that was a dual core system what would happen

if you start isolating CPUs for just handling that interrupt and see what happens so basically that was the next

measurement we take we've taken doing the same measurement with an isolated

CPU so you can see it gets slightly better like from ninety to what eighty

microseconds now this is basically well you don't hit a specific worst-case because it's running on a different CPU

but this is done pretty often real-time systems that you just isolate a specific

core for for some specific tasks so well since there was a standard Linux use

case it was quite easy to isolate this core so we've got this comparison I

think the most important graphs are these two right here the green one and

the red one the red one is just a preamp RT without any special configuration and

the green one is cinema without any special optimizations you can see

basically the latency we got for the users based tasks was pretty much the same which is actually pretty cool when

compared a dual kernel and single kernel approach so we did another measurement

and what actually I was not really happy with that measurement well you might get

that if you look into that slide right what we also did was we measured the kernel latency and what was the reason

why I was not happy with that measurement because basically in my opinion what you basically do you

compare about full-featured Linux system with the reaction time of a micro Cal

well you can discuss about that but in my opinion it's not a fair measurement

because there we compare Linux in the micro curl so basically in my opinion we compare apples with peers but basically

the results were actually quite interesting so I would like to show the results right now because this is the

result for say no my and well if you if you look in the Internet when we get a couple of measurements in

the internet were just do kernel approaches we are 300 or 400 percent faster than a single kernel approach and

basically yeah I was expecting something similar right here so we got 30

microseconds for say no my well and if we check out what we achieved with grams

RT without any optimization was like well it's slightly better than the the users k-space latency but well we we

need to remember we just go into a kernel thread right here so it's different it's not that big but now if

we start to optimize this use case and just once again start isolating the core

we even get down to 60 microseconds a latency for the for the brand RT which

is basically if you compare a micro coil and well a full-featured Linux system I

think this comparison is not too bad 60 microseconds is actually pretty fast on

that kind of CPU so the difference is not that big as you would expect and not

that big as a couple of measurements in the internet claim - so actually we're getting pretty close with the single

kernel approaches so now we did one last measurement on on

the criminal agencies well and basically the idea was we were running on an arm platform and well I was saying well we

compare apples piers but well if you go with the microkernel you might be willing to accept a couple of

limitations on your system so I was thinking about could we also put some

limitations on the brand RT system and see if that could somehow improve the

latencies well the the idea I had was just I was just curious how that would

improve the timing behavior just trying to use the f IQ feature of the arm CPUs
FIQ
------------------------------------------------------------
which is a hardware feature it's a special interrupt vector on arm which is running in its own context so it's very

limited in the things you could possibly do it's living in its own world so it's very limited what you can do but well

when I'm willing to to accept limitations basically this might be an

option so what we figured out was well we've got 10 microseconds or even less

average latency and you can see the worst case is also around about 30

microseconds and that was actually a pretty interesting number because if you compare this it's also 30 microseconds

so we are quite sure we just hit a hardware latency in this measurement we

didn't have to take the time to track this down right now but we've seen this on similar architectures with cortex a9

CPUs we see the similar latency so it really looks like a hardware thing so
Final comparison
----------------------------------------------------------
well this is the final comparison of the kernel sight so taking into account that

we compare a full-featured operating system with a micro coil actually these

numbers are not too bad and well we need to remember and that's that's a conclusion with a pre and RT patch we
Conclusion
---------------------------------------------------------
have a single kernel approach which is basically nowadays the de facto standard for Linux and and it's getting

integrated in the mainline Linux development it's pretty simple to use you can use

standard c library knows nothing special it's available for every second kernel version so it's the standard it's easy

to use and it's basically for the most of the use cases it the micro kernels

don't have better latency so basically the latencies you can get are really comparable so basically if that should

give you a recommendation you know pre and RT would be the way because it's the

standard and the latencies are pretty good you you could possibly get and last but not least well if you're willing to

take limitations instead of going with the micro kernel solution you could also check out which features your hardware

is offering like the FI queues on arm you can use that we've we've got support for that in Linux but you need to be

aware of that the things you can do with these hardware features are actually pretty limited so well there was

basically all I wanted to tell about real time Linux so it was pretty higher-level I know but hopefully it was quite useful

for you to get an overview about real time Linux so well basically thanks for

listening and well feel free to ask any questions