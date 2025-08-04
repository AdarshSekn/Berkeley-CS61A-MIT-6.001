Transcript


at four o'clock this afternoon is the undergraduate town hall meeting for CS
and EE CS and wannabe CS undergraduates to meet with faculty and administration
of the department and discuss whatever concerns you have the four o'clock it's
I'm pretty sure an HP auditorium I better know before the time comes because I'm going to be at it so I'm one
of the people you can ask questions up and that means that my office hours
which usually run until 5:00 we'll end it for today so sorry but come to that
instead okay so the big topic that's
going to take up most of our time today is where did they put my school no
that's not the big topic oh there we go that's a little topic the big topic is
how tables work so what a table is an
association between keys and values and you've seen different kinds of tables by
now you've seen a two-dimensional table back when we did data directed
programming and in the current programming project you're seeing
one-dimensional tables but more than one of them you can create a table as needed so we're going to talk about those
different variants and all the different ways of doing things the code on the screen here is for the simplest possible
version where there's only one table and it's one-dimensional because I like to start simple and work up so the first
thing is to talk about Association lists which are up on the top board there an
association list is a list whose elements are key value pairs a key value
pair is a pair whose car is a key this could or is a value so that's a pretty
simple definition it's a very useful idea to have in many
many situations so much so that scheme
comes with procedures that know how to deal with Association well one procedure
anyway that knows about Association lists and that's a sock key in
association list which returns a key
value pair or false so if the thing
you're looking for is in the association list it doesn't return the value the way
our table structure does he returns a key value pair and we'll see in just a
moment that that's useful for allowing modifications to the table it's also
useful if you need to be able to distinguish a key that's associated with
the value false from a key that isn't in the table at all because a sock if it
does find a match in the table always returns a pair so in one case you get
back a pair whose could or is false that's if the value in the table is false or you get just plain false
meaning that the key was not found in the Association list let's go ahead and make an association list define a list
to be list no no no done rhythm all base
well now I should make it john dot rhythm
all doc bass George dot lead and Ringo
dot drums okay here's my association
list and now I can say a sock pull let's
quote Paul a list and I get back not the
word bass but the key value pair whose car is the key I was looking for his cutter is anything so if I say a sock
[Music] mint a list I get back nothing because
he's in the wrong group okay questions about Association list good this
association lists are a really really really ancient list data structure there have been a list since the very
beginning in 1962 with Lisp and they've survived again because they're really
useful now for making a table the obvious thing to do is just use an
association list as the table that's not what we do instead we have this yellow
pair which is a header it's you can it sort of serves two purposes you can view
it as attaching a type tag right so this is a thing of type table to the
Association list but it's more important than that it serves as what we call a
sentinel or sometimes a dummy node those are
names for this pair because um the
reason for Sentinel is you put them at the front and maybe at the end of the
list or an array it's a very common technique even in those other ways of doing things to serve as end points
pseudo elements of the structure and this often saves you writing special
case checks for running off the end so sometimes for example you'll see
algorithms for searching sorted elements in an array and what they do is they put
the value minus infinity at the front and they put the value infinity at the end and so you're always guaranteed that
anything you're looking for is within the limits of this array even though
those aren't really part of your data and we're going to do sort of the same thing we're using this as a sentinel not
because its value is less than anything else let's bet the different use here it's
for two things one is it makes an empty table not be a special case so when
we're talking about looking things up in the table or inserting things into the table you'll see in a moment that we
don't have to have any null question mark checks to handle an empty table
differently from any other kind of table and the other thing that's important about it is it allows us to maintain the
EQ nests of the table even if all its
elements are gone or it doesn't have any elements in the table
so imagine if you will that there are four different variables that are local
two different procedures in your program that all happened to point to the same
table and let's say now that we want to
cons a new pair at the front of the Association list because that's how you
add an element well we did that for one of the variables and we could say set
bang this variable to cons new element the old value of the variable but those
other variables that pointed to the same table don't anymore because the
frontmost pair of the association list isn't what it used to be having this
sentinel node avoids that problem because any variable that points to the table points to this pair and each table
that we make will have a different one and it's always going to stay the same so you can rely on any set of variables
that point to it continuing to point to it no matter what happens in the program is that guess might be sound a little
abstract until we actually look at the code so let's go ahead and do that in this program I defined a table this way
and you'll notice that I did not say quote open parenthesis to our table star
close parenthesis because we're going to mutate this table and you're not allowed
to mutate quoted lists you can quote the elements of the list you have to to get a symbol in there but the list itself
has to be generated by your program by calling cons or something that uses cons
like list or append or whatever okay so
back at the ranch the current value of the table is a list of one element star
table star okay if we want to extend this program for
multiple tables then instead of having a variables a table we'll have a procedure
called make table that generates a list and that has just the element 1 element
start table stock books but I wanted to
make these procedures really easy so there's no argument for which table to use in these procedures so how do we
look up the key in the table well the first thing we do is we a sock the key
in could err of the table so could or the table is an association list to
begin with it's an empty Association list but that's perfectly okay we don't
have to say null question mark because a sock is perfectly happy to be given an empty list in which case it will return
what false not the empty list okay so we
say everybody always asks why do I have this not here why don't I just have the clauses backwards no a special reason I
just sort of think of not finding it as a kind of base case so I wanted to come
first in my code but you could do it in the other order that'd be fine and just say if record so if we didn't
find it here's where we return false so a sock
returns false we return false also if we did find it we don't want to return the
key value pair we just want to return the record so the trade-off is the user
of get doesn't have to know how the table is implemented doesn't have to
know that there are key value pairs involved but we can no longer
distinguish between a value of false on the table and no value at all that turns
out to be just what we want in the adventure game project and it's not so unusual the value of false means that
there is no value and you can set something to false to make it have no value effectively so that's why this says
cooter record the thing that it's taking cooter of is a key value pair and the coder of that is a value this notion of
key value pairs by the way we're going to come back to it when we look at Map Reduce because that relies heavily also
on key value pairs okay so a little more interesting is putting a value in the
table and we do it also starting with a
sock we want to look up the key in the table and the reason is if we do two
puts for the same key we don't want to waste memory by having the same key
appear in the Association list twice the LIA sock works it starts at the beginning and Cooter's it's way down so
as soon as it finds the key that matches its argument key it will return that key
value pair so any other key value pair that later in the list and therefore was
put in the list earlier has no effect so we might as well not have two values for
the same key so we look to see if we found the key in the table if we didn't
find the key in the table then what we want to do is expand the Association
list with a new element so we're going to in that case create not one but two
new pairs this one is going to have the key and the value and then this one is
going to get spliced into the spine of the Association list okay that's our
goal so if you look at the line below the one where the cursor is blinking
it says cons cons that's because there's two pairs if you look up at the picture
of the Association list on the top you'll see that for each key value pair there's a pair right above it which is
part of the spine of the associate okay so we are going to take first we
make the key value pair when I say first scheme evaluates expressions from the inside out right so we're going to first
make a key value pair and then we're going to make a pair whose car is the
key value pair we just made and his cutter is could er the table which is
the head of the old head of the Association list and then finally we set
cutter the table to that new spine pair that we made
okay so we're splicing a new value into the table any questions about that okay
so you should by now be familiar with the idea that when we're building up a
list we build it up kind of from right to left that the head of the list is the
most recently added member because you make lists by Khan Xing onto an existing
list recursively okay so that's what we do if we didn't find the key in the
table if we do find the key in the table then our job is simpler record is a key
value pair in that case and we just set cutter the key value pair to the new
value so that's changing the table by mutation not to add something but to
change something that's already in it okay so notice it doesn't say the first
one said set could or the table the table is that yellow pair up there this
time we're saying set could or record which is the value returned by a sock so
it's a key value pair questions about this
great okay so what would we do if we wanted to have more than one table well
we would just add an extra argument to get input called table and every place
where it says the table we just use the argument table instead so we can have lots of tables each one would be a pair
like that yellow pair with a start table star in the car and the association list
so they could oh by the way why is it star table star it's an old old list
convention which I don't think they follow anywhere else in this text that
sort of manifest constant symbols that are not variables but just use them
themselves have stars around their name it's like declaring something constant
languages that have that feature but it's not a type declaration it's just a
reminder to the programmer so the stars are not important we never actually look
nothing in this code ever looks at the car of that header pair the sentinel
node that's important or will be important in just a moment when we talk about two dimensional tables so even
though I said at the beginning that you could use this as a kind of type tagging in fact we don't do any type checking we
just assume that the argument that's supposed to be a table is a table okay
why is that important well let me look over to this picture so what's a
2-dimensional table well first of all
look only at the stuff above where my arm is and it looks just like any table
it has a star table star a sentinel node at the beginning and then it has a spine
and each element of the list is a key value pair except this is a key one pair
because we're going to have a key one and a key too all right we're doing a 2d table so what
we have is a plain old table of key ones now for
value I put dot dot dot here not as in goes on forever but as in I don't want
to talk about it right now but there's one example that I actually worked out so this Karen yellow and this
is something it's a stupid little detail but a lot of students get confused when they see this picture in the book partly
because the book is in black and white so I'm having this in yellow should really help I think if you're paying
attention this pair does double duty as far as this first top most table is
concerned this is just a key value pair just like these ones key value key value
it's a key one the same as all those other key ones but now I'm showing you
which value is namely not a table but an association list so the thing that
confuses students is why don't we need a star table star pair right here the
answer is this yellow pair is the sentinel node for the table that
includes it along with association list okay so it's not really a key value pair
the value is the pair right because this
pair is the sentinel node for the second table that has key to value key to value
right so the way you look things up in a two dimensional table as you start by
looking up the first key treating this as a one-dimensional table and you take
the answer you get from a sock not from get from a sock which is this key value
pair and you say guess what I'm going to treat this as my value namely the table
for the key twos that go along with this particular key one okay questions about
that yeah
yeah we're making a two-dimensional table so it's like the table that we used for data directed programming where
there was a row key in a column key so the row key is key one of the column PC
- yeah how do you question is how do you
differentiate between a one-dimensional table where the values happen to be
lists and a two-dimensional table and the answer is you built the table you
know what you're trying to do it with it if it really bothers you you could make
that first pair say star 2d table star if you want to be able for some reason
to pass around both one dimensional two dimensional tables mixed together but ordinarily that's not going to be the
case ordinarily the application that you're using means either that all your
tables are one dimensional or all your tables are two-dimensional however one of the homework problems that you're
going to do is to implement multi-dimensional tables where instead
of having a key one argument in a key two arguments and a key three argument you have one argument that's a list of
keys kind of like a type signature you get all the keys together in a list and
use that to look up in a structure that can have any number of dimensions and then the way you know is that you
believe the user the user gives you a list of length 1 then you give the user
back whatever the value is for the key 1 etc okay um alright so again this is not
the world's most intellectually interesting point but it's something that trip students up a lot how that
pair serves double duty and from if you look at it from above it's a key value
pair if you look at it from below it's the sentinel node of the second table by the way how long does it take
to look something up in this table data of what what's in the number of
elements on the table nope somebody
raised and it's just mutter because I can't hear the muttering yeah the number
of keys yes but it's the number of key
ones plus the number of key twos in the worst case half of that in the average
case because in the worst case what we're looking for 41 turns out to be the very last key one
and then when we get to the second layer table it's the very last key to so it's
the total number of key ones plus the total number of key twos so it's linear in the sum of two things but that's less
than if you implemented this table there's a simpler way to do two
dimensional tables which is just to make the key be a list of two words right and
check both keys at once in a single linear table and the problem with that
is the then it would be that the running time would be the number key ones times
the number of key twos because that's how many key 1 key 2 possibilities there
are so this is a little bit more efficient in time at the cost of a
little bit more complicated data structure okay
right should we use equal or EQ when
we're looking to see whether the keys match okay let's take a vote
the votes for equal votes req okay
you're both right it depends on what you're doing in all the situations in
which we've used tables and we'll use tables in this course the keys are
symbols since they're symbols they are
[Music] EQ if they're equal so it does oh wait a minute I take it back
there'll be a couple of situations coming up down the road in which we use
numbers as keys and remember I showed you last time two numbers that are equal
are not necessarily EQ if the numbers are very large like more than plus or
minus 2 billion and so if you have
numeric keys then it's the right thing to use equal to make the comparisons if
the keys are just words it doesn't matter if the keys are lists then it
depends whether you mean to test that these two lists look the same or whether
you mean to test but it's the identical list so you would use either EQ or equal
in that situation because it depends we
have actually two procedures for looking things up in Association lists the other
one is called a ssq ask you it sounds
kind of funny but that's its name which is just like a sock except that a sock uses equal to
make its comparisons and a skew uses EQ to make its comparisons okay so you get
your choice okay where am I looking
right along this is great okay memoization so exercise 3.27
is one that asks you to draw an environment diagram for Fibonacci
numbers and it's a big pain in the neck if you actually get it the diagram you
got was long and complicated but let's
look at
hip dad scum
so what we have up here the first procedure fib is the simplest most
straightforward possible way to implements of Bonacci numbers namely numbers 0 & 1 are 0 & 1 so if n is less
than 2 return n and otherwise return the
sum of fib of n plus 1 at n minus 1 sorry in fib of n minus 2 because that's the definition of Fibonacci numbers
right each one is the sum of the two that came before it so if we actually do
this we can take you know fib of 6 good
above 15 tip of 20 see there was a
little bit of a pause there that's fib
of 25 has quite a noticeable pause fib
of 30 it is already way too slow to be
comfortable so as you know for this
particular problem there's an iterative method of doing for Bonacci numbers that
runs in linear time but I want to look well this thing is taking its time now
that we always finally got an answer I want to look at this implementation so
I'm going to say fast fib of 30 what oh
did I make a mistake here that's 230 huh
Oh wrong getting blue let's start again
I wanted to use the table that we the two-dimensional table did we built in and I had this one-dimensional table in
the way so let's love and now I can say
fast 30 and I get the same answer but I get it instantly takes a little while
but not exponential time it's only quadratic time oops
oh I see
ah so that's what I'm in control oh
there we go that's how big it is so how does this
code work it works by a technique called memoization which is a little bit of a
tricky word I'll write it down doesn't
have an R in it it's just memoization although it's related to memorization because what we
do is every time we compute a value for this function we remember it and here's how that works fast fib says if n is
less than 2 returned in same as before and now let me do a get this is the kind
of get that has two keys so the situation I was telling you about before where one of the keys is a number so the
first key is the word fib that's sort of the operator that we're doing to only instead of a datatype the other key is
the number that we want fib of so we look to see if the number is already in
the table if so just return it if not
then I call fast fib twice add the results put it into the table and then
return that value from the table it's loop I could have used the let to put the sum
in the variable result and return that but it's just as easy to get the result
so if we look at the table what we find
is I can say get fib 100 and it scored
in the table and I can also say get the 99 which is a
slightly smaller number because all the intermediate results is stored in the table because the reason the ordinary
fib takes exponential time is that it's doing redundant work right does
everybody understand that that let's draw a picture I want fib of
100 in order to do that I need 99 and 98 well for 99 I need 98 97 97 96 97 96 96
95 96 95 97 96
okay so we're calling fib of 96 1 2 3 4
5 whoops nope that's what I was doing
so just 4 times 4/5 of 96 because it's
four down from 100 I guess so by the time we get to fib of 3 we're calling it
a bazillion times and namely 2 to the 100 times more or less and using this
table for memoization avoids that repeated calculation so how long does
this take do you think native what theta
n later then squared maybe
hey you might think yeah ah good
question well now you know how tables are implemented you tell me is our table oh and lookup time you know the table
that we gave you with the get input is that table it's one of those so you
might well think that the answer is theta of N squared because we're making
in calls to fib and each one does the
lookup that takes theta of n time as it turns out we're lucky about this because
entries are added to the table at the beginning so when I'm trying to compute
fib of 100 it just so happens that fibbed 99 and 50 98 are at the front of
the table so it takes a constant amount of time each time to do the two lookups
that we have to do and therefore the whole computation is Theta event
provided that the numbers are smaller than plus or minus well plus like that's
two billion when the numbers get bigger than that the computation the adding for
each number takes time proportional to essentially the number of digits in the
number which is login so the running time for very large numbers will be n
log n okay but that's you know knowing more than you want to know about how
numbers are implemented basically as far as the table business is concerned we're
just really really lucky about the order of things in the table and so each lookup takes a constant time instead of
theta n time if we put things on the table and random order then it would
take theta n time to do each lookup um
okay so that's memoization now we did this
memoization using a particular kind of table structure that is built into our initialization file for scheme for this
class you don't have to use this particular data structure so you know
when you're finished with this class you may never again see exactly this kind of table but you will I promise
see memoization and it's going to really save your life it's going to take
problems that would otherwise use exponential time and turn them into
plenty err time or maybe it works quadratic time programs so really really
really important technique for optimization that's based on let me
remind you the ability to mutate a data structure because what makes memoization
work is those set cars in the put
procedure ok Oh which reminds me it's
fast fib a functional program take a
vote he says yes he says no oh come on I
think like hardly anybody voted here's a sideway some yeah is that a hand up I don't know ok ok it's a tricky question
it's a really complicated question the argument for yes which is a very good
argument is that if you pay no attention to its implementation
it is absolutely functional every time you call fast fib with the same
arguments you get the same return value
the argument for not being functional is that if you look down under the
abstraction barrier you can see that things are being done by mutation that makes it not functional
the counter-argument against that argument is every single thing you do on
a computer if you look closely enough involves mutation you will learn that
when we get to 61 C and you learn about how computers actually work you will
find that you're doing mutation right and left even in the most functional of functional programs so that kind of
licenses us not to look below the abstraction barrier if the program
actually is functional in its behavior now its behavior is a loaded term its
input-output behavior is totally functional it's running time behavior is
not because if I asked for fib of some
really large number like a thousand it's going to take a while the first time
second time it's going to take no time at all right because it's right there in the table at the front of the table
in fact so if in behavior you include
how long it takes to do something then you would have to say that this isn't functional is that ever anything other
than a quibble yes if you're in the
computer security business because if
you have as is common in military applications different people working on
the same computer with different security levels and somebody with a high
security level wants to elicit ly transfer information to somebody with a
low security level which really secure operating systems know about security
levels don't let you do that one of the backdoors to doing it is to artificially
change the how busy the computer is in
the high-security persons program and then the low security persons program
just keeps asking the operating system what's the load average meaning how many other programs am i competing with right
now and that number goes up and down and you can use you know Morse code or something to transmit very slowly
whatever information you want yes somebody said something well they're
mine cancer information from a high security level to a low security level so if you're a security person that is
to say a professional paranoid then you have to say that fast fib is not
functional for the rest of us I'm willing to say that it is functional
because it doesn't make any visible change in the environment the table is all you know beneath the surface and
it's input-output behavior is repeatable so all of which is just a way to say
that these ideas about functionality are a very important and be a little
complicated to really really think through um what if we try to memorize
the random procedure is that a good idea
no right if we do memorize random of 10
the first time we call it we get some number you know three or seven right
those are the numbers that everybody picks and you say pick a number from one to ten so I'll pick four just to be different
I say random 10 and I get four next time I say random 10 I'm going to get for the
next time I'm still going to get four and so on forever so if the underlying
computation is not functional then memorizing it won't work it
actually makes your program incorrect so this is a reason that functional miss
are not as important because it helps us decide can i optimize my program by
memorizing this computation okay oh yeah
later on when we get to streams and I
don't know a few weeks we're going to see another important example of an
implementation of functional behavior that is not functional in the
implementation so that's an idea that's going to come back to us okay any questions during the end huh pretend
you're actually finished early okay see you Friday all Friday we're going to talk about vectors which are not in the
textbook so your only resource is my lecture notes page 327 for reading about
UC Berkeley