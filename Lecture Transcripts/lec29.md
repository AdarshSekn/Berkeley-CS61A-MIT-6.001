Transcript


okay good afternoon I'll stop saying that I'm still connected yes we are all
right good morning Oh excellent okay as you see behind me here we have
the list of four programming paradigms that we're talking about this semester we've finished the first two which are
from the perspective of this course the major ones that we're spending a lot of time on client-server which is today's
topic is just this week it's one lecture and some lab and homework time and it's
not a minor paradigm in the world it's only minor with respect to the
curriculum of this course it used to be pretty minor even in the world before
the internet but now practically everything you do you run a client on
your computer and then you run and there's a server running somewhere else
like at Google or Yahoo or at eeks that
berkeley.edu or something okay so I have
two different windows here both connected to star you can join in this
little network if you ssh to your class
account that star then run STK and load I am client and then I am enroll quote
double quote that is 128 32 . 42:27
double quote space five to eight eight - that's a lot of magic numbers we'll talk
about them in a bit and what you can do once you've done that let me do it
myself I am one twenty eight thirty to forty two
twenty seven five two eight eight - okay
great connection refused what Oh eight two two yes okay I don't think
your word for it
why isn't this okay I give up
sorry hate computers
oh yeah I'll get that okay so now I can
say sinned right oh whoops I am that's
what it is okay I am CS 61a oops you see there hi there
whoops of course that didn't work I am quote CS 61a you see I never okay great
so everybody's sending me hello messages and you can send each other messages
okay yeah right
so while everybody's playing with this let me explain something about these
magic numbers so this is first of all
hey - - so you may be wondering if you
have to connect to star before you can do this why does it also need an internet address that magic things
starting 128 32 is an Internet address
and the reason is that in principle this
program will take connections from anywhere but in fact
come on Beatles lyrics we want Beatles Oaks in fact the lab computers have
firewalls attached so that people from out that's better so that people from
outside can't connect so you have to be inside the firewall which means I think could be probably on some other machine
on the okay on the second floor but you
can't be you know here on air bears okay
so okay who's never seen an Internet
address like 128 that 32 etc before almost everybody has alright it's
different from what you usually see which is a host name like star dot see us that berkeley.edu but those are
actually the same computer every computer on the net all your laptops
included have an Internet address okay
Wow all the internet addresses in the
world that start 128 32 belonged to Berkeley ECS I have actually eaten three
orders of pot stickers that are sitting like 18 but that was all I ate for that meal I had along with me three of my
high school students are visiting for the summer and they also had three hours of pot stickers and there's tiny little
hole-in-the-wall restaurant that had the best pot stickers in the world and Louie the chef who ran the place got mad at us
for using up his entire stock of pot stickers because we hadn't warned him we were going to do this and it turned out
the next table over from us were a bunch of people from Lucasfilm who ordered pot
stickers and Louie said well sorry those people over there taking them already so we we bartered
some of our pot stickers for a tour of the Lucasfilm computer facilities which
was pretty cool anyway so every address
that starts one 2832 belongs to berkeley EECS that's cuz we got there early in
reserving internet addresses so we have the whole big chunk of them the five to
eight to two that's a fairly arbitrary number that was assigned to us when I
started running the server so let me see if I can actually back this window up
oops oh it's this fight no it's this way
there we good okay so all the way back
at the top it should say oops
every time somebody comes and goes it I can probably make it stop doing that
hang on let's see no no that's not it
how about this one what Oh
all right that'll work
right thing yes yeah
all right nope didn't work yeah well
everybody stopped doing things for a second oh I see that might work whoops
that was shift s to show less okay so
here's where we started the server I said I am servers start and it told me
its IP address and a server port number
no and basically it's a random number
the way the way these things usually work is you start let's say a browser
and you say to connect to you know berkeley.edu and your browser knows that
because it's a browser and it's using the HTTP protocol it should connect to
port 80 because that port number is assigns to the the web protocol HTTP
protocol if you're talking to your bank or somebody now you might be going to a
page where the URL is HTTPS or the S stands for secure and that's a different
port number which I don't know but your browser does so typically the port
numbers are built into the client software and how do those numbers get
assigned until fairly recently there was one person who did it you sent an email
to Jon Postel and say I need a port number and he'd send you back one but
now there's a whole committee it's the Internet I can't Internet
Consortium for Assigned Names and numbers which is this International
Committee that was only theoretically international until really quite
recently it used to be all people in the US but now it really is international
after some agitation from foreigners no
that's good that's a good thing and they're in charge of assigning numbers but they have sort of small numbers like
80 if you say SSH its port 22 right yeah
right those are the only ones that memorized these big numbers like five to
eight to two are officially reserved for
private use so if you're you're having some little local protocol that you're
playing with like ours then you can ask
your operating system to assign you a port number and it will out of that range of fairly large port numbers so
what we're doing of course is instant messaging instant messaging is a little
messy actually in the world there ought to be a port number for instant messaging but actually as I understand
it tell me if I'm wrong there's a port number for AOL instant messaging and a
different port number for Microsoft instant messaging and a different blah blah blah blah blah Skype who has Skype
on their computer Skype is really really good at getting through firewalls and
the reason is Skype actually will pick some port number for the Skype you know
protocol but and if your how your computer is just a plain old normal
computer it'll probably let that through but if your computer is professionally managed
won't because you have a firewall software that prevents connections except on certain ports so it falls back
on pretending to be various other protocols and if all else fails it pretends to be a web browser because
everybody let's that through the firewall so Skype is really really good at perverting this port number system
but for the rest of us we just pick a particular port and connect to it okay
I'm about to show you some code that's full of messy details the messy details
have to do with the way the internet works and let me take a minute to joy
you the picture or how the internet works yeah this is the Internet no no
it's it's several layers of abstraction this is an abstraction diagram okay so
the actual internet hardware that's on your computer which might be an Ethernet port or a wireless antenna or something
like that gives you local unreliable
packets a packet is like a burst of
information that you just throw into the internet and hope for the best and your internet hardware only knows
how to talk to people who are physically very near you on the same network so you
guys laptops can all talk to each other but your internet hardware doesn't know
how to connect to star dot CS that Berkeley dad ed you because that's not on this local network so local means
really really local and then we have something called IP which is the
Internet Protocol the reason the
internet is called the Internet is that it's not a network of computers it's a
network of networks okay so air bears or the little local
piece of air bears that's served by can we see them somewhere there's antennas
up here anyway served by local routers that little local network is connected
to all the rest of the networks in the world by the Internet Protocol so what the Internet Protocol is all about is
understanding those numbers 128 32.4 digit when t7 the notation by the way
there's always four numbers connected by three dots each number is one byte of
computer memory eight bits so it's between zero and 255 decimal so we're
exactly halfway up at 128 so the internet protocol says okay let me look
at this IP address oh it's on my local network I can connect directly or oh
it's not on my local canet work a local network let me see who is on my local
network that knows how to connect to somebody else and that will be your router like in your house maybe you have
a wireless router you know or in this building we have a router and so on and
the router knows how to connect every place else so for almost everybody in the world the algorithm is very very
simple it's step one am I talking to myself that's a special case I don't
have to go through any network at all step two am I talking to somebody on my local network if so I can connect directly in
hardware nope send it to my router my router knows how to connect to the
entire rest of the universe okay and your router also has a very similar
thing it how to connect to the next round or a long until you get two really important people like you know AT&T net or
somebody and then the routing algorithms get more complicated by the way
depending on what state you grew up in ro ute might be pronounced route or
route who says route who says route
interesting okay I guess there must be a California ISM but no matter where you come from the machine that does it is
called the router and I think that's probably because Rooter is those people
who clean out your sewers you know when I get confused okay what IP gives you is
world wide unreliable packets unreliable
because if we want to get a message from here to MIT we don't just send it from
our router to mi t--'s router it doesn't work like that we get through like maybe
five hops before we even get off the Berkeley campus and those are all computers that have to work and then we
take several more hops to make our way across the country and then back down through you know my t's routers so the
particular computer we're talking to and same for anybody else that you might be connecting to and any one of those
computers might crash so that's why they're unreliable and furthermore if I
send out a packet and then I send out a second packet to the same place and I'm
hoping they're going to be received in that order there's no guarantee that they'll be received in that order because every packet you send out the
some more complicated routers midway in between make different decisions about
which direction to go through the network because of you know local
measurements of how much traffic there is at this millisecond so it's entirely
possible that your second packet gets there first and then whoever's the recipient might get all confused
so because of these problems the unreliability about failure all together and unreliability about ordering of
packets we have something called TCP which is the transmission control
protocol and TCP is an abstraction layer
that provides you with worldwide
reliable streams a stream of information
right so things come in order you stay connected they the model the abstraction
is that there is sort of a long-term connection directly from your computer to the other computer and back to
connections actually and you can just keep throwing data down that tube and it
goes directly to the other computer that's the abstraction even though it doesn't really work like that making
this happen is very very complicated making it happen
quickly turns out to be very very very very complicated and it was one of the
hardest things about getting the network to scale up from the old days when there were you know dozens to hundreds of
computers to now when there's you know hundreds of millions or maybe billions of computers on the network I don't know
how far we've gotten but a lot so TCP is hugely complicated if you take 122 right
isn't that works you'll spend a lot of time learning about how to make TCP work
so these two things are often referred to together tcp/ip like that are what make the
Internet actually function now when I say reliable if a huge
nuclear explosion goes off from the center of the country then your
message may not get there so it's not reliable no matter what but under normal conditions where computers sort of only
fail locally instead of all over the place at once it's going to be reliable and that's that works basically not
because your computer knows which other computers are dead that's not the case
you have no sort of global knowledge about how the network is connected what
happens is you send out a message and part of TCP is that the other side sends
back an acknowledgment yes I got packet number bah blah blah and if within some
number of seconds you don't get an acknowledgment you send it out again and you just keep trying until it gets there
now by the way that means that at the other end they may get the same packet
more than once because maybe that first one was just really slow but it does get
there eventually so part of the job of TCP at the
receiving end is to put the packets back
together in the correct order using these packet numbers that they have and if duplicate comes duplicates come in
just ignore them so that's part of what makes TCP complicated ok so now what we
do is we have above this a bazillion applications
you know Firefox SSH etc and those
things provide you know the World Wide Web and so on okay so that's the
Internet when they first started talking about how to make networks talk to each
other a bunch of professors invented a
diagram like this that had seven layers of abstraction which people refer to as
the seven layer cake who's eaten a seven layer cake
oh my god go to David's in San Francisco and tell them you want a seven-layer cake but nobody actually implements it
as seven layers and the reason is that each level of abstraction here
introduces some overhead time and so by
the time you get from here up to here and seven layers it's way too slow and cumbersome to actually get any work done
even this if you do it completely straightforwardly is typically too slow and sometimes you'll see little back
channels where this layer talks to this layer directly and so on again that's all 122 I've said far too much about it
already but now you know basically how the internet works oh except for how did
it happen that I said connect to star dot Siesta berkeley.edu and my computer
figured out to connect to 120 8.30 2.40 2.27 well up at the application layer
there's an application called the domain name service the NS and basically my
computer knows how to talk to a domain name server typically a local one so I
like a berkeley.edu one but it also knows your your browser for example
knows how to connect directly to name servers for all the top-level demands
what's a top-level demand it's like edu or calm or org and the people who run
those name servers know how to connect to the next level like Berkeley did you
or you know google.com or something and then those name servers know how to
connect to the next level like CS stuff Berkeley I did you and then there are CS name servers that know how to connect to
start out CS and so finally you got to Adam a name server who sends you back the internet address for the computer
that wanted to talk to you and that all happens kind of behind the scenes so you're never really supposed to type in
internet addresses you only type in host names and it all works and the reason
it's scales is that host names have you know host dot little net dot medium size
in that dot big net because if everybody
had to pick a host name there would be too many duplications and everything just like if you want a gmail account
it's too complicated to get excuse me a name that isn't already in use all right
okay great let's see if we can look at
some code okay
here's I am server start excuse me this
chalk dust getting to me um so what does it do it calls make serversocket right
here a socket is an abstract data type that has to do with the internet and
sockets include port numbers among other information so it's an ADD data
abstraction and this year is a selector for its socket port number is a selector
for the socket abstraction it gives you back a port number given the socket so
this format thing prints out the message that you saw up at the top of the server
window server IP address that on it's like a port number at the top okay now
we've at a quarter to three finished all the unimportant stuff and we're getting
to the really crucial part of understanding client-server programming which is this
when socket ready does this it says when
socket ready is part of the network abstraction by the way you are not responsible for knowing how a network
connection is set up things like when socket ready you don't have to know about that but if you're interested in my lecture notes in
the course reader for today is like six pages of the STK
internet interface that you can read at your leisure but that's just for people who are curious about it the important
thing is this what windsock it ready does it says okay
I have nothing to do I've set up this socket and now I don't have anything to
do until somebody connects to me so if I look at my server
window oops
I was interesting
alright let's try this again
okay notice it's the same Internet address but it's a different port but what I'd instead of all connecting what
I'd like you to notice is that I have an SDK prompt and I can go ahead and do computations right I'm not sort of
sitting in a loop waiting for connections to come that's the crucial point here because what when socket
ready does is not sit in a loop waiting for the socket to be ready it tells the
operating system hey operating system kick me when a
request comes in on this port on this socket so which socket well server
socket is the first argument to win socket ready that says which socket do I
want to get kicked about and then comes this this is a procedure of no arguments
we've seen those before in implementing delay and force there's a technical term
for a procedure with no arguments it's called the thunk dhun cake for some
complicated stupid reason having to do with some metaphor that somebody made up 50 years ago the metaphor has faded into
oblivion but the name remains because it's so cool funk
well when socket ready says is okay when somebody makes a request on this socket
call that procedure and furthermore do so in a new thread what's a thread it's
a way of letting two things happen or many things happen at once in the same program okay so in my SDK that's running
right here well right there on that other window there's one thread that
typed in SDK prompt and I typed in plus t3 into it and it called the evaluator
and gave me back five well if I if somebody makes a connection request a
new thread is started by the operating system this is a feature that operating systems provide
is multiple threads all running within the same program having access to the
same data okay start a new thread and what should that new thread do it should
call this procedure this is called
callback okay here in this board is the things I really want you to learn today
so let's look at server client callback
in the other programming paradigms that we've looked at so far there's a
sequence of events you can sort of trace your way through the program first this happens and this happens and this
happens no no no okay that's not true in the client-server paradigm nothing can
be happening or many things can be happening all at once okay so when you
make a search request to Google you think you're the only one who's making a search request right now no it's you and
you know 20,000 other people or something and so on Google servers
well I was about to say Ally I was about to say there's a process that's running
20,000 threads one per connection that's actually not true what happens is the
server you connected to has redirected you to a different server and so you
know maybe there's 200 different servers running each of which has 100 is that
right yeah a hundred threads within a process okay something I mean I don't know what the exact numbers are I'm
making the numbers up but basically they have a lot of servers going and also a
lot of threads in each server ok isn't
this cool you know when you call win socket ready it returns right away it
doesn't sit and wait for it just puts an entry in a table in the operating system saying when this event
happens do this okay so it's a kind of
data directed programming except that the set of people waiting for things
changes dynamically when we did that table in the data directed program a table of operators and types we set that
up at the beginning and then it's fixed here this is a table that's dynamic because people keep connecting and
disconnecting you know with search requests and stuff
okay everybody with me that's what a callback is it's a procedure that you
use as an input to another procedure so when socket ready is a higher-order function right because it takes an
another procedure is an argument but that procedure doesn't run until you
know two hours later when somebody gets around to connecting to it to our server
right and then the operating system
sends a message to SDK and STK says oh yeah I'm supposed to run this thunk
right here and does so okay so it means
you have to write your program in little tiny pieces so here's what to do when
this event happens here's what to do when this event happens and so on and
those little tiny pieces are typically operating on shared data so you have a
problem which we're going to look at in I think two weeks of what happens if two
threads try to modify the same thing in a data structure at the same time and
that turns out to be an enormous ly messy problem so one of the reasons why
functional programming is so good because you never do change things in data bases in functional programming on
the other hand here we're trying to model in the computer events as they happen we're trying to
respond in real-time to to unpredictable events like somebody connecting to our
service and so we typically don't do it
in functional style we do it in this you know clobbering the database style and
therefore we have to be worried about two accesses to the same thing at the
same time so this is like my favorite example which we'll talk about in a couple of weeks is two people try to
reserve the same seat on the same airplane at the same time okay actually
quite likely because you know when you go to reserve a seat on an airplane you
look at the map right and you get you asked for the best seat that's still
available which is either the window or the aisle depending that's closest to
the front of the airplane right everybody wants those seats so it really
is not such a coincidence if two people ask for the same seat at the same time and our software has to be able to deal
with that okay now you know what a callback is it's a very very versatile
technique window systems when I Here I am here's my little oops my little
screen cursor zipping around up here in the top right corner and I come over here and I click on this title bar and
this window comes to the front okay why did that happen because as I clicked the
mouse the window system sent an event
notice to the x-term program that's in
charge of this particular window saying you have come to the front somebody has
asked to pull you to the front please redisplay yourself in the front and
previously the window manager has set a
callback for this event right when I get call to the front message run this
procedure now they probably didn't do it in scheme they did it in some language
that doesn't have first-class procedures and what they do probably have is
pointers to procedures but the procedure has to have been written ahead of time you can't sort of create a procedure on
the fly with lambda so this procedure here my callback has access to the local
variables of I am server start I don't think it actually uses any local
variables here but it could have done if you wanted to and that won't be the case
when you're doing this after this semester you'll have a more impoverished
environment to work in but you will even though you won't be able to create procedures on the fly you will be able
to use pointers to procedures the memory address of a procedure as a data type
and you'll do that for callbacks okay so
this thing is printing out lots of logging messages you know I connect it to so-and-so I did this so I'm so
connected so-and-so dropped out here's a message that I'm sending it does that because you guys are going to work with
this in the lab and this will help you understand what the sequence of events is as you play with the system okay so
what exactly is it that we do when a request comes in well first I say
duplicate the socket so there's a pipe that's the you know send me a connection
request but as soon as I get a connection request I make a new pipe just for you so a new socket and then I
call handshake which we're going to find somewhere here it is okay so now I say
accept the connection and that you know sets up some data in the system that I
that I'm the program that's to port such and such so port from
client port sooo quiet so a socket is bi-directional and it's bi-directional
by virtue of having two ports which are unidirectional the port coming in and a
port going out and then I say get
request port from client so you might
think that this has to wait forever but it doesn't because the reason we got here to handshake is that you made a
request so there is a request already waiting for us to look at if not if get
request return false that's an error shut down the socket one of the things
you'll notice if you read this code is lots and lots and lots of error checking
and that's because all these errors really happen computers crash you know
you send in a connection request I am enrolled blah blah blah and then you
lose your air Bears connection or something so then we would end up here
so that's why it always does error checking but if we do get a connection
we say request received and now in these requests this is a selector request
action a request has a bunch of fields in it and one of them is the action what is it we're trying to do and it had
better be hello hello is the only one we accept from a brand-new client if not
shut down the socket but if it is then
we look to see who is this coming from Who am I and we look at the clients we
already have and if your name your login
in other words is already connected then we send a message saying sorry from
server to the source of this request sorry because only one person can have
the same login connected at the same time so otherwise it's a new person I
send a message from server to the person who's connecting saying welcome
so welcome is the response to hello okay
now this thing actually waits for a
message to come back from the client and it only waits for you know some number of seconds and then it gives up and
returns false but if we do get a request back I look to see if the action part of
the request is thanks if not shut down
the socket if so then I can do register
client so you sent me a hello message I
sent you a welcome message you sent me a thanks message that's called a three-way
handshake the point of it is to make sure we can talk to each other one of
the homework questions this week is for you to explain why it's not good enough to do a two-way handshake hello welcome
well I sent them a you send a message to me I send a message to you it all works why do we need three of them that's part
of the homework figuring that out okay and then the rest of it is handling
client requests and this is when we register a client
here we go setup client request Handler and then within that there's an internal
definition of client request Handler and here we really are using local variables
namely name and client socket is going to be used all the time in here so if I come down here and control meta
F this is the actual body of setup
client it says when port readable the input
socket of the input port rather of this client socket so in socket input is a
selector on sockets it says I'm listening on the input port and then this is a callback client request
Handler okay so oops
omit it I don't know I see which all metabee here we go client request
handler doesn't take any inputs it's a thunk again so this is the callback for
[Music] messages coming in so what do we do when we get a message well there are various
kinds of message the most common one is send a message to somebody so that's
when I say I am person text and we have
to handle that we have to look up the person find that person socket in the table and sort of forward the text on to
that person all these people standing out in the hall are waiting for this class to be over so you can come in for
the next class reminding me therefore that it's three o'clock so that's it see you next time next virtual week which
starts Wednesday
UC Berkeley