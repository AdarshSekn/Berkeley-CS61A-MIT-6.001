Transcript


hey good afternoon uh welcome back hope you had a good spring break and all rested unlike me
um important administrative announcement this Saturday is the CS61A dim sum
brunch um this is a tradition that started many many too long years ago um
when during the um adventure game project somebody said "What's a pot
sticker?" Um so we decided that an important educational experience was dim
sum um uh for those who don't know about it
they come around with trays with little teeny plates with you know two or three or four tidbits and you say "I want some
of this and some of this and some of this." And in real traditional old-fashioned Chinese dim sum places uh
they just count up the plates on your table at the end to write you a bill but in modern um American we don't trust
anybody dim some places they make note as you're going along um of how much you
ate so that's how dim sum works um I have to say it's not very vegetarian
friendly or kosher friendly or halal friendly um that is to say there's lots of
groundup mystery meat that turns out to include pork and shrimp um but it is
delicious um and no we're not treating um should plan to spend $10 to
$15 um and we're going to meet up outside the Berkeley BART Saturday
morning um I know uh this seems ridiculously early to you um but if you
wait until noon you it takes hours to get in especially with big groups um so either meet us at the Berkeley
BART at 10:30 or else um meet us at Legendary Palace in Oakland um at
11 um I would tell you all about how to find Legendary Palace but you all have
computers so shouldn't be necessary you can do the same Google that I did okay
um this week we're talking about two related topics today we're looking at
another programming paradigm called client server um so the way this course
is structured there are two paradigms that we look at at length and we've done that they are functional and
object-oriented programming and there's two more that we barely touch on so when
you come out of the course and you've forgotten the details you should know that this exists and you should
understand sort of the big ideas of each paradigm and we'll talk in a minute
about the big ideas of the client server programming paradigm which is very very
important um in computer applications today where
you know you connect to Facebook and you're you have a client on your
computer and they have a server on their computer and you talk to each other um so instead of the computation happening
in one place it's sort of distributed over a network um okay oh and later in the week
we're going to be talking about concurrency um that is different things
happening in parallel and how that gives rise to programming predicaments
um that it's really best if you understand ahead of time because once you introduce a concurrency bug in your
program you're never going to find it um you can ask anybody who's taken 162
about this about all the allnighters that they've pulled in labs because of concurrency bugs so you really want to
understand that and they go together because when you have a server that's supporting many many clients at once uh
you're doing concurrency and so these kind this kind of problem arises a lot in this
particular way of organizing a program okay so I have two windows open i'm
connected to um star.cs
um and uh in principle you can connect to the
server that I'm about to start up from anywhere on the internet but in practice uh the instructional computing folks
have a firewall that prevents connections from anywhere else so if you want to play along you have to SSH to um
star so I'm going to say over here I am
server start and it's going to tell me two
magic numbers it's going to tell me my IP address which
is
128.32
42.27 and it's going to tell me a port number which is
42275 okay so um those of you who have laptops uh if
you SSH into star and um
load 61Alib you know twiddlecs
61a imclient.com IM for instant message um
something you all know about uh when you say I am enroll that's an e um you have to give your host in
quotation marks uh and that's because it has digits and decimal points so it
looks like a number but it's a badly formed number because it has more than one decimal point so we have to tell
Scheme to treat it as a character string by putting it inside double quotation marks um so 128
32427 is the internet address of um star takes the instructional server
on which we work in the lab um 42275 is just an arbitrary number that
the operating system picked for our use as a port number
um ah good there's somebody here let me sign on my other
window so I can say oops stop
that i am enroll
128.32 427 close
quote 42275 this one isn't in quotation marks because it's just an integer
um interesting okay um I wonder who this person is whose
name is supposed to be Brian Harvey that's not me this is me
um okay so we're already seeing uh some security problems in this uh protocol uh
but that's okay i can say I am quote
CS61A TE hi welcome
to instant
messaging it says okay and on his screen it should pop up a message and over in
my other window we can see all the messages going back and forth
um
yeah right
oops okay so here's the message that I
got interesting so um unlike unlike real
IM software this version is instrumented with a lot of extra debugging printout
so you'll see a lot of junk scroll up on the screen about I got this message and I'm doing this um and that's so that
when you're working on it in the lab which you will be this week um you will have an easier time of debugging what
you do ping okay i am quote
CS61A SE quote
pong right um okay
so uh this is the this is the program that
we're looking at today as an example of client server programming
um I'm going to um
just Whoops not maximize i didn't mean that i meant
minimize just to be a little less uh interesting um and so that I can pop
up in another terminal
um and look at the code okay so first of all um probably
most of you are already familiar with all this but just a brief detour into
how the internet works um this is not a class about how the internet works uh there is one of those
it's E122 um but
128.32.42.27 um that's just um
a 32-bit number divided into four pieces of eight bits each uh they thought it
would be easier to remember and type internet addresses if they put in those
dots um everything that's
128.32 something is a computer in the E ECS department at Berkeley so we own
128.32 which is um 2 to
the 16th addresses 2 to the 16th is 65,000 and some odd so that's a block of
65,000 addresses that we own and we have some other ones too um the entire
internet address space um using this protocol is 2 to the 32nd addresses
which is about 4 billion um we are running out not because there are four billion
computers on the internet there aren't but because big chunks are allocated a
chunk at a time and they're not all full so we may not have um 65,000
computers in our bit of address space maybe we only have 20,000 computers in
which case that's 45,000 unused addresses that nobody else can have because you know they belong to us um
the theory is that sooner or later we will have 65,000 computers because you
know each little dust spec computer that the um remote sensing people build is
going to have its own IP address um there's a solution to this problem called IPv6
um that has 64 bit addresses instead of 32bit um I
don't remember how much 2 to the 64th is but it's more than the number of atoms
in the universe i think I think that's right uh so we're not likely to use
those up anytime soon till we start exploring parallel universes
um 42275 that's just a number that nobody
has to know except the client and the server so what happens is uh when you
say I am enroll in scheme um your computer sends
a message to star.ex takes um saying I
want to connect to port 42275 and the operating system on star
looks up um which application program has registered
that port number and connects your incoming request to that program which in our
case is the IM server um so you connect to the IM server by knowing its port
number you know its port number because I wrote it down on the board and you copied it um in general the way real
systems work is that um there is an assigned port number for a certain kind
of service and everybody just knows or rather everybody's computer just knows
what that port is so if you want to make an HTTP connection that's port
80 if you want to make a Tnet connection which nobody does anymore that's port 22
those are the only ones I have memorized um but you don't have to have them memorized because um the software that
runs on your computer has them memorized so when you run Firefox or something uh
and you type in a web address it knows to connect to port 80 unless the web
address starts HTTPS which stands for secure HTTP which
has a different port number which I forget but somebody knows um so those
are low numbers like you know two-digit numbers for these well-known ports um
the higher numbers are reserved for private or experimental protocols like
our IM thing so that's a private protocol um if we uh wanted to make a
million dollars by distributing our instant messaging software competing with AOL and Yahoo and those guys um we
would make a request for a registered port number um we would make that request to I can I
guess which is the internet consortium on assigned names and
numbers and they would um give us a number that thereafter everybody would
know and well we would distribute free client software that would have that
port number built into it um and of course our servers would know
what the number was okay so that's host addresses and port
numbers um so what happens when you enroll you send a
message [Music]
um well let's start actually right at the beginning here's IM server start
this is how I started up the server so what does it do it prints a
message it calls make server socket a socket isn't a number like 42275 it's an
abstract data type that includes a port number and a bunch of other things
so make server socket um that gives us a
a socket which is an abstract two-way internet
connection or kind of repository for connection we're not connected to anybody yet people are going to connect
to us on it um and now we print server IP address and server port so we get the
IP address from the operating system um and right here socket port number is a
selector for sockets that gives us the number
42275 okay now do I expect you to memorize all
these details about what a socket looks like and everything no absolutely not
none of those details are important for you to remember it's important for us to walk through it for you to get a sense
of how it works but don't remember the details if you actually are interested
in the details of networking in SDK uh in my lecture notes um
pages 332 to 334 in my copy are three
pages of documentation of STK networking primitives
um and again none of this is stuff you have to know it's only there in case you're interested and you want to play
around with it
okay now comes our first example of the most important idea that
we're going to talk about today so if you've been things going in one ear out the other listen up
uh when socket ready is a networking primitive in SDK
that takes two arguments the first one is a socket so we asked for a socket we
got one and now we're using it in this when socket ready and the second one the big
important idea so important that I'm going to write it down if I could only find there you go is a
call back procedure so when socket
ready doesn't sit there stuck until somebody
connects to the socket when sock get ready returns instantly but it has
established a matching up between our server
socket and this procedure
okay this is a procedure of no arguments and the operating system is
going to poke STK when a connection request comes in
for port number 42275 the operating system is going to
look up port 42275 it's going to find this socket it's going to find the user process
associated with that socket and it's going to wake up that process and say hey do this and STK
uh represents the do this in the form of a procedure unsurprisingly
um in those other languages uh you can't generate procedures on the
fly the way this lambda is doing but what they do is they have something called a pointer to procedure so if
you've written a procedure ahead of time you can use that written ahead of
time procedure as an argument to something and that's how they do callbacks in those other languages um
but in this case for example uh you'll notice that the procedure that is now
highlighted includes within it a reference
to server socket which is a local variable it's just inside this procedure
because it was created uh oh no I'm wrong it's a global variable i lied but it could have been a
local variable in which case this lambda would still have access to it we'll find
some things like that later on so forget I said that for now but uh the important
part is this is a call back procedure what that means a callback procedure is
a procedure that the system this is a kind of
handwavy thing the system something that somebody else wrote not you is going to
invoke when a certain event occurs in this case the event
is socket ready meaning somebody requests to connect on this
socket okay so what does this procedure do this lambda well it prints a message
new client connecting and then it um then it does this interesting
thing it says make me a copy of that
socket what's that for well many different clients are going to
connect to this server at once and each client is going to have
its own socket so we can keep them apart pull them apart right um so if two
messages come in right at once it doesn't matter because one message will go to one socket and one message will go
to the other socket um socket dupe is an SDK
primitive that says make a copy of the socket so now we have a special socket
just for this client who's connecting right now and then we call handshake
which I'm going to look at in just a second okay questions about what a call back
is programmed with callbacks before some context hardly anybody okay a few people
have this is a very very very ubiquitous concept it's not just for writing um
network servers so for example um if you're writing a program that has
a user interface that has a window and in the window there are buttons you can click with your mouse and there's little
rectangles in which you can type text and all that stuff um associated with
that window are probably a bunch of callbacks
one for mousecllicked um one for key
press and if it really wants to get fancy your program can have a call back
for key down and another call back for key up
um and that's important if your uh user interface lets people type you know
control alt shift blahy blah you can keep track of
all those modifier keys that way
um so all of those things work with callback so a typical
program that you see that you buy in the store you start it up it takes a while
it sits there with that splash screen you know saying this is a great program send money you know and then the real
window pops up and then after that the program does nothing it's sitting there
doing nothing waiting for a call back that could be from a bunch of sources it
could be something you do like click the mouse or type some text or it could be
on a network connection or it could be um some input output on your local disc
finishes or something like that so there are many many ways that things happen all of it is done with callbacks and
what your program is doing is just sitting there saying um I'm going to sit here and wait until some I get a call
back about something all right so let's find Handshake here it
is um it has a lot of comments which I'm going to skip
over uh what we're about to do it's called the procedure is called handshake because what it's about to do is
something called the three-way handshake
um I send a message from the server to the client then the client sends a
message to the server uh nope i have it backwards the client sends a message to the server
server sends a message back to the client client sends another message back to the server so
um how does this work we say let port from client be socket input of sock and
port to client be socket output from sock so here a port is like half of a
socket it's a onedirectional connection between us and the person on the other
computer and get request um that's not an SDK primitive it's um
something that's part of this IM package that waits for a connection and and says
okay let me find the data and parse it into pieces and then comes something
interesting it says if request is false that's what notrep
means then shut down the socket otherwise do some other stuff um
so what you're going to see is that there's a lot of error checking
in this code mostly the procedures we've written so far the whole first half of the
semester are written on the assumption that nothing's going to go wrong um I mean not that the user can't
make a mistake but that the hardware is going to work um that's an assumption you can't
make in networking network connections fail for all kinds of reasons maybe the other computer that
you're talking to crashes or maybe in between you and that
other computer there's somebody in the middle that your connection is going through that crashes and maybe you can
route around that and maybe you can't depending um so network connections are really really flaky and network code
always does a lot of checking to make sure we're still connected
okay so print the message and now messages have uh different parts um
there's an action there's a sender there's a receiver and there's so the
text of the message so here we're looking to see um if the action part of
the request is the word hello so what we're expecting is that the client is
going to send hello to the server um if it sends anything
else we give an error message and shut down the socket and go away um because you know it's a client
for some other system not ours if that works
um then we look at the source of the rec who is making this request
c61A-xy and we look to see if that person is already included as one of our
clients if so then uh we send a request saying
sorry and shut down the connection
uh because you can't have the same name as a client twice on two different computers two different
clients um so let's say we get past that test so it's a hello message from
someone we haven't seen before then oh then we still make sure of one
more thing oh no we don't i'm sorry then we send request
make request is a constructor for an abstract data type um and the source is
the word server so it's a message from the server and then the destination
uh of the of this message is whoever is trying to connect to us the action that
we're saying is welcome and there is no text there's just the action so we got
hello we send back welcome and send
request returns a value um basically true or false meaning did
it did that work or not if it didn't work shut down the
socket okay now we wait for another message to come
in so we get request client fork if we don't get one
um shut down the socket otherwise we make sure that um this new message from
the client is has an action of thanks so client sends
hello server sends welcome client says
thanks one of your homework questions this week is why do we have to do a three-way handshake why isn't it good
enough to just send one message each way why do we need two messages from the client so you can work that out um and
then finally that all worked so now we call register client which just puts the client in a list so we associate the
name you know CS61A whoever it is with the
socket corresponding to that person and that's done that's it then we
return okay all right now
[Music] um let's look
at register client which is right
here how do we do that well we add client to
table um and then we call setup client request handler name socket so let's
look at setup client request handler this is all part of what happens when you imroll this is what the server is
doing on your behalf so here's setup client request handler name client socket
um this is an internal define of a procedure called client
request handler takes no arguments so it says get the input port
get the output port get the request if there is no request forget it otherwise
received request and there are two message this is like a dispatch
procedure in object-oriented programming these requests there are two different actions we know how to do um and the
first one is send message in which case
oops in which case we look up the um
port for the person you're trying to talk to uh and then
um right here we do send request from the source to the
destination uh receive message uh and then request data which is
whatever the text is that you're trying to send so we send a request over the network to the client and the action of
that part of that request is receive message
um the other possibility is that the action is log
out so one is [Music] um send message and the other is log out
if it's logout then we just remove this person from the database otherwise
um it's an unrecognized action and we sent back a message saying
I don't know how to do that you sent a request that you know isn't either log
out or send message
and that's the end of that internal definition and now here's the actual
body of setup client request handler it says when port readable so this is
another callback situation so which port socket input of
client sock and what's the procedure the callback procedure it's client request
handler so this whole thing could have been a lambda expression uh the reason they did it as an internal
define is just that there's a lot of code in that thing and if it started twothirds of the way across the screen
with a lambda it wouldn't be very readable um
so client and server um callbacks the client also has a bunch of callbacks so
let me um bring these windows back oops
okay so here I am and I'm uh enrolled as a client and
meanwhile I can do computations in SDK right uh I can do anything I want in
SDK and also receive messages at the same time how come SDK can do both of those things at once uh because of
something called threads um threads used to be called lightweight
processes which is kind of a good name because it explains the idea a process is something that your computer is doing
it's some program that's running on your computer
um a thread is like a process that shares
memory with other processes so you start up a program and that program can spawn
off various threads to do different things so in the server
um back here no back
here um when we said way back at the
beginning well also for this when port readable when we say when port readable that returns right away and we can go on
and do other computations when the port is readable when a new request comes
in the system will start a new thread and invoke the callback procedure
in that new thread so it shares all the programs global variables and everything
but it's a separate computation from the main SDK readal print loop
the server is going to have many many many threads one for each client plus
one for the read val print loop because I can do that same trick in the server i can type in scheme expressions and get
values back while this is running because we set up a special thread for
each task okay so that's the other part of this client server paradigm so second
big
idea okay if you understand what a callback is and you understand what a thread is
that's pretty much what I would like you to understand about the client server
paradigm and understanding what a thread is means understanding that several
different things are happening in parallel that share access to global
data among all the different threads that's going to be important next time when we talk about what can go wrong
when different threads share the same data um okay what have I forgotten to say
all right let me give you the five minute story about how the internet works
okay so um the internet
hardware provides the ability to
send unreliable
packets to the local
network okay what that means is your computer is connected to a network like
right now your computers are probably all connected to airbears okay um
so your internet
hardware basically knows how to send messages to only one place which is the Airbears
server that's running in this room and furthermore the messages may
not always get there um so that's not so good that's a and
and oh what's a packet a packet is just a bunch of information but just one bunch there's no idea of a continuous
stream of information back and forth there's just it's more like tossing a ball than like having a phone
conversation okay so on top of
that we have the
internet protocol otherwise known as
IP um and what that does is it provides an address for every computer in the
world and it provides a mechanism for messages to be forwarded from one
computer to another by the way this is a very very remarkable thing that everybody in the
world who has a computer well everybody in the world who has a computer that's sort of in the
middle of things on the network not you you mostly don't have to forward messages because you're at the very end
of a thread that you know doesn't that only connects to one other place but everybody who has a computer that's
connected to a bunch of places takes messages from just anybody could be a competing company and passes
them along and doesn't read them at least we hope so um there's some evidence that commercial
ISPs actually do read your messages as they go from your computer into the
network in order to sell information about you to advertisers but that's a whole different
subject but this system just sort of grew organically that everybody cooperated with everybody when it came
to making the network work um and it's quite a remarkable example
of largecale human cooperation uh doubly remarkable these
days when we have the um idea very prevalent in society that nobody ever
does anything nice for anybody unless they get paid for it um and that really was not the case in the building of the
net okay so the internet protocol gives us the ability to
send unreliable
packets worldwide so IP has not solved the
reliability problem all it's done is extended your reach from people right
around you to the world um for some purposes that's good
enough um I send a message to an internet time
server saying "What time is it?" Right which your computer does
periodically if that message doesn't get there so what you just try again okay it's no big deal um but if
you're trying to have a a if you're trying to send a file a big file over the net it gets divided up into little
chunks and if some of the little chunks get there and some don't that's not so good so now we have
the transmission right control
protocol TCP and what that does is it gives
you two-way
continuous ordered
reliable streams
okay so built on top of unreliable packets we now have reli well it isn't
100% reliable if the computer you're talking to crashes then you know what can we do but um if some computer in the
middle crashes TCP will work around
it so it'll try again it'll keep trying until it gets through and furthermore it
puts a serial number on each little packet so that the receiving end makes sure they come in order it does a lot of
very complicated stuff tcp is very hard to get right um if you just read the specification and implement it you will
end up with code that runs way too slowly to be used um and so there's a
whole science of coming up with wrinkles to TCP to make it run fast enough um and
then on top of that we have an
application that gives you you know whatever it gives you a web browser or a file transfer protocol or something so
this is called the network stack um in the literature somebody long time ago
came up with a seven layer stack um this is a three layer stack one two three
really well four if you count the application layer
um and this is called TCP IP which is an abbreviation
you've probably seen this is what it stands for all of this goes on behind the scenes in your
computer um hardware there's lots of different ways
of um building networking hardware depending on uh what problem you're
trying to solve so right now um you are all using
uh Wi-Fi connection um which is a you know
radiobased way of communicating with a server um but maybe at home in the dorm
if you live in a dorm there's an Ethernet port you can plug into right in the newer dorms anyway um so you can
plug a cable in and get onto the internet that way the Ethernet is um a
bus a collection of wires that sort of runs around in one local place and uh
that hardware has its own protocols associated with it so one of the
Ethernet issues my favorite example about this is what happens if two people try to send a message over the the local
Ethernet at the same time well the answer is they kind of mix up with each other and get garbled and
so everybody on your local net reads this and says "Uhoh this is a garbled
transmission." And drops it and in particular the computers that were trying to send a message can see their
own message as it comes back and they say "Uhoh that didn't work." And then
each computer waits a random amount of time and then sends it again the random
amount of time is important because it makes it likely that next time the two computers won't collide when they're
sending this message if it just kept trying boom boom boom then they would keep on colliding over and over again
and the message would never get through so this is the kind of thing that people think about at the hardware level higher
up in software we think about things like how much redundancy do we need in order to get this illusion of
reliability in the connection um and how do we make sure things come in in the
right order and so on okay um you're going to play with this in the lab
there's both lab exercises and some of this week's homework is about it and then we'll talk about concurrency on
Wednesday
UC Berkeley