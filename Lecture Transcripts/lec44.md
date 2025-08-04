Transcript


okay good afternoon we come a long way huh
I hope you're feeling like your heads are bigger than they used to be more
stuff crammed inside so I have an hour
to summarize the whole course which of course I can't do but I'll try to put it
in some context for you journey is writings okay journey is writing about a review session for the
final which will be at the usual lecture time next week but running two hours
here and as a final exam that that you
should an old final exam that you should take ahead of time and that's what they'll be discussing at the review
great anything else no good yeah come to the final right Oh
final exam all individual the usual rules for sheets of notes our usual one
per chapter style so one slice of what this course is about just want to remind
you is programming paradigms I don't know that I ever defined the word paradigm but maybe you can get a sense
from what we studied of what it means it's sort of a way to set your head to
do programming you say you know for the purposes of this program I'm going to
think in such a such a style and the main ones that we looked at were
functional and object-oriented programming we looked at both of those as abstractions as sort of you know
here's the paradigm and also under the hood to see how we implement those
things and we looked in much less detail
but just touched on client-server programming which is very related to the question of
parallelism that's the hot topic and computer science right now and
declarative this last week also known as logic programming programming language
people these days don't talk as much about paradigms as they used to because
actual programs in the wild tend to combine bits of different paradigms but
that doesn't mean just throwing things together any old way it means combining
them in a disciplined way where you really do understand what it means to to
write a function something that doesn't remember its past history and always
gives the same answer for the same inputs and so on as a completely
different example of this when you take
61c and you're learning about how a processor works on the inside you're
going to see pictures that look a little bit like this
and so on there may be like five or six or seven stages that look like this
we're inside the processor there's a not
not a lot of memory not gigabytes but a little bit of memory they'll be the
registers that are visible to the programmer and some other internal
registers maybe you know hundreds of bytes altogether and that memory feeds
values into a cloud of function so there's going to be a bunch of circuitry that does various things but the stuff
in that cloud is all computing functions in fact it will be computing boolean
functions with predicates because the inputs are single bits one and zero like
true and false and there are just bazillions of those and then after that comes another batch of state memory and
so on and that that whole thing is a pipeline they're not going to call it
State memories we're going to call it registers and they're not going to call it cloud of functions they're going to
call it things like adder you know multiplier but it's what it is or the
cloud of functions and then more registers and so on so this is kind of a
in the hardware level a combination of object-oriented paradigm with state and
functional not programming but functional hardware so these are ideas
that are just going to come back over and over the other big idea this the central idea if I had it say in one word
what's this of course about is abstraction and if you look up hey oh nothing's on the screen because I didn't
do this if you look on the screen you'll
see a handout that you got back on the first day which says you're not supposed to understand this yet but that was then
this is now I know you are suppose to understand it the book talks about abstraction a lot but never actually
defines it and that's intentional because abstraction means a bunch of different things so it's not easy to
define for the purposes of this handout I picked the most controversial
definition I could think of so this definition is an attempt to wake you up it says voluntary submission to a
discipline so that's like joining the Moonies you know except it's not like
joining the Moonies because you don't do it for life you do it for this program
that I'm writing right now so you say I'm going to program functionally or
object-oriented lis or whatever in order to gain expressive power that's a paradox I'm agreeing to refrain from
doing certain things because refraining in that way gives me more expressive
power you'd think it would be less expressive power so if there's anything
you've gotten out of the course I hope you've gotten what it is I mean when I say that if you're programming
functionally or if you're programming object-oriented lis or if you're programming declaratively you have more
expressive power than if you just do the first thing that comes into your head
okay and and that really is the big lesson of this course some programming
languages sound less and less these days but still some try to enforce a
particular programming paradigm so there are purely functional languages
in which you can't change the value of a variable there are object-oriented languages like
Java is one of them in which there's no just procedures all there is these
methods of classes and so you have to make a class even if you're only going
to have one instance of it and so on so all of these things some languages try to enforce but it's much better if the
enforcement happens in your head so if instead of fighting and pushing the
limits of the paradigm you're saying how can I make this paradigm serve me and then the rest of the handout I'm not
going to go over every single thing on it but there's a bunch of them is for various abstractions what does the
abstraction focus our attention on and what does the abstraction hide from us
so in functional programming the focus is on repeatable input-output behavior
that's the definition of the function and composition of functions as the way
you build complicated programs out of simple pieces as opposed to first do
this then do this and do this so composition of functions is the big combining message for the primitive
functions to get interesting programs what's hidden is side effects which are
happening down inside the computer and also hidden is the innards of a
procedure once it's written so once you've written a procedure it's just as if it's a primitive you don't look at it
you only look at what am I supposed to give it for input and what is it promising to give me as output the same
is true for all of these things every abstraction focuses your attention on certain things and hides other things
from you and that also the idea of hiding something from you sounds you
know like something you wouldn't want you want to see everything and some of
you maybe a lot of you will remember having trouble the first time you saw
recursion because you didn't feel like you understood it until you traced every
step down at the lowest level if you understood how it is that you know level
five calls level four and that caused level three and that goes level two and you actually had to trace through all of
that every time and finally I hope you got to where you just trusted that
recursion works it's like that for all these things it's not that it's hidden in the sense that you can't know it you
know it's not a secret but you're not thinking about it right now because the whole point of computer
science is to make it possible for you to write computer programs by thinking
about the problem you're trying to solve instead of thinking about oh this
computer has 32-bit words which means I can represent blah blah blah blah blah you don't want to think about your
computer you want to think about the problem before there was computer science there were computers and you had
to program them at that level of knowing what every last vacuum tube was doing
and then they invented programming languages and that really was the beginning of the idea of abstraction
although they didn't realize it the first higher than machine language level
languages like Fortran the people who invented them thought of them as just a
shorthand for machine language so they were thinking machine language in their head and writing down Fortran and that
was helpful but it became much more helpful when they probably without even
noticing shifted over to thinking in Fortran the same way when you're
learning a foreign language you start translating it to English in your head and then there comes a time when you're
thinking in French or thinking in Spanish or whatever it is it's the same thing with abstractions and programming
languages so that's what we mean by hidden that you're you could think about
those things but you've learned that it's more productive not to right now okay so I'm not going to go through the
rest of these but you should you still have this handout you know it's in lectures slash summary
and you should read the seven little things that it talks about and just go
through those and refresh your memory about some of the big abstractions we've talked about okay so speaking of
abstractions now this is a picture of computer science in terms of levels of
abstraction and there's a cloud up at the top which is theory which is in a
way the most abstract of all but it's not built on applications it's built on
mathematics so it's sort of off to the side so CS 70 is a course in the
mathematical foundations of computer science theory and then the 170 172 174
that series is about theoretical computer science we made a beginning of
that the week that we talked about orders of growth you know that this procedure takes theta of N squared time
or whatever that's one of the foundational pieces of
computer science theory another one is the theory about what computers can and
cannot do at all never mind how long it takes that's called automata theory and it's
really fun if you like math you don't like math you'll wonder what the point is um maybe but there is a point um
as John Bentley says in programming
Perls the remember the picture I put up about the Radio Shack trs-80 versus that
create supercomputers that came out of programming pearls another thing from programming pearls a great book is it
says knowing a little theory can stand you in good stead when your boss asks
you to do something that's theoretically impossible so instead of saying gee I
don't know how to do that let me go dry you can say I'm sorry sir but that's just not possible you can
point to where it says so in a theory book okay leaving Syria aside for a
moment there's there's this hierarchy of levels this isn't anybody's official
pictures it's just my picture of levels somebody else might show it a little bit differently but not that much so up at
the top we have applications this is the thing that we're trying to get the computer to do and if we're lucky we
write our application in a high-level language typically the high-level
language is implemented in a low-level language I think I talked about this a little before but let me remind you low
level is not an insult you know high level is not praise they're technical
terms a low level language is one that exposes how the hardware works to you
that lets you know you know an integer is 32 bits wide and we have these
mechanisms built into the computer and so on and so forth and you can point to
a particular specific place in computer memory and say give me this whereas the
high-level language tries to hide those details from you so that you can write your program in terms
of the problem you're trying to solve so scheme is an example of a high-level language C is an example of a low-level
language Java tries to have one foot in both worlds it's sort of in between and
you know their event benefits to that too because it means you can do the
low-level stuff when you really have to but you can ignore all that some of the time opinions differ on how good a
design job they get let me just leave it at that and then below that is the
language that the computer actually understands called machine language and there's assembly language which is sort
of a human readable abbreviation for machine language they're basically the same thing and there's a dotted line
there because it's really the same level of abstraction as architecture except
machine language is the programmers view of it an architecture is the electrical engineers view of what makes this
computer of Pentium and that computer of PowerPC or whatever architecture is
built in terms of circuit elements called logic gates these are boolean
functions things like Anthon or not and everything else is built up out of that
logic gates are both in terms of transistors that's a big big should this
line between logic gates and transistors is a huge abstraction barrier because at
the logic gate level the hardware is well behaved so if you look at a wire
inside the computer it's got a 1 or a 0 and that's that at the transistor level
that's not the case there's noise there's bouncy switches there's voltages
that are in between the zero level in the one level the all kinds of things there's just little bits of randomness
that come in or you know interference from the machine next to the computer
somebody's running the lawnmower outside or something so all that messy stuff that electrical
engineers have to deal with or at the transistor level and the optical
engineers through heroic efforts provide us programmers with these nice
well-behaved almost logic gates I'm saying almost because even at the logic
gate level there's a little bit of thinking about hardware that architects have to do for instance if you take the
output from one of these logic gates and connect it to too many inputs of other
functions its voltage drops a little bit and it stops looking like a 1 or a 0 so
you have to think about you know the messy real physical world a little bit even with logic gates but much less than
with transistors and how do transistors wear transistors work by magic just like
primitive procedures so the way we teach
you computer science is from the top down so in 61a we're programming in a
very high-level language and we're looking not at all about at how
computers work 61b you think a little bit about how
computers work in particular in 61 D you start thinking about efficiency the
topic we just touched on here but you're going to start to really worry about you
know how long something actually takes in the world and it's a little more practical in that way but please don't
forget what you learned in this course because as I've said several times before it's much much easier to take a
correct program and make it run fast than to take a fast program and make it correct so start by thinking about the
computation you're trying to do and then think about the efficiency things even in 61 B and then 61 C Oh 69 B is taught
in Java which is this sort of one foot in each camp language 61 C they use Java
briefly but mostly C and assembly language machine language for the MIPS
architecture which is just chosen because it's simple as computers go and
it takes you down a little bit into the logic gate level the mainly logic gate
level is the architect people 150 and 150 to by the way I should say the
actual pieces of hardware that you can look at if you open up the back of your computer you see one of these little
black tips that has what are we up to millions of transistors so it's not like
you're going to open up the back of your computer and see a transistor okay
but in terms of the design that's sort of what you're working with
how transistors work is electric circuits which is 40 and so the 140s and I guess
I should have written e1 4x up a little bit higher I think it's the one 30s or something that's actual device physics
so this in EE classes on device physics and it all starts with physics 7c quantum which I don't believe in so I
think it's software all the way down
okay so partly this is to reinforce the
idea of what abstractions are all about and why it's important so if you're trying to write an application you don't
want to be thinking about logic gates okay partly it's an answer to the
question can I take 61 C before 61 B and
the answer is the official answer is yes you can if you speak Java but there's a
reason that they're in the order that they're in it sort of makes sense as a sequence we think some schools do it in
the other direction they start with how the architecture works because they think that if you
start low and build up then you'll believe each level like by the time you
get to recursion you'll believe in it because you'll see you know how the bits move around in the computer but we start
at the high end because we think we're putting our best foot forward that we want you out there in the world to have
as your first instinct thinking at a high level and you need sometimes you do need to think lower down but start time
and work as high as you can and that's how you're going to get the program written and debug the soonest even out
in the world oh yeah
this technical meaning of abstraction I don't know if I said this before not is
different from what laypeople mean when they talk about something being abstract
to laypeople the stuff in the middle that you can actually open up the back
of your computer and look at that's concrete and both software and quantum
physics are abstract and it's not that that's a wrong definition but it's not
the one we're using we're talking about what sort of structure is built in terms
of what other structure and it isn't um [Music]
historically I guess it starts with
architecture and logic gates because before there were transistors there were
other kinds of circuitry that they built computers out of and the the pioneering work was done around here and so they
did kind of move out in both directions from there but now that that pioneering
work has been done in today's world everything is built on top of the level below it ok now for the secret of
success you are most likely in your
career going to inhabit one particular level of abstraction most of the time so
maybe you'll be an application program or maybe you'll be a language designer maybe you'll do operating systems which
is sort of off to the side here maybe you'll do architecture and so on and
that's fine so you're going to have an area that you're most expert in and most comfortable with and have the most fun
doing but the engineers I'm including
software people in this the engineers who change the world tend to be people
who are aware of what's going on above them and below them in the abstraction
hierarchic because if you are designing
an architecture to pick something in the middle your work is going to respond to
pressures from above and pressures from below I learned this from Dave Patterson by the way so the pressure from above is
that the users of your architecture are going to want to do different things
with it so they're going to want to be able to handle massive databases in
parallel they're going to want to be able to do very fast 3d graphics they're
going to sort of make demands based on the kinds of programs people want to write you're also going to respond to
pressure from below because both limitations and new capabilities will
come from the lower down level for example right now one of the big
constraints in computer architecture is temperature and so the more gates you
put into a circuit the more heat you have to dissipate somehow and you know
one time they thought well you know of course we're going to run into limits there's the speed of light and things but we're way shorter the speed of light
and we're still running into limits because of heat dissipation problems and
multi-core processors are in part a response to that that it's possible to
build so because it's not just how many transistors it's also how fast you run
them so they would build circuits that were faster and faster and faster and that means they got hotter and hotter
and hotter and now instead we back off a little on how fast each individual core
runs but we put a bunch of them in there so you know the goal is a decade from
now each processor on your desk will look maybe not so different from how they
look today but there'll be a thousand of them on your desk or 10,000 all in the
same size box is the idea and because each processor will be running slowly we
won't hit the heat limit so that's an example of responding to pressures from it's not just an architecture every
level when you design a programming language even a high-level programming language you have to be cognizant of the
fact that the hardware people are giving you multi-core machines and that affects
how people write programs even in your high-level language and you have to try to abstract away the parallelism so that
the users of your language can write programs still in terms of the problem they're trying to solve rather than in
terms of understanding how to divide it up into pieces one thing we've seen like that is MapReduce write MapReduce is a
piece of software that deals with tremendous amounts of complexity in
terms of things like load leveling and dealing with processor failures and
figuring out where things on the distributed disk system and so on and it
hides all that under a level of well tell us what the map function is and
tell us what the reduce function is we'll get the job done so that's an example of a not a programming language
but a library that responds to pressure from below pressure from above of course
is the applications that people want to write so scheme which started like as a
tiny little jewel of a programming language that was stripped down and
theoretically beautiful and could do all kinds of programming paradigms and everything is getting more and more
complicated as people start actually trying to write applications in it and
they start worrying about things like um
how do you know whether the character that you just read from the keyboard is a digit or not that used to be really
easy there were ten digits 0 through 9 but now there's Unicode which supports
different languages different human languages and it turns out different human languages have different kinds of
digits and so even just something as simple as that is
now much more complicated because of the pressure to have programs that work all over the world in people's native
language so at every level that you work it's very very helpful if you're
comfortable at other levels of the abstraction hierarchy if you sort of keep up with the literature at different
levels especially the ones right near you but all the way up and down really
so that's the secret of you know being someone the world will remember 100
years from now is to be able to anticipate what your level of
abstraction is going to have to do in a few years because of what people are doing now above you and below you in the
hierarchy um all right it's time for
your problem okay remember I told you to bring something to write on so this is a
binary search tree all right what I want is range takes a binary
search tree and two number is low and
high and it returns a straight linear
list the sequence in order of the numbers in the tree that are greater
than or equal to low and less than or equal to high and furthermore does it efficiently so if I ask for the range oh
let's say 65 now 64 to 83 okay that's
the range that I want in this tree okay so I'm going to start by looking at the
value at the root which is 37 and I'm going to say hey 37 is outside
the range it's too small right therefore I'm not going to look at any of these at
all that testa tree I don't have to look at okay 37 is too small I'm going to
look at 72 now that is in the range so sadly I have to look in both directions
but when I get to 81 oh no no let's do
it this way better example when I get to 80 or and I say oh that's too big so I
don't have to look at this guy and so on okay go ahead write it I'll wait
you
you
you
who's finished Wow nobody
yeah I'm sorry you're supposed to return a
straight list of the numbers in order
ascending left to right just like the
tree
now what do I say
you
got a hand up for you get it on now what
do I say con because it's one element
that I okay why did I ask you to do this
because I'm going to tell you a story about this problem quite a bit before
you were born I was teaching 60 C it's a
long time ago it's more or less the course that's now 61 B data structures the programming
language we used was C and one semester
I gave this problem as a midterm question nobody got it
so next class I came in I said what's up
with this how come nobody got this I was really hard you know and I said okay
take out a piece of paper the way I said to you just now write it and scheme and
they all groaned at me because they hadn't seen scheme in a year you know
year and a half whatever it was and you
know that was back in 61 a now we're doing this other course let's put the scheme and I said hush write it in
scheme and you know what not all of them but about half of them were able to
write it in scheme class or at least mostly righted in skiing
maybe they didn't get the upend kind thing quite right and they said yeah but
that has nothing to do with what you asked because you asked us to do it in C and then C we don't have all this
abstraction stuff so I said
she's supposed to be looking at both boards at once yeah never mind if you
don't speak this language it doesn't matter
yeah
arms getting tired
you
whatever
okay and and they looked at me and they
said but she doesn't have a pinned and cons and left branch and all that and I
said you know how to make linked lists they all said yes and they said well you
know these are just simple procedures you can write those too or not write them I would have been
happy to see that answer on the midterm and it's you know it's a perfectly legal
C program and you do have to do a little more you know the same as in scheme you
have to define left branch and right branch and data so how come nobody in
the class did it that way well because they tried to write it with global
variables and loops and it just never
occurred to anyone in that class even though we're dealing with a tree data structure to write a recursive function
and why is that it's because you can see culture and sadly also in Java culture
real men don't write recursive functions
so every once in a while I overhear a
student conversation in which somebody refers to 61a as the scheme course it's
not the scheme course it doesn't matter if you never see scheme again in your
life you are going to see trees and if
you believe in recursive functions I don't care if you're writing in COBOL you will get the job done better if you
understand what a recursive function is than if you're afraid of them okay thank you for a great semester
[Applause]
UC Berkeley