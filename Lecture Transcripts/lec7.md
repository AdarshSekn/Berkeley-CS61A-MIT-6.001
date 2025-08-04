Transcript


two administrative things one of them is we now have a room assignment for our
midterm they were going to put us in different more than one room but luckily
a few people have dropped the class and we now all fit in 2050 vlsb so that's
where exams are going to be the first one is two weeks from today we'll talk more about that later drop-in tutoring I
had a visit the other day from a student who went into the CSU a office the one
that's on the outside of the third floor entrance looking for drop-in tutoring
apparently she had an unpleasant experience which shouldn't have happened but could have been avoided by me
telling you earlier although it is in the handout where to go for drop-in tutoring we have hkn ADA Kappa nu which
is the EECS Honor Society and Epsilon Pi
epsilon which is the letters of science CS major honors society and both of
those groups offer drop-in tutoring they're right next to each other in 3:45
and 346 so to all so that's the place to
go if you want help besides my office hours and your TAS office hours I also
every once in a while I get an email from a student wanting to pay somebody to tutor them in this class and I don't
have a supply of such people but the honor societies would be a good place to
look that's what you want although you know before you spend money on tutoring
you should make sure you're availing yourself with me and the TAS and so on and you can ask questions on Piazza
which some of you are already doing about the project which is another administrative announcement in case you
missed it you are this week working on programming project one
Volume one of the reader the little skinny one okay that's it for
administrative thing the topic for this week is efficiency which we hardly ever
think about in this class because we
want you to get your program to work before you worry about our faceted 61b is very largely about efficiency you'll
spend a lot of time on that next semester but we do spend one week on it
just to introduce you to the ideas the general ideas that people use in talking about the efficiency of programs and
every once in a while we'll actually have something to say about a way that you can organize your program to get big
efficiency again again it's not our main focus it's not our main topic and it's
not the main thing you should be worrying about right here it is okay so
how do we measure the efficiency in time of some algorithm that's whether the
program using this algorithm runs quickly or slowly how do we measure that
and the obvious answer turns out not to be a very good one the obvious answer is
you look at your watch and start the program and you see how many seconds it takes and that's your measure of how
long the program takes to run and the problem with that as a measure is that the actual running time on a computer is
affected by very many things other than the actual algorithm so it's affected
first of all by how many years old your computer is that's a very big factor
another one is what else your computer is doing and you may think it isn't doing anything but that's not true if
you look at a list of the running processes which all the operating systems let you do more or less easily
you will always find twenty or thirty things their programs running with names
you've never heard of you have no idea what they're doing and the efficiency of your program
is very much affected by what all those things are doing so to talk about the
efficiency of an algorithm what we do is we don't talk about this is how many
seconds it took instead we actually look at the algorithm and count how many
primitive constant time operations is that so for example for our purposes all
arithmetic operations like plus minus those things take constant time that's
actually not quite true if you're doing in very large integers now if you take the factorial of 500 or something and
then you try to multiply that by 3 that actually takes the time proportional to
the number of digits and the numbers roughly but we're not going to think about that because mostly either you're
using small enough numbers or you're using floating point representations as
ones with powers of 10 and those things really are constant time so here's an
example up there I have a procedure
squares that you've seen before it takes a sentence full of numbers let's what I just do
takes a sentence full of numbers and returns assent another sentence full of numbers in which each member is the
square of the corresponding number in the interest okay very simple program so
what I want to do is measure of the running time of this program and I'm
going to say in squares what are the primitive operations there's empty
question mark constant time there's if deciding which branch to take constant
time there's first constant time there's
but first constant time now square here
is not a primitive operation it's defined up in the top line of the screen
but if you look at its definition it just does one multiplication so it too
is constant time so that's one two three four five things with a constant time
and then this is something a little
tricky and I wouldn't expect you to know this but sentence actually turns out to
be pretty complicated in the way it's implemented and it has different running times for different cases but it so
happens that in this program the way we're using sentence in which the first
argument is a single word only the square of one number and the second
argument is a sentence namely the result of the recursive call this call to
sentence takes constant time also that's one two three four five six constant
time operations plus the recursive call
okay and recursive calls on the but first of the sentence which is a sentence that's one shorter so how many
recursive calls happen in this example where I gave it five numbers how many
calls two squares where they're all together here some fives and some fixes
on a vote this is five it says six okay
a little more sixes I say six also there aren't six recursive calls but there's
six calls because this one right here maybe that you aren't cancelling this is a call with the length equals five so
five four three two one and zero there's a recursive call with the empty sentence
okay but that call for the empty sentence only does to constant time
operations it does the empty and the if and then it just returns the empty
sentence and it doesn't take any time at all okay so okay so for squares a
sentence of length in we do six n plus
two constant time operations right
because the five calls with non-empty sentences have six operations plus a
recursive call and then the empty sentence one only does two operations so
the running time of this program should be proportional to six n plus two okay
yeah any questions so far
great Oh is a hand up yeah what is n I'm sorry
it is the length of the sentence that you give as input the number of words
other questions yeah yes the two is for
the if and the empty when the argument is the empty sentence and the very last recursive call okay um okay we're going
to see by the way in just a moment that this is sort of too much information and
we're going to get to that because just
a hint coming attractions we're going to end up saying okay the amount of time is proportional to the length of the input
and that says that the DOB that turns out to be the best thing you can say about this okay
now
here I have a function called sort and what it does is it takes a sentence of
numbers and it returns a sentence containing the same numbers but ordered
from smallest to largest okay so we're going to look at how long
sort takes well this is a little bit
trickier because sorc has one empty two
if three first four but first constant
time operations it has the recursive call to sort but it also calls this
helper function insert that's defined just below it we're going to discover that insert is not constant time so
first let's look and see oh well first let me explain the algorithm to you this
is called insertion sort and it's what you do when you're playing cards and you
have a pile of cards that have been dealt in front of you and you pick them up if you're me pick them up and you're
the left hand because I'm left-handed maybe you pick them up in your right hand and then one at a time you transfer
the cards from this answer that hand and so we start by taking any old card and moving it to the other hand then we take
another card and we put it either before or after the one that's already there and we take the
next part and there's three places that might go at the beginning inside the other two or at the end and so on we for
each randomly chosen whatever order we got them in card we insert it into an
already sorted hand okay so the trick about insert is that it takes one new
number and it has this argument sent
which has to be a sorted list of numbers so since is already in order first the
left and we're inserting one new number into it right okay how long does this
take it's a con so it's a three-way choice here's the base case sent is
empty in which case we return a one word
sentence containing the number so this says that to be constant time if sent
isn't empty then we can compare the new number we're inserting with first of
sent we can say is this new number smaller than first descent and therefore
smaller than everything in sent because we're assuming sent is already sorted so
we're comparing the new number with the smallest number in cents which is also the first number okay so this is to
constant time operations first and less than and if that's true we do this
sentence which is constant time because
it's adding one word in the front of the sentence if we were adding the word in the back of the sentence it would take
longer turns out well we'll get to that next week why that is and here's the else clause and what else Clause does is
it says okay this new number is not the smallest first of sent is smaller or
equal SS so my result should start with
first of sense because first of sent was the smallest number in sent and it's
also smaller than num which is the new one we want to add so therefore the first number in the result should be the
first number in sent and what do we combine that with a recursive call in
which we're trying to insert the same new number into but first offense so
basically we're going to march down this sense until we hit a number that's bigger than the new one and we're going
to end up inserting it right there okay let me um actually show how this
works moment by saying please work
cert and see this again so it's a little
tricky here we go so I'm calling set up sort with the whole center that you
can't see this but it says is the sentence empty no it's not is the new is
the first of sense so because I'm sorry the what sort does
is it takes first of sense and uses that as num in the call to search okay and it
also sorts but for system so what we're doing here we're looking at this sentence 623 five tenths of hundred
seven and before we can do anything else before we can call insert we have to
sort the but first attempt so first thing we sort 23 5 107 and that starts
by sorting 507 and that starts by sorting 107 and that starts by sorting 7
and that starts by sorting the empty sentence right down here so we call sort
bubble of them sorts the empty sentence that's the base case of sort it returns
an empty sentence and now we can start inserting so we want to sort this
sentence so we end up calling insert with none is first of sent which is
seven and sent is the sorted version of the empty sentence which is also the empty side so in that situation we're in
the base case insert right away we're inserting into an empty sentence so it immediately
returns the sentence of length one with a seven in it and because insert returns
that that's what sort returns so that innermost sort here returns sentence
with seven system sorry sort through these and so that's this value here so
seven was just the first number that happened to be in the sentence not necessarily the smallest so now I'm
going to take I'm sorry the last number that was under sentence it goes right to left so now I'm going to take the number
before it which is a hundred and I'm going to try to insert 100 into this
sentence so insert says is if since
empty no it isn't okay let me compare
num which is 100 with first descent which is seven it asks the question is
num smaller the first descent the answer's no num is 100 first of sent to
seven so num is bigger so therefore I'm
going to do this recursive call to insert I'm going to insert 100 into the
empty sentence that's the base case for insert so it returns this sends with
just 100 and then we're back here
inserting the set by sentencing sorry to seven which is now the smallest number
of the ones we looked at in front of the results from insert so insert returns
seven 100 so therefore this recursive call to sort return 7 100 and now we get
the next number which is 5 let's up
so I try to insert five into the sentence seven 100 this time we're lucky
five is smaller than seven so without even trying we know that 5 is smaller
than 100 because we know that Santa's in order so 7 is the smallest number in it
so we can just stick 5 in the front insert right away returns this and so
does sort and then we go to the next number which is 23 we're trying to
research this here this time we weren't so lucky so 23 is bigger than 5 so I'm
going to try to insert num into but first of stamp which is 7 123 is still
bigger than 7 so I'm going to try to insert 23 into the sentence with just
100 this time we are lucky insert sticks
two sentences 23 it's n to the 100 and then this next call up with 6 to 7 in
front of that and X call up stick to 5 in front of that as all the numbers we have so the recursive call to sort
returns this sorted sentence now we're all the way out to the beginning of the
original sentence so num is 6 we're trying to insert that into 5 7 23 106 is
bigger than 5 so we do a recursive call to insert 6 is smaller than 7 so we just
stick it in front and we stick the 5 in front and that's what sort return ok
it's pretty quick but I think the algorithm is not that bad questions yeah
okay good question the question is since sent is empty why do I have to do this
why don't I just return them and if the
overall input that I started with is more than one number that would in fact
work because sentence is very forgiving and you can do sentence with a word in a word not just a word yes
but if I did it your way and I said sort a sentence with only one number in it
you wouldn't return a sentence it would return just the number because that's
what insert would be that's not so good
because somebody else who's calling sort expects to have a sentence even if it's
a sentence of length one they're going to be you know but first thing down the sentence looking forward day so my
overarching answer to this question is domain and range always remember domain and range so in particular as we're
writing insert we say what is the range of insert there is to say what kind of
thing is insert supposed to return the answer is it's supposed to return a sentence so that's true even in the base
case we have to make sure we're returning a sentence and that's what this does okay so it's a much better way
to think to think about things then wait I could get away with shaving you know
one instruction off of the off of this program by having the base case not in
the range but something else instead don't think like that you'll get all messed up wait until they get to trees that you'll die if you think that like
think I'm supposed to return a sentence I'm going to return a sentence in every
one of these three cases so you'll notice that in fact every one of these three cases calls that precedes the
dr. procedure sentence to produce it result okay yeah yeah we didn't have any
there we just returned work so that's what number yeah here if we're talking
about this we've just checked and we've discovered that sent is empty so we know
what so we're just making a one word sentence if it said here if I put sent
right here where the cursor is before
this close paranthesis it would be okay I would then combine numb with an empty
sentence but it would Nell I know what happens when you combine one word with an empty sentence you get a one word
sentence so I'm just asking for that directly it
does create a sentence yo are you saying
does it clobber pointers to change something se is a function it doesn't
change any of its arguments okay functions that's an important point for
the you programs before in high school or something right yeah we're doing
functional programming never ever are we going to write something for the first month and a half of course that changes
the value of anything it's always going to be creating a new value okay that new
value might or might not share memory and if you're worried about space efficiencies you know the answer is it's
none of your business how it does it under the hood you just
worry about the value of what you get okay yeah
okay he wants me to insert values into an array in functional programming we do
not change the value of anything we don't set up some data structure and
then put things in we write a function that returns a value period okay you
have two people who program before in some other paradigm you really have to
try to sink in functional programming terms and not try to solve this problem the way we're taught in high school or
the way we were taught in Community College or the way you were taught in a seven okay don't think about what data
structure should I build we don't build data structures think about what is the value that this function is supposed to
return and you make an expression whose value is that value like this this is an
expression whose value is the thing that we want sort to return okay do that it
looked like that I'm not mad at but like
it's a good question everybody else wants to know that to everybody who went to high school at the same thought
memory but I'll do that so yeah does he he didn't go to high
school you're doing fun okay um all
right so subproblem what's the running time of insert well I see one two looks
empty three less than four first five
sentence sometimes we get five sometimes
it's five sentence six first
recursive call seven but first okay so
the time for insert sub-problem here is
either if the input sentence is empty
three or five if num is smaller or
or something in between the actual running time depends on how lucky we are
maybe it's just five altogether if none is smallest maybe it's seven plus five
if none is second smallest or fourteen plus 5 if none is third smallest the
worst it can be is 7 n plus 5 actually probably 7 n minus 1 so I mean that 7
times n minus 1 right no 7 7 n because n is the number of things in since not
including those so this is the worst
case so when we're trying to figure out
how long sorts takes what we're going to do is assume the worst case that's the
most conservative assumption we can also say on average the number we're trying
to insert is going to be halfway down right so we could say 7 n over 2 plus 5
average case so that's another way to
think about that to keep in the back ear mind but generally speaking it's easier
and more helpful to think about the worst case in estimating running time of
a program ok so given that how long this sort take well sort has one
two three four constant functions plus a
call to insert plus a recursive call so
there's n recursive calls right sorry so
the results for sort is going to be n times something plus a constant is 2
what's the something well it's for constant things plus the worst case for
insert all right
okay which is 7 n squared plus 9 n plus
2 everybody happy with this okay
somebody whose thumbs down after question yeah what's the two the two is
the if and the empty in the final base case of an empty sentence questions yeah
oh three um no most of the time that's
only he wants it to be 7 n plus 3 not 7 n plus plus most of the time almost all
the time the new number that we're inserting is going to be somewhere other than the very end so when we get to a
number bigger than it we're going to do five steps that's the second case of the
cond which is also a base case there's no recursive call on the second on closer than search does that answer your
question yes the very worst case you write would
be that but if you think about the big sentence that we're trying to sort we're
only going to get to that worst case like once unless we're so unlucky that we get the numbers in inverse order
backwards order or something okay yeah
ah yes good question you get a gold star
he wants to know this makes up for you wanting to put things in a race he wants
to know isn't it the case that each call to insert has a different size scent
right it's not that we're going to make any calls to insert and each of those
calls to insert has a sentence of length in to work with we're going to make an
insert into an empty sentence and then insert it into it and a one number
sentence and then insert it until it's to number sentence up to insert it into an N minus 1 number sentence so really
this should be 7 n over 2 and this should be 7 n squared over 2 but right because on average we're
inserting into a sentence of length n over 2 okay now I said we're only doing
one week of this and 61b you'll get a much better treatment to this whole topic I am hand-waving a lot
by saying okay 7 n over 2 it's the right answer but I have not proved that it's
the right answer ok next semester you'll actually do that but yeah it's actually
7 it's great over 2 plus 9 n plus 2 is the right answer doubt longest time okay
now that you know it's 7 n squared over 2 instead of 7 N squared do you feel edified you have a better understanding
of this program I don't because this
division by 2 is the kind of change in
running time that is going to be obsoleted the next time you buy a new
computer right next year's computer is going to run twice as fast that would
also make it dividing the time by 2 so
constant factor in running time are just not very
interesting here's what's interesting about running time if I want to take
squares of the thousand numbers it's
going to take some amount of time okay whatever it is if I want to take squares
of two thousand numbers it's going to take twice as long right everybody happy
with that because it's proportional to n basically if we have if we have three numbers that plus two at the end matters
but once we have a thousand numbers that plus two at the end is totally down in the noise basically you double the
length of the input you double the amount of time it takes the behavior of
sort is very different if it takes a certain amount of time to sort a
thousand numbers how long how much more
time will it take to sort two thousand numbers I'll take four times as long
right because there's an N squared in there and the square root of two
thousand is four times the square of 1,000 not just two times right now
there's also a linear term it's something n squared plus something times in but once we're up in the thousands
that doesn't matter right the difference between four million and four million
two thousand is nothing right I tell you
the running time your program you want to know question should I go out for dinner while I'm waiting for this result
or is this result going to be computed in my lifetime right that's the kind of
question you want to know not can I get down to one percent one tenth of one percent and knowing exactly how fast
it's going to be that one tenth of one percent be swallowed up by things like all those
other programs running on the computer swapping you in and out of memory and that will affect the running time too
okay so really what we want to know about these programs is that squares
takes linear time double the input double the output mm sorry double e
input double the running time sort takes quadratic time double e input quadruple
the running time okay and that's way way more important than the constant factors
because next year all the constant
factors will be cut in half and so the
running time of the program will be cut now but that's not going to change the fact that doubling the size the input
quadruple the amount of time that it takes okay so that's really what we need
to know about the algorithm and we need a way of talking about algorithms that captures that essential point okay the
difference between linear and quadratic there is a notation for that and I'm
sorry there's some math up on the board if you're a math hater this is as bad as
it gets okay never going to do anything like this again next semester maybe I'm defining a
notation called big theta but in order to find it I first have to define a notation called Big O you will see in a
lot of books and papers something like
the running time as a function of something or other equals of x squared
but that's wrong that notation is run this equality sign
T of X is not equal to whatever this thing is because this thing is not a function it's actually a set of
functions so what it should say and what the careful papers do say is T of X is
an element of of x-squared okay if
you're really really careful it will say G of X
nobody is this careful but they should be X maps to x squared that's what they
should say because what goes in the parentheses after the O is a function
not a number so this way it makes it really look like a function okay so what
does it mean here does all these horrible symbols which I am going to
deconstruct for you it says there exist
numbers N and K by the way N and K are both greater than zero I forgot to put
that in such that one of the horrible
things about mathematical notation is that if you see two vertical bars that means absolute value but sometimes you
just see one vertical bar that means such that it's easy to get confused but
try not to for all X greater than n what's that about well
axis x and f of X whatever this is what
a linear function looks like right you double the input you're double the
output it's linear here's what a quadratic function looks like okay once
you pass this point the quadratic function is always bigger but prior to
this point the linear one is bigger for a little while right good this says I
don't care about small values of X why
don't I care about small values of X here's why if I have a thousand numbers
to sort given how fast computers are these days the speed of the computer
sorting the numbers is going to be limited by the speed at which I can type them in realistically speaking you know
we can figure out exactly how many nanoseconds it's going to take to do that sort but it's going to be less than
a billion of them which is to say it's going to be less than one second if it's
less than one second it doesn't really matter if it's less than half a second or not right it's fast enough it's when
we have a billion numbers to sort and that takes a thousand million billion
trillion quadrillion that takes a quintillion operations alright that's a
billion squared right I get that right I think so yeah
quintillion that's a big number all right that's more than a second that's
when we have to worry about efficiency so if for small values of the input size
the wrong function is bigger who cares what we care about is large inputs not
small inputs when we're talking about efficiency so that's why there's this capital in this is the biggest value for
which the wrong function is on top okay and this notation says who cares because
for almost every imaginable problem that cut over point is small enough that
we're not talking about a significant amount of time we're not talking about hours of runtime or days at runtime
we're talking about seconds so um just a minute oh yeah in this class the
question was this efficiency played a great role in grading project no I think
for most of the projects in this class you'll have to work hard to make a
program that's inefficient by this standard that I'm talking about I in a different order of magnitude if you
actually did manage to do that we might take off a little bit but it's not we don't want you to worry about efficiency
I'm doing a project ok the next thing to
worry about is these absolute value signs these are here to make the mathematicians happy if a function goes
negative it's the how far away from zero is it the dot that we're talking about
in terms of what family of functions is again luckily if you're a computer
scientist you can just read this as if the absolute value signs weren't there why because these functions that we're
talking about are amounts of time and no
matter how hard you try you're not going to write a program that solves a problem in negative
time okay so for our purposes F and G are always both positive and you can
forget about the absolute value what about K this is the part that says
constant factors don't matter so 7n
squared for our purposes is the same thing as 7 n squared over 2 because that
factor of 2 is always a factor of exactly 2 no matter how big or small n
is right so doubling the size the input
it's still going to be quadruple the running time not only half the running time because that over 2 right
so constant factors if your constant factor is bad and running your program
and you're trying to optimize your program to get rid of a constant factor the way to do it is stall for a year get
a new computer constant factor is gone
what we care about is this or domination by more than a constant factor of one
function by nutty so this K says the
function f is less than or equal to some constant times the function G ok so 3x
squared 4x squared a thousand x squared a thousand x squared plus twenty million
X is still quadratic time that front that x factor really began which is what
we care about is down in the noise it's the height for polynomial function it
says that it's the highest power of n X whatever your variable is that counts
okay which do I do I don't have time to
do both I'll tell you next time about the families of functions but what I want to show you right now
John Bentley who wrote not the greatest our textbook is the greatest but one of
the greatest computer science books ever called programming pearls which I definitely recommend we're in 61 D they
don't require it decided to do a demonstration of this thing that I just said and it's the order of magnitude
that the the exponent of the function again that matters rather than the
constant factor so it Bentley did was he took the cray-1 which was at that time the very fastest computer in the world
you know they were like five of them or something in the whole world and they were used by the NSA to crack codes and
by the weather bureau to compute the weather and stuff like that and he wrote
a function to solve some problem that did it inefficiently in time
proportional to N cubed but with a small constant factor this is measured in some
amount of running time and then he took his Radio Shack trs-80 little 8-bit
microcomputer terrible slow clunky he wrote a program in interpreted basic
versus highly optimized compiled Fortran so it had a huge constant factor
nineteen and a half million but proportional to n rather than n cubed so
here are the different values of N and here's how long things took and for
small values of n the supercomputer with the small constant factor 1 3
microseconds versus 200 milliseconds so that's a factor of 10,000 better three
milliseconds versus two seconds or still a thousand of the factor better but
eventually it crosses over at N equals 10,000 this supercomputer with the super
fast compiled program and the tiny constant factor takes almost an hour against three minutes for
this little dinky micro with a huge constant factor but proportional to n because the difference between 10,000
and 10,000 cubed swamps even this constant factor of 19 million um the
last ones he didn't actually run it on the Cray because you couldn't actually have a super computer to yourself for a
month but it would have taken a month for something that took half an hour
with the linear algorithm it would have taken a century for N equals a million
versus five hours now five hours is a long time to wait for a result but it
sure beats a century okay see you Friday