Transcript


okay um thank you those of you who are here for braving both the rain and the
iodine um the rain actually is good because it keeps you all indoors where
you don't get radiation poisoned um okay so today we're talking
about a topic that's not in the book uh and the reason we're doing it is that the 61b instructors want you to have
seen it before or you do 61b um and what we're looking at this is
kind of the big picture here we have the abstract notion of a sequence first
element second element third element and so on and two different ways to implement it the way we've been talking
about up to now is the list where we link pairs together by their cters and
have the cars point to the elements um and this new way is called a vector in other langu is it's often
called an array and it's a bunch of locations in memory that are right next
to each other so there's no link there's no cter linkage it's like a just a bunch of cars in a way in a big
block um abstractly they behave exactly the
same way abstractly they're both sequences and you can do everything that
you can do to a sequence with either one um
different things turn out faster depending on which one you
use um so let me talk about the similarities and differences um well no
let me not let me um start by showing you a little bit about how vectors
work so I'm going to say Define
V1 to be make Vector
4 and here's the value of V1 um the first thing to notice is this
number sign right at the front um so number sign and then stuff
in parentheses means this is a vector so it's the notation is parenthesis element
element element element close parenthesis just like a list the only difference is that number sign at the
beginning um the standard does not say what the
initial value of those elements are in STK we have this funny thing called number sign Unbound meaning we haven't
given this element a value yet um I could also have said if I want
Define V2 to be make vector
for um I don't know the empty list and then
V2 would be a vector containing four empty lists so let me back this up so you can
see both kinds so make Vector takes an optional second argument which is the
value to put in all the elements um if you pick a non-empty list as the initial
value which would be unusual uh you should bear in mind that all of these elements are going to start out
EQ not just equal because we take the very same thing and stick it into every
slot so with lists um you don't say ahead of time how
big the list is going to be right you can just cons things onto the list
forever um with vectors you do say right at the outset I want a vector of this
size and that's how it's going to be forever uh and that's a consequence of
this picture um the scheme system has to allocate a chunk of memory that's a
particular size and there might be something else right next to that block of memory so it
can't just grow and Shrink um so that's a very important difference vectors are really good in
situations where uh you do know ahead of time how many elements so the ex example like uh X Y and Z coordinates for a
point in three space you know and it's always going to be exactly three elements
um okay now that I have this Vector what can I do with it well I can say Vector
ref V1 uh two let's
say that's Unbound and if I set it for v2 I would get the empty list um the in
scheme the elements of a vector are numbered from zero so these vectors have
elements number zero through three and there is no element number four
um so if you want to know the position of the last element it's the length minus
one um and I can say Vector set
bang V1 to quote Fu now if we look at V1 we'll
see that element number two which is the third element has the value Fu
okay um very commonly what you have is a a vector of numbers and you give uh them
the initial value zero and then you you're counting something or other and you add one to each one is that a hand
up no okay um
okay so um the main Constructor for
vectors is uh make Vector which is very different from
anything for a list there's no make list of size n what there is however is there's the
procedure
list and there's similarly a procedure Vector as opposed to make Vector that
takes any number of arguments and Returns the vector of
those elements so that's something that is kind of the same as how lists work but
these are derived procedures I in chapter two you learned how to write list using cons and the same thing is
true here this Vector procedure is implemented using make Vector yeah
can you quote a vector yes you can say quote number
sign and then whatever
okay um just as for lists you're not supposed to do that if you're going to
mutate it which you always are for vectors
right Vector programs it's very rare to see a constant Vector that sits around
forever um okay so Vector ref which we've
already seen works just like list ref um the difference is the list ref is
um not one of the central selectors for lists it's implemented using car and
cutter whereas Vector ref is uh basically the only selector for vectors
it's the Primitive selector um for vectors and lists we can ask how long they are U
length is for lists implemented by cing down uh vectors just know how long they
are each Vector has like a header that contains that information
um and then here are the things that are different there's nothing like K car and
cter um there's nothing like make Vector there's nothing quite like setar
and set cutter but there is the mutator vector set bang which is different in that it takes not only a vector but a
number which says which element do I want to change in the vector okay questions so
far okay um up at the top of the
screen uh let's make this a little smaller there we go up at the top of the
screen is map for lists you've seen that a million times before so I'm not going to go through it but it's just there for
contrast with Vector map uh implemented below it so Vector map takes a function
and a vector and it returns a new Vector in which we've applied the function to
each element of the original Vector so um
unlike regular map Vector map has a helper function um and then here's the call to
that helper so this is the actual body of vector map and before we get into the
loop procedure the very first thing we do is make a new Vector in its entirety
whose length is equal to the length of the argument vector okay if we were trying to do Vector
filter it would be a lot more complicated because we don't know ahead
of time how many elements would satisfy the predicate so we wouldn't know how big to make it in advance but for map we
know that the result Vector has the same length as the input Vector so here we are making this vector and in the loop
procedure it's going to be called new VEC that's a formal parameter and the other argument that
we're giving it is um Vector length of x minus
one um which is the index the element number that's called an index of the
rightmost element um I wrote this procedure going right to left through the vector you could just as well do it
left to right um I find this a little bit easier because the end test going
right to left is is n equal to zero rather than the longer n equal to Vector
length of V minus one
um wait oh less than n zero sorry it would have to be greater than Vector
length minus one or equal to Vector length it's less than n0 because zero is a perfectly good element number it's
only when we get down to n equals neg1 that we're finished so if n is negative
we're finished just return new VC new VC started out having Unbound as all of its
elements but you'll see that by the time we get to the base case we've filled up each slot with the new
value um so if N is a valid index number then we do this um I think you've seen
begin before in other contexts it has any number of it's a special form
it takes any number of Expressions evaluates them left to right or top to
bottom in this case and Returns the value of the last one um so in this case there's two
expressions first one is Vector set bang new VC element number n to fun of vector
F the original Vector n so we take element number n call fun on it and put
it into the same slot in the new vector and then we call Loop recursively
this is a tail call by the way so this is an iterative process with new VC being the same Vector it's not cter of
new VC the way it would be for a list um but the new index is n minus one so we
work down to zero which is the leftmost element then negative one and that's when we return new V is that a hand up
yeah why did I make a new Vector instead of just using VC um
because I like functional programming and um even though we're
dealing with vectors I still would rather leave my old one intact just in because I'm this is a
very general procedure right that you put in a toolkit um maybe whoever calls
Vector map is finished with the original values after the call to Vector map but maybe not so I would rather leave the
user with that choice by returning a new vector okay um you can write and people do
write Vector map bang Vector map bang that does what you're saying just
replace the values in the original vector and that exists also okay other
questions cool who's programmed with arrays before someh have some haven't okay so
this is worth doing um okay
that's Vector map um
okay why would we want to use vectors versus lists or lists versus
vectors and the issue has to do with certain things are fast with list and
other things are fast with vectors it's just efficiency like mutation altogether is just about
efficiency um so there's a chart over there on the third board um the place where vectors
definitely win is if we want to look at the 100th
element for a list we have to do 100 Cutters or 99 cters whatever no 100
cters because we number from zero have to 100 cters and then a car so it takes
Theta of n time to find the nth element for a vector because they're all right
next to each other and these pointers that we represent as
arrows in the diagram each pointer is the same size given that we know where the
starting point is of this Vector we can calculate where the hundredth element is
so that's just a piece of arithmetic start with the starting position of the vector and add 100 times
however long a point there is and there's the H 100th element or there's a that's the location of the 100th element
and we can just look at that so finding the nth element of a vector is Theta of one time not Theta of end
time that's important if you're writing a program that sort of jumps around a
lot you know first we look at the 100th element then we look at the 35th element then we look at the second element then
we look at the 200th element and so on um where lists win is if we don't know
the length ahead of time and so we're going to write a program that builds up a list element by element it builds up a
sequence element by element that's easy to do and fast to do with lists and very
hard and slow to do with vectors um so for a vector if you have a
vector of length five and you now want to add a Sixth Element you have to
create a brand new Vector of length six you can't say make my Vector bigger you have to make a new vector of length six
and copy over each of the five elements b boom b boom b boom b boom b boom and
then add the new one in the new position so adding a new element to a vector
takes time Theta of n because
um you have to copy all the old elements whereas adding an element to a list
takes time Theta of one you say cons it makes one new pair and that takes constant time I'm saying that with my
fingers crossed it takes constant time unless you run out of memory and the system has to do a garbage
collection but it still takes constant time almost all the
time another thing I'd like to point out is that the most common thing to do with
a sequence neither one is more efficient and that is look at the first element
look at the second element look at the third element the way we did with map and Vector map both of those take time
Theta of n it's only if you're jumping around in
the sequence that vectors win if you're going from left to right through the sequence which is the more usual thing
then vectors and lists are equally good so a lot of people are confused about that um and think that vectors are just
always better at finding things but it's only finding things where you jump around so
um my favorite example about this is writing a program that plays some kind
of card game solitire or 21 like the project or
something um the first thing you have to do is make a deck of cards and Shuffle
It shuffling a deck of cards is a great example of something that's best done
with a vector because the way way you shuffle a deck is you pick a random number less
than 52 and you interchange that element with element number zero then you pick
another random number less than well all right let's exchange it with element number 51 that makes it easier now take
a random number less than 51 and interchange that element with element 51
so because we're picking a random number each time we're jumping around in the deck that's it means to shuffle you want
you want it to come out random and so vectors are really good at that now we
finished shuffling we have this deck um and let's say we're playing Solitaire
how do you play solitire with a deck of cards here's the deck of cards in probably your left hand but I'm
left-handed so it's in my right hand and you go vom ch right schung schung schung one card
at a time moves from your hand to a pile one of the seven piles
right that's much easier to do with lists because the card that I'm moving
is car of the deck what's left in my hand is cter of the
deck and the new pile after I've put that card down is K's carve the hand
onto the old pile okay so writing a program to deal out the cards is much easier with a
list so much so that when I write such programs I actually convert between list
form and Vector form I shuffle the deck as a vector and then I
call something I didn't write on the
board Vector to
list of V this is a minus sign followed by a greater than it's supposed to look
like an arrow and it's pronounced two as in Vector to list and there's also
list to Vector L that does the obvious
thing okay um don't fall in love with those
conversion procedures in particular and the next midterm when we say write a
vector program that does such and such don't say Vector to list and then baah blah
blah blah blah and then list to Vector zero points it will say that on the exam
um but for situations like you know that're special like this G deck of cards thing um it really is useful once
in a while to be able to convert what's the order of growth of the conversion how much time does it take
yeah it's Theta of n both ways because you have to visit every
element it's like the last row of my table there you have to visit every element in order to do
it um list to Vector you have to start by finding out
how long the list is so you're going to probably end up traversing the list
twice whereas Vector to list you know how big the vector is and it doesn't matter anyway because you're going to
cons one element at a time when you write Vector to list are
you going to go through the vector left to right or right to
left and why
yeah yes thank you the only right way to do it is right to left because for each
element you're going to say cons this element onto the list I already have and so the one that you cons on last in time
is going to end up being the first element of the list so you should start with the last element of the vector and
work your way down to the first element of the vector okay good um
I'm always terrified to show this to people because some people think it's meant to
be a good idea um this is something you shouldn't do I'm just showing you that
it's possible and why it is that it's slow so this is Vector cons nobody would write a vector program
this way if you find yourself wanting to use Vector cons you should have been using
lists in the first place um well or you're not thinking about your
vector program properly so what I want to do is I have a vector and I want to stick a new value
in front so I'm going to start all Vector programs basically have this
structure with a little inner loop I'm going to start by making a vector that's
one bigger than the vector I was given okay and I'm going to start with an
index that's Vector length of VC not Vector length of VC minus one the way it
was last time but Vector length of VC because that's the rightmost element of the new Vector the new Vector has length
Vector length of V plus one so its rightmost element is Vector length of VC
um so here's Loop new VC n um and we start out this time the base
case is n equals z we'll see why in a moment but let's start with n being big and we're going to do this begin here
Vector set bang new VC n so put into the new vector vector ref VC n minus
one so let's say we have a vector of length five and now it's going to be a vector of length six so we're saying
Vector set new VC five Vector fve Four Element four of the
old vect becomes element five of the new one and so on down then we loop with n minus one finally when we get to zero
we're not copying from the old Vector anymore we're going to Vector set new VC zero to
be this new value here the thing that we're trying to cons in front so that's what we stick into slot
zero and then there's no recursive call this is the base case and we just return new V right so how long does it take to
do Vector cons Theta of n because we're going through the whole vector copying
things over um so again don't do this this is just to show you why you wouldn't want
to is that a hand up no everybody's sort of doing this
today maybe it's a symptom of radioactive iodine poisoning
um
okay so I talked about shuffling
um I have a few different Shuffle procedures and lecture notes um so the
first one is here's how we would do it just with lists
functionally um so I want I have a list and I want to shuffle it get it in random order I'm going to say here's the
body of the procedure after that inner definition of loop says if the list is
empty then return the empty list there's nothing to shuffle there's only one
ordering for an empty list otherwise we call Loop list old list empty list we're going to
build up a new list on top of that and a random number less than the length of
the list okay
um and then there's this Loop which does something awfully complicated
um let's say n is not equal to zero
so uh we have a list of length 100 and our random number was
five so we call Loop cter of in so one fewer element in
N I'm sorry no that's if n equals zero so if n is no it's not if n is not equal
to
zero wait is this backwards wow is this program been wrong
all these years or am I losing my mind let's see if it works
yeah it works so it must be right okay so if n is not
zero we remove the top card from the
deck um we add that top card to
out oh I see out isn't really out at all
that that's what's confusing me it's very complicated progr I should rewrite this um out is a sort of holding tank
where because we picked a random number we picked five so I want to get down to card number five so what I'm going to do
is take the first five cards of the deck and put them in a separate pile which is called out so I use cter
to remove the card from in and I cons that new that card onto out and I make a
recursive call I keep doing that transferring cards from in to out until I've
transferred n cards so the N plus first card is element number n because we
count from zero um and so now I have car n being the element I want so what I'm
going to return is cons car in onto a recursive
call to shuffle a pending could or in without so the transfer from in to out
sort of has no particular meaning because once I found that card I was looking for I'm going to SM smush the
two together and they're not in any particular order anyway they're the ones that haven't been shuffled yet and now
I'm going to call Shuffle one not Loop notice that this that's the important point that I missed first time around
this call is not a call to loop it's a called to shuffle one so we
take every card except the one I just picked shuffle them randomly and then
stick this card that I picked randomly at the front so that's the shuffle algorithm how long does it
take
why yeah moving some element to the front takes that element's index number
of operations okay the index on average is
half of the size of the list um so n /2
which is Theta of n operations to find that card and then we have a recursive
call to shuffle for all the rest of the cards so it's order of n for each card
and there's n cards so it's order of N squared time to do this Shuffle so
that's pretty bad um I'm not even going to look at this
Shuffle Tu bang is just to show you that even with list mutation it still ends up
taking n squar time so you can read that on your own I don't like it even though
I wrote it and we'll move right along to shuffle three so now we have is a vector that we
want to shuffle so we call Loop Vector length of v um which is
one more than uh the rightmost element number so what does loop do um if n
equals zero never mind that yet otherwise let index be random n and this
is why we used Vector length and not Vector length minus one because random n
returns a number between zero and N minus one which is just what we mean what we need to get a random index in
the list um so index is the random
number temp is the rightmost element of the vector so I
pull out the rightmost element of the vector we're going to do a swap that's why I'm doing this pulling out into temp
I think when we talked about set bang we might have gone through this that if you're trying to exchange two things you
can't just say set the first one to the second one set the second one to the first one because if you set the first
one to the second one you've lost the old value of the first one and now you're going to have two the same thing
so you have to say save the first one in temp move the second one to the first one and then move temp to the second one
and that's what we're doing here temp is the the value that's at the right end of
the vector index is a number between zero and one minus the length of the
vector now I can say set the that last element the one I
pulled out into temp change its value to Vector ref VC index index is the random
number so pick a random element stick it in the end um and then Vector set
bang uh V index which is that random position to Temp which is the old value
from the end of the list end of the vector so I've swapped two elements of the vector
how long did that swap take Theta
what constant time Theta 1 that's the advantage of vectors I can
go to a random element in constant time um the whole thing is going to take
the shuffle is going to take Theta n because we have to do this Loop n times
because right down here we say Loop n minus one so the entire Shuffle takes Theta n whereas for the list it took
Theta n^ s that's a big difference how much is 50 squared 52 squared once say
50 squared it's easier 2,500 right so the difference between 50
and 2500 is worth thinking about
um okay uh if n equals zero we're finished just return VC that's
easy what if the random number that you pick is n minus one so we're
interchanging the last element with itself that's fine no problem we and
it's the same thing all all of these Vector sets are setting the same value into different
places um not a problem so that's how we shuffle a
vector questions
could you write this program on a closed book exam not that we're going to ask it but
suppose we did there's there's two parts to being
able to write this program one of them is understanding how Vector programming
style Works in general and pretty much without
exception it's
the body of your procedure is a called a loop with um an index and maybe a new Vector
that you make in this case it's Shuffle bang we're shuffling into the same
Vector if I wanted to do a shuffle that made a new Vector I could do that make a
copy of the vector then I wouldn't even need this temp thing I could just put things down in random places in the OR
well put random things in place boom boom boom in the new Vector
yeah no random n returns a number from zero to n minus
one yeah
okay ah how is random written in scheme um well the scheme standard does
not have random in it at all I believe although the next one will um so I can't give you a definitive
answer to that question um so here's a little potted five minute lecture on
random numbers um there are two ways to get random numbers one of them is truly
random numbers which means that the value is somehow determined by Quantum
effects um now seriously and the other is what's called pseudo random numbers
which is what almost everyone does so the way you get a truly random number um for those of you who are
electrical engineers you will remind me that the voltage drop across a
diode is 1 point something
volts is that right who's an electrical
engineer okay all the electrical engineers are too wimpy to Brave the rain or maybe they really know about
radioactive iodine and we don't um anyway the voltage drop across diodes is
always the same amount plus or minus a teeny bit so for
purposes of this discussion I'm going to pretend that I know that it's 1.4 volts
so the real answer is somewhere between 1399 and
[Music] 1.41 okay so you take a diode you get a
very good voltmeter you measure the drop across that diode right now you subtract
1.4 and that gives you a random number okay so that's how you make
really random numbers um the way you make pseudo random numbers works
by things about the properties of integers so you take a course on number Theory which is the mathematical study
of the integers and you learn about um
algorithms that spread out values pretty well and what you do is something like
this you start with uh what's called a seed an initial
value you get that not by always picking the same value that would be bad because then
you'd always get the same sequence of random numbers instead you take the time of day in
milliseconds and add to that um the angle of at which your disc is
spinning right now how far along a rotation is it and that kind of thing that is sort of more or less random and
you mix all those things together and you get an initial seed that's your first random number now by the way
random takes an argument in so what you do is you take your random number divide by n and you return the remainder that's
how you get random number in a particular range now what you do is something like and
this is not the best possible algorithm but it's an okay algorithm you multiply your random number by
itself um as you remember from elementary school when you multiply two four-digit numbers you get an
eight-digit result right you take the middle digits of the
answer so in computer binary terms you have a 32bit value you multiply it by
itself you get a 64bit value you drop the first 16 and the last 16 you like
the middle 32 and that's your next number okay the AL the re algorithms they really use are more complicated
than that but that's a simple example
um that particular kind of random operation although it's very very
standard in computers that that's how they do it it's not very good um
I remember really having my eyes open about this uh when I happened somehow to
web surf to uh an online gambling
site um that was advertising the quality of their deck
shuffling of their random numbers um and they pointed out that the number of ways
in which you can order 52 cards is greater than 2 to the 32nd
power so if you take the usual computer 32-bit random numbers and you use that
to shuffle a deck of cards as in this procedure um you don't get every possible deck shuffling you only get a
few of them and clever adversaries can figure out
how your random number system works and which deck shufflings you're going to get and after the first few cards come
out can predict what the rest of the cards are going to be um so if you want
a good fair game of cards um you need a better random number generator namely
one that generates wider random number so there's there are standards in the world for how to get you know a 100 bit
wide random number and so on um and there are pain in the
neck um does that answer your question okay good all right back to vectors
um okay so uh in order to write this program that was where I was what I was
talking about there's two things you have to understand one is the general characteristics of all Vector programs which is there's going to be a loop that
counts the index either up from zero or down from length minus one or something
and um maybe there's a new vector or maybe you're modifying the original
vector and then in your Loop there's going to be um Vector ref things like
this Vector ref V index and things like this Vector set ve
index something or other okay and that's what's going to happen each time through the loop so every Vector program that
you write should look like that now in order to write a shuffle
program uh you have to know a good algorithm for shuffling a
deck um it's not obvious how to do that uh a
lot of sort of first try algorithms for shuffling decks
um certain outcomes are more likely than others so like you know cards near the
front tend to stay in the front or or vice versa um this is the correct algorithm
how do you know it's the correct algorithm because at home you have the as of like a week ago four volume series
The Art of computer science by Don K um and you look up in I think it's
volume two shuffling and you look at the algorithm
and he tells you what it is and then you code it that's how
um you don't get to bring can with you to the exam however
um so I wouldn't ask a question quite this hard not that this is hard hard hard but
it's a little bit tricky to to get a good Fair shuffling
algorithm okay
um oh yeah so just a brief comment on how this
all works in the computer there's this memory which is a huge bunch of um what's
called addresses uh the word address is a metaphor for you know your street the
street you live on has you know Number One Main Street and number two main
street and number three main street and number four main street and so on so each house has an address and the
addresses are at least in principle consecutive numbers although sometimes they're not for various reasons um but
in a computer they are consecutive numbers and um the computer hardware
lets you say tell me what's in memory address such and such software uses that capability to
build a storage allocator this is one of the things you're going to learn how to do in
61b is write a a procedure that you call it with a number that's how big a block
of memory you want and it Returns the pointer to a block of memory that's available for your use that's that
size um memory management is a little bit tricky because what happens after a
while
um is here's memory and somebody asks for a block
this size and then somebody else asks for a block that size and then somebody else
asks for a block this size and now this guy in the middle says okay I'm done using this block so return that to the
memory that's available for anyone to use and then a little bit
later someone comes along and asks for a block of this
size and it gets allocated Here and Now what you have is this tiny little sliver of useless
memory right um so uh that's what makes memory
allocation complicated and one of the nice things about
lists as an implementation of sequences is that all pairs are the same size right they all have two pointers exactly
and when everything's the same size you don't have this what's called fragmentation of
memory um so that's a nice feature of pairs um vectors however the reason you have
to say how big it is is that we're going to allocate a chunk of memory all at once to hold it once you have that thing
if you want element number 100 this is just simple arithmetic so this block
here is at memory location a th000 a pointer is is four bytes long
typical I want element number 100 I take that number 100 I multiply it
by four which is the size of a pointer I get 400 I add that to a th then I get
memory location 1,400 I said give me the pointer at address 1,400 and there it is
so that's why um finding the nth element is constant time for vectors whereas
with lists the pairs can be all over the place place in memory because people are constantly allocating and deallocating
pairs um and you never know where they're going to end up so you have to go cter cter cter cter 100 times to find
the N element all right um I'm not going to ask you questions
about what I just said about how memory works that's 61b material I just you know want you to if you're interested
have a clue about it one last question Everybody's scared to ask the
last question it's like the last cookie
yeah okay why not round up the size to a power of two you can do that that's one of the ways of doing memory allocation
to avoid fragmentation yes um that is a way um it turns out even better from a
fragmentation standpoint but more complicated to implement you can look it up in K is um rounding up to the next
higher Fibonacci number it's really weird um it's very
strange algorithm anyway yes so there are ways to improve the fragmentation problem and you'll learn all about him
in 61b okay see you next week if you haven't died of I9 poisoning
UC Berkeley