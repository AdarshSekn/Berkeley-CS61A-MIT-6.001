Transcript


okay good afternoon um this week we're talking about
streams which are an alternative implementation of the idea of a sequence
um so far we've seen two different implementations of sequences namely lists and
vectors and remember we said the difference between them was one of efficiency certain things were more
efficient with lists and other things were more efficient with vectors uh now we're going to look at a third
implementation of sequences and uh find out about its efficiency properties
which are pretty cool um so we are
Okay so behind me on the board I guess I should put it
up so I'm not in its way behind me on the board is the definition
of a prime number an integer n is prime if it's greater than one and
um it has no factors other than itself and one saying that another
way it has no factors in the range of numbers from two to n minus one right so
here's a um a helper procedure called range
and what range does
is return a list of the integers between two values starting and ending value
uh so using that I have a predicate prime question mark that takes a number
in it constructs the set of numbers where we
don't want it to have any factors so the range from 2 to n minus
one and then we say filter that list of numbers with the
predicate um is the remainder when we divide n by
x zero which is how you say is x a factor of
n and then finally we say is that set we
got from filter empty so if it's empty then there are no factors between 2 and n minus one and we
can see that in fact um if we ask is six a prime it says
false if we ask is seven a prime
oops five would have worked
too let's pick an odd number that isn't prime
just make sure that works everything is fine okay so prime works um and it works
in a way I want to claim that really precisely models the ma mathematical
definition of a prime number so you can read this
code these three lines right here and say okay I'm picking out the factors of n in
the range 2 to n minus one and I'm asking the question are there any or not
if there aren't any it's prime okay
um however there's a problem with this algorithm
that's this let's find out if a million is
prime so while we're waiting you tell me is a million prime no how did you know a million
isn't prime it's even right it's divisible by two oh not only did it take a long time
we didn't get an answer at all let's try again
we'll ask if a 100,000 is prime so what it's doing is creating a
list whoa
man this used to work
sorry no no i've always done it locally i just
used to have a real computer instead of this one you know that one back
there ah okay 10,000 isn't
prime all right so we ask about the primitude of primality of large numbers
large even numbers and it generates this huge list the reason I was getting segmentation fault is it's making a list
of length a million or a list of length 100,000 minus two right so for a million
it's 9999,998 numbers in the range that we're interested in then it's going through
that entire list asking each number are you a factor of a
million and it gets a whole bunch of factors of a million two and five and 10
and so on um and then it says is that
list I got empty and the answer is no it isn't but that's very very
inefficient um and so therefore getting to the punch
line therefore people tend to write programs like this one
so now I can say prime six
no prime 7 yes
prime a million no it's not
okay now if I
ask is a million and three prime prime it's still going to take a while
to come up with an answer okay if if the number is prime
then we still have to check all the possibilities while we're waiting yes it is how does this program work well it
has a helper function called it whose argument is a candidate for being a
factor of n and down here we start out uh with factor being two because that's
the smallest number that counts for making something not be prime and what
it does is it says have we reached n is factor equal
to n in other words have we tried every possible factor from 2 to n minus one if
so n is prime otherwise is n a factor of I'm
sorry is factor a factor of n if so then the answer is
false because we found a factor between two and n minus one so the number isn't
prime otherwise call it with factor plus
one as the argument okay
um so everybody agree that this program works yeah and this is the one you wrote
in junior high school yeah yeah yeah he says "Couldn't we optimize
by only checking up to the square root of n?" And yes that's true and it's pretty important actually because the
square root of a million is quite a bit less than a million so yeah that would make a big difference um I didn't do
that for any of these versions that I'm showing you just to keep things simple so yes all of the versions that we're
looking at could be optimized by u checking only up to the square root okay
um okay the problem with this version that's on the screen here I want to
argue is that it's not very easy to read i mean because its name is prime
question mark you know what it's trying to do but if it were named mystery and you saw it on a midterm saying you know
in one sentence what does this mystery procedure compute it would take you a while to figure out that it's checking
to see if n is a prime number okay certainly it would take you a while
to be sure that it really succeeds that you know it doesn't mistakenly check for
one being a factor or not check for two being a factor or something like that um
it's just a lot harder to read I think even though it's more efficient so
um I want to have my cake and eat it too it's what computer science is all about
being immature and wanting to have your cake and eat it too and figuring out a way to do that um so here's what we're
going to do wait yeah I'm in the right
window helps if you spell it right
okay so this version looks exactly like the first
version I had except that the word stream is thrown in here and
there so it says stream null of stream filter
same filtering predicate stream range same
arguments all right and now if we load
this I can now say oops stream prime question mark
of a million and get false right away
or any number you like
false and of course uh for small prime numbers we can try it on like um 17 says
true and for the same reason as before I'm not going to try on a large prime number because you know we'll get in
trouble well let's no let's do try it on fairly large prime number anyway
uh what did it It failed on a 100,000 before right see what
happens whoops i didn't mean
that okay so this version succeeds it doesn't say segmentation
fault so what I've done here is write a
program that essentially looks like the one we started with the one that made
the list of all the factors here we're making a stream of all the
factors and then it picks out the ones that actually are factors of n and then
it asks the question is that result empty so it works it looks like the
first version and yet it has a running time like the second version namely instant for uh composite
numbers with small prime factors um and doesn't blow up for large
primes okay um how is that possible
streams by the way [Music] um work just like lists so here's cons
stream and we also have um stream car and stream coder if I
um show you the definition of stream filter you can see
constream and then stream car of data and here's a recursive call on stream
cutter of data okay
so conar cutter just like lists and yet it has this very different behavior why
is that how do we make this work well let's see what happens when I say
well first of all let me just remind you about range 3 to 8 gave us this list now I'm
going to say stream range from 3 to
8 and I get something different what I get
is this is I'm going to just abbreviate by calling it range even though for for
chalkboard purposes range from 3 to 8 gives
me a pair whose car is three so far just like
a list and then where the next pair of the spine of the list should be is a
promise to
compute the range from four to eight later on
okay so this this um cloud shaped thing that's supposed to look like a cloud is
a promise um and you can see it's actually called a promise in
SDK um and what it says
is if you call stream cuddter on this
stream then you're cashing in the promise and I will do whatever the
promise says when you do that that's how the promise gets cashed in you ask for stream
cutter of this stream now does that mean that if I ask for stream
cutter of stream range
38 am I now going to get the list four through eight no
i get a pair whose car is four and whose
coder is a promise to compute the range from five to eight so each time you cater this stream
um you get one more element plus a promise is that clear everybody
understand that i know you don't know what a promise is yet but you get the idea of what a promise is for right any
questions
what about when you get to the end so the base case here in stream range
says if from is greater than two which means we've run out of numbers to pick
return the empty stream it's a thing streams are an
abstraction okay um so just like lists in the list abstraction to make lists
work we have to provide two things one is pairs and the other is a thing called the empty list so for streams it's the
same business we have pairs whose coders are promises right for lists it's a pair
whose cter is a list for streams it's a pair whose cter is a promise presumably
also to compute a stream um and there's this thing called the empty stream which is how you know you got to the end
okay um
okay so why does this speed up
um finding out whether a million is prime well
[Music] um what I do so remember it's
stream
filter some predicate right lambda something and then extreme range
uh from two to n minus one whatever that is
right yeah
well we call stream filter we have to evaluate these arguments we evaluate the lambda expression we get a procedure we
evaluate this call to stream range and we Get a
pair whose car is
two and whose cooter is a promise to do stream
range from three to n minus one
right now that's a value that was computed in
essentially no time right constant small constant time because we're only really
looking at one element that's what we give as the argument to stream filter now you
remember how filter works right it says is my input empty if so return the empty
list otherwise the next there was a three-way con clause the next clause says um does my
car satisfy the predicate if so
cons the car onto a recursive call to
filter if not then just do a recursive call to filter on the
cutter okay well the predicate says is the
car a factor of a million yes it is
so what does filter return a
pair because stream filter calls stream calls
constream so we're going to have to talk in a bit about how constream works but what it returns is two because yes
that's a factor and we're collecting all the factors of a million and a
promise to do filter
stream filter of this function
over the thing that that promise promised right stream
range 3 to n minus one okay that's what we're promising to
do stream filter returns this stream filter's finished at least for now because it
found one element of its output and it's only promising to do the rest later so
it hands this to stream null does stream null have enough
information to know whether or not this is empty yeah it does this is not empty it
has at least one element so even if two were the only factor of a million we already know that two isn't
that that a million isn't prime okay so stream null is going to be
perfectly happy having found one element and therefore is never going to
cash in the promise to look at the rest of the elements so all those promises are just going to be
unused and that's why streams can do the job
quickly right yeah
yeah good question um let me reward your
question by going back to stream
filter and looking at this right here so u stream car satisfied the predicate
tube was a factor of a million so we do this well when you call a
procedure first we evaluate the arguments because scheme is an applicative order language right so
first we evaluate the arguments um and one of those arguments is the recursive call to stream filter
um and that calls stream to get one of its arguments so aren't we going to cash
in this promise right away is what you're asking why doesn't that happen it's a very good question and the answer
is it doesn't happen because and this is the entire secret of
streams con's stream is a special form okay everything else here is just
regular old stuff but constream is a special form i mean even special forms you've seen special forms before i mean
they're different but they're not really deep magic you know uh they just don't
evaluate their arguments until you know they decide whether they should or not so the way it works is if you
say constream AB
the evaluator sees oh constream that's a special form um in fact it's an
abbreviation the way let is an abbreviation for something it rearranges things
syntactically constream is an abbreviation also what it abbreviates is
cons plain old cons that makes a pair a because we want the stream car to just
be the what the car would have in and then
delay B okay now
constream is not a scheme primitive it's something that we added
um to do the stuff in the book about streams delay however really is part of
Scheme it's built into Scheme but I'm not allowed to say it's a scheme primitive because it's not a procedure
at all it's a special form so delay is a built-in special form that takes any
expression and returns a promise to carry out that expression
later so delay
expression returns a promise to do expression later
okay is that clear and that's why I'm finally answering your question that's why
stream filter returns right away because it does constream rather than cons and
that means the recursive call the thing that's the second argument to constream
is delayed so we just make a promise to call stream filter
later okay
everybody happy so far um okay so I want to back up here a
minute and look at this sort of the important procedure of this
example and I'd like to make sure you really appreciate what it is that we've
done here with very little in the way of underlying mechanism basically just
delay um we have
decoupled the sequence of events in the computer from the algorithm as laid out
in the code okay so according to this code we
get the whole range of factors of possible factors from two to n minus one that's what this code says give me the
range from two to n minus one okay um now according to everything
we've known up to now that means we have to sit and wait
while we generate a big list of numbers the actual sequence of events in
the computer is much more like that second version I showed you the
iterative one that didn't make all the factors in a list but just made them one at a time that's what we're doing we're
coming up with factors one at a time to try out
yeah how would you calculate the running time of this the order of growth of running time um well
um the worst case running time is sort of the same
uh the worst case is you have a large prime number in which case um it's basically
theta of n because you have to check every value to find out that it isn't a
factor before you can say conclusively that this number isn't prime now as someone over there said we can make it
theta of square root of n which is a lot better because um if a number doesn't
have a factor less than its square root then it doesn't have a factor bigger than its square root either okay um so
worst case theta of square root of n for doing it for any version of no matter
how you write your prime program there's no getting around the fact that you have to try all those things well that's not
true um the book points out in a little bit of heavy mathematics that some of you
won't like but the book points out that there are some interesting ways to find out if a number is prime that almost
always give you the right answer uh and are very
fast almost always meaning almost always the book says um the probability of
getting a wrong answer through this algorithm is smaller than the
probability of getting a wrong answer because a cosmic ray happens to strike your computer at the wrong
moment um so it's really very good but um it's not perfect it's not
mathematically you know anyway
um if the number is composite then the running time will be
theta of its smallest factor other than
one right um so some primes
um I mean some composite numbers sorry uh they have exactly two factors other
than themselves in one and both of those factors are huge 80digit prime numbers
um so it's really very difficult to check whether that number is prime or not numbers composite numbers like that
that are the product of two very large primes are at the heart of modern
cryptography basically you tell people one of the factors or no you tell people the the product That's right but you
don't tell them the factorization and you need the factorization to decode your message okay
um okay well that was a little bit off to the side but no it's not it's it's important for you to know I guess um but
but let me restate one more time because it's really important what we're doing
is decoupling the sequence of events in the computer from the form of the
program so this is an amazing piece of abstraction right in essence uh you're
telling the computer to do one algorithm and the computer is saying "No I can do this faster than that i'm going to use
this other algorithm and yet I promise to get the same answer." Um and you don't have to worry
about it that's really amazing and the mechanism to do that is just delaying
the evaluation of one argument to cons
um by the way how does delay work delay is built into scheme um so
you might think of it as you know a piece of complicated
magic but we're going to implement delay version one of delay
um as again a syntactic abbreviation so I'm going to
translate delay expression into something else
what I'm going to translate it to is lambda no
arguments expression that does it
right because when you see a lambda expression do you evaluate the
body no you don't evaluate the body until you
call the procedure so the opposite of delay by the way is called force uh
that's not a special form it's an ordinary procedure so we say
define force of some promise to
be call that promise right because the promise is a
lambda expression with no arguments we can invoke it invoking it evaluates its body which is the
expression that we were delaying before everybody see that this works any
questions about that
yeah okay suppose that the number that we have um isn't divisible by two let's
say we want to know if nine is a prime okay so we make maybe I should
actually draw this
out so I want to know if nine is prime so I'm going to make the range from 2 to
8 okay which
is two and then a promise to do range from 3 to 8
yeah now I'm going to give this to filter filter is going to say is this
empty no it's not does car stream car of it satisfy
the predicate no it doesn't because two is not a factor of nine else it says in stream
filter stream filter I'm going to make a recursive call to myself with the same
predicate and stream coder of my argument list my argument stream
right so it does a recursive call to itself having called streamter stream
coder forces this promise so stream cutter and this is happening
during the call to filter this is none of this is delayed because the delaying
only happens in constream and we only call constream if we want to keep this
value in other words this value is a factor as long as it isn't a factor
stream filter keeps on doing recursive calls in the same way that filter does recursive calls okay so we try again we
take the range from 3 to 8 and that is three followed by a
promise to do range from four to eight stream filter says is three a
factor of nine aha yes it is so this is what stream filter
returns okay does that answer I forget whose question it was did that answer the question yeah okay good we only
barely have time to get to the crucial next step
um oh no before I ate the crucial next step I have to point out something else i've been writing on the board things
like when you do uh range 28 you get a promise to do range
38 well if we look in the actual constream here in stream
range and the important part of it actually is this here's what we're going
to promise to do this doesn't say stream range 38 it says stream range plus from
one two
well when I force this promise it can be some completely different world how do I
know what from and to means well that's a lucky side effect of lambda because
you now know from the evaluation model of environment that lambda creates a
procedure and what the procedure
is running out of boards already what the procedure is
is two bubbles this one basically is just a
pointer to the expression because there aren't any arguments right but what is this it's a pointer to an environment
and guess what we have from is two two is
eight okay and the expression in this case is um stream
range plus from one
two okay and all of this is the
promise so promises carry around with them the correct values of variables for
this particular promise that we're making and that just exactly does what we need so it's important to understand
that too okay now for the fun
part I need from this colored chalk
collection couple of colors here so
here's
define range from
to if greater than from to empty list
uh otherwise cons
from onto
range plus from one two close range
close con close if close define okay that's the plain old range for plain old
lists so here are the changes we made
we changed the name we changed this to the empty
stream we changed cons to
constream uh and we called it
with Okay so the change of name that doesn't do anything really that's
trivial we could have kept it the same name i just wanted to have them both around at once to let you in on our secret the
empty stream is actually the empty list we could have used anything it's just being compared against but we use the
empty list so really this isn't a change at all the only actual change that matters is this little thing right here
so we made this teeny tiny little change to the program and it had a huge huge huge
effect on the program's behavior
right now we're going to do something different i'm going to do
this recursion without a base case what should happen
infinite loop right looks like a disastrous
change so let's go ahead and do it except
um I'm going to change the name
and because I'm not doing this base case test anymore I never use the argument
two so I'm just going to get rid of that also and I'm going to say
um constream
from bus from
one whoa what does that do essentially nothing interestingly
enough I say um ins from
one and I get an answer which is one dot a promise to do ins from two so I'm
going to actually just for ease of use define integers to be ins from
one um and now if I look at integers I get this um unedifying thing um but we
have something called show stream uh it takes a stream as argument
and it does this it gives you um if there are fewer
than 10 elements it just looks like a list otherwise it gives you the first 10 elements and then a dot dot dot okay so
you can see what you've done here um you can also say oh there's an abbreviation
for show stream it's SS it takes an optional argument where
you can say how many values you'd like to see okay
um so that's the integers we have all the integers in our computer
i can say uh show [Music] stream
map lambda x times
x2 integers and what I
get is I don't have a parenthesis there we go i get all the
even integers okay so we can do arithmetic on
an infinite data set in no time in this tiny little box I have all the
integers um that's pretty amazing as an
abstraction [Music] um okay we're going to do something even
more amazing um it's called the civ veritoines and works like this you write
down all the integers starting from two this is going to take me a few minutes
no I'm kidding that's enough um and then what you do is this
here's the algorithm circle the first otherwise unmarked number it's
prime now cross off all its
multiples did I get them all i think so repeat just like
shampooing so take the next unmarked number that's three circle it it's
prime now cross off all its multiples
okay some of them we crossed off twice it doesn't matter okay repeat find the
first unmarked number circle it it's prime cross off all its
multiples basically that's all I have to do rest of them we all got already um
circle the next number cross off all its multiples of which there's only one left
49 because all the other ones are seven times something smaller than seven so
we've got them already um and that's it all the rest of these numbers on the board here are are
prime okay that's the veritoines
so what does this say so we take stream coder of integers because integer starts
with one which doesn't count for primality we want to start with two um
and we call civ civ takes a stream of all the numbers that haven't been crossed off yet
basically it says constream the first number that's like
drawing a circle around the first number we keep it it's prime and then we do a
stream filter on the stream coder of the stream where we say uh take out all the
ones that are divisible by um the stream car
um and then we just recursively call civ on
that okay so that's an infinite recursion and here they are all the prime
numbers all right that's a pretty amazing piece of computation
um and how we got there is
um by understanding abstraction basically by saying we can take the idea of a sequence and we can implement it in
this completely different way and also by understanding something else which is
normal order evaluation because that's basically what a special form does right
so constream um well it's kind of a hybrid it uses
applicative order for its first argument um you could write it the other way if you wanted but it delays which is to say
it normal order evaluates its second argument it doesn't evaluate it until somebody needs it till somebody calls
stream cutter okay so this is just an incredible result
that I can't get over it every time I see it it's amazing all the prime numbers you want to see some more
there okay all right see you Wednesday
UC Berkeley