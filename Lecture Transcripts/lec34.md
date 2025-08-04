Transcript


afternoon okay um
i did my income tax yay i'm in a good mood yeah
i know that's what i did all day yesterday it's a good thing that the berkeley public
schools have spring break this week so instead of being with fifth graders i did my taxes okay
um prior to this friday that's two days from now if you haven't already done so
please read the therap 25 article that's in volume 2 of the course reader
because we're going to be talking about that friday um i think oh no one more little administrative announcement
there is a midterm next week i think wednesday
it does have a group part this time the group part comes first because it's
different questions from what you do on the individual part so your overall score comes from the group part plus
your individual part um so you should arrange where to meet your group
um ahead of time so you find each other right at the beginning
otherwise we'll be off to a late start which is bad um
historically midterm three has had a
higher than average incidence of us catching people copying
um and i think that that has to do with the fact that you start with the group part and you kind of get in the swing of
working with your partners and then you forget when the individual part comes that oh yeah now i'm not
supposed to do that anymore so don't forget um okay
back to work i want to remind you up on the board is um the
the two changes i made to the range procedure first the yellow one this teeny weeny little change i changed
the word cons to con stream and also i changed the name of the procedure but um
for purposes of making this point i'm only putting the really essential change all the other ones are just what things
are called consticon stream um sounds like
you know it should have hardly any effect on the process
that the computer goes through to carry out a call to range and yet as we
saw it has a very profound change um so it doesn't do what it looks like
it's doing it all and then by contrast in red i crossed off the base case check
and that looks like it ought to have a very profound change on the program's process namely that it should
never give you an answer and yet we discovered that that that's not the case that it really doesn't
change things at all except that you get an infinite stream instead of a finite stream
and then you have to wrap your mind around the idea of an infinite stream and we have that sieve procedure that's
up on the screen that i showed you right at the end last time that makes the point that
it's not just something trivial like all the integers you can actually construct
an interesting stream in this case the stream of all the prime numbers so you have essentially all of the prime
numbers in your computer and that means you can write programs
starting on the assumption that you have all the primes so basically you don't have to write programs that have limits
built in so if you're trying to let's say write a program now that finds the prime factors
of a number you don't have to say as you did in junior high school
well i'm going to find prime factors of all numbers up to a thousand
or something and then have a finite list of primes in your program uh to make that work up to a thousand
you can say i can find i can prime factorify any number uh because i have all the primes in my
computer and if you write a program that way and if you believe hard enough just like you know believing in fairies and
saving tinkerbell if you believe hard enough it will actually work now if your numbers are very big it will
work very slowly but if your numbers are very big any program will work very slowly
it's not special to streams um
okay so
a few more points we're almost um at the end of the big ideas so the the
big idea here is um delaying the evaluation of one of the
arguments to constrain and you should see the relationship between that and
normal order evaluation that we talked about way back in week one in which we delay the evaluation of everything
until we actually need it namely when we call it primitive um
well constream is a primitive but let's imagine well no costume actually isn't a
primitive we wrote it um but and that's important because we
don't want it to evaluate its arguments so special forms don't necessarily about the arguments primitive procedures are
different um okay and let me put back up on the board
um the way that we implemented con stream so i said whoops
stream a b
is equivalent to cons a
delay b and i said
delay of an expression is equivalent to
funk of that expression
this is not quite as trivial as it looks because remember that the result of
evaluating a lambda expression isn't just a container for its body it's
also the environment in which that lambda was seen so that we know what the values of variables are like from and to
in the call to range um but that simple version is actually a
little bit of a lie um and the reason is that we do an
optimization namely we use memoization you learned memoization about a month or
so ago um it's the idea that when you compute something
the first time you remember its value um and then the second time
you just have it already available so the code is in the book
for this but they actually define delay of an expression to be
memo-wise of lambda of nothing x and memoize is a function that takes a
function and returns a memoized version that um remembers its argument so a memoized
function has this state variable it says two state variables associated with it one is have i been evaluated yet true or
false and if that one is true then there's a value variable that
contains the result from that evaluation so if that says true then you just pick
up that value and you don't have to reevaluate the body um that you that was delayed
so force um calls a memoized procedure rather than just calling
lambda nothing x directly um so that again is just an optimism
well it isn't just an optimization because it means that
if the thing that you're putting in your stream [Music] your con stream had a side effect like
printing something or changing the value of a variable it's only going to happen once not each time
so let's start up this game here
um so
oops
so this thing um makes a stream whose first element is one
and whose stream cutter is a promise to look up the value of ones
so every element is the same as the first element okay
now let's try this
it's going to give me a stream of random numbers
look and see now it's only going to do this
once all right so let's try it a different way
how about this
who thinks i'm going to get a stream of random numbers who thinks i'm not going to get a stream
of random numbers ah come on be brave he thinks i'm going to get a stream of
random numbers he thinks i'm not going to get a stream of random numbers okay let's try it
looks like i am um so how did that happen well
i hope what you're thinking is that based on what i just said the stream would be memoized
um so that when we asked for the stream critter we would just get that stream again
that's not actually quite right because the stream cutter isn't
a symbol like ones the way it was or ran stream in the example that didn't work
it's a procedure call so each time we're promising to do a procedure call and each time we do do
that procedure call now what is true
is that the next time i look at that elements of that stream i get the same stream
that would not be true if um we didn't memoize i think
i think we'd get a different one each time because we would keep forcing promises
we'd probably get the same first element but all the rest of them would be different something to experiment with yeah
the one that didn't work the one that didn't work was right here
and that doesn't work because the thing we're delaying is just
look up the value of the variable rand stream it's not saying do another procedure call
so the value of randstream is a stream that starts with an eight so it's stream
cutter is also going to be a stream that starts with an eight it happened to be eight that i got if i did this over
again it'd be a stream of some different random number repeated infinitely so
it's the difference between looking up a variable and calling whoops
calling a procedure okay um
all right good next thing so going along with what we
just oh yeah
is there a stream ref function um i don't think there's one built in but
it's easy enough to build just you know re do end quitters and then do a car
um yeah that would be a terrible idea if we weren't memoizing but since we are
it's not it's okay yeah
okay the question is up here if we said cons instead of con stream
would it generate an infinite list of random numbers and would each one be different
and the answer is there's no way to find out because it would run forever without giving an answer
um is that true no wait if we just said cons oh no right if we just said cons instead
of constrain what would happen
is this okay so we would be making a circular
list of one pair
yes can you define something using itself if
it's not deleted yeah good point um you're right what would really happen is that um
if rand stream were not previously defined we'd get an error here and if rand stream were previously defined yes
i take it back about the circular list it would just error out because
there wouldn't be a rand stream to to cons onto
so this this thing that um that we did to get ones
and also what we did that to successfully make the stream of random numbers
is an example of sort of just-in-time manufacturing
right so when you do this there's really only one one
and a promise when you stream cutter it
we make a new pair whose car is one and whose critter is a promise don't we
no we don't uh in this case we don't but
in this case oops
with make ran stream we do we generate each pair just in time
it's not like we make them all we have exactly as many as we need in
order to do what you needed to do which is kind of cool but something you have to remember another thing to think about by
the way is that since rand stream
once we've generated it is always the same this is a way to write a program
that uses random numbers like to you know calculate the value of pi
by seeing if the toothpick fell on the who's it
is functional every time you do it you get the same answer
if i say give me you know the result of a thousand toothpicks falling and then i say again give me the result
of a thousand toothpicks falling i'm gonna get the same answer okay because
in principle the answer was computed at the beginning
as soon as we make this random stream you know your value of pi
in principle is um ready for you all along but in fact you have to
ask for a particular number of iterations and then you then you get the result and
then that result is remembered so next time you ask it doesn't even have to do the computation it's just
there um so this is a way this is something that
in a moment i'll talk about how this generalizes it's a way of talking about
time varying things like random numbers in a purely functional way
namely you have all of the variations over time
in principle computed right at the beginning so you don't just have what's the random
number right now you have what are infinitely many random numbers and then you
do a computation that essentially treats that as a vector
of size infinity but a single vector right rather than a stream of numbers
and then um you're doing functional programming again which is nice because functional
programming as we saw last week parallelizes easily whereas non-functional programming doesn't
and also that brings up a related point which is streams and side effects
don't mix very well and that's because as we saw from this range example
when you write a program using streams the sequence of events is not what you
think it is okay so if you write a program
it says something like set bang x
5 and then it does some other stuff and then it says
setbang y times x 2
and then it does some other stuff and then it does set bang
x 7 and then we ask for the value of y
if this is the first time we're asking for the value of y this may not have happened yet
so the actual sequence of events in your process might be this and then instead of the 10
that you were expecting you would get 12. okay but you can't either write a program
relying on that happening because maybe you'll look at it's like sort of like quantum mechanics you know as soon as
you look at something its value is fixed like schrodinger's cat um it's just like that actually as soon
as you look at why um its value if at least if it's a
stream the first element in it is fixed and um
so the answer you get for y down here depends on whether you've looked at y in
here someplace in which case it'll be 10 or you haven't looked at y before in which case it'll be 14.
okay is that clear to everybody um
so the moral of the story is not to write clever programs that take advantage of this the moral of the story is
um only use streams if your program is functional
in style even though footnote by the way the implementation of streams
because it does memoization if you look inside it it's not functional so this is a conversation we
had before about memoization and whether the resulting program is functional or not
and the answer is if you look deep enough it's not but if you look at its behavior
not including its timing behavior just what answer it gives you then yes it is functional
and i think i may have said before but i'll say again in this context uh
the fact that it's not functional inside isn't really something to be embarrassed
about as long as the behavior is correct because
even if you write a purely functional program the scheme interpreter that's making it
work is not functional okay it does things that has state
and if um if you well let me take that back maybe
isn't functional it depends on how it's implemented um maybe if you write a functional program the interpreter is
functional too but maybe not but in any event underneath that if you look at the machine that's carrying out the program
it's not the least bit functional it's putting you know it's putting something in memory and then putting a
different something in memory and putting something in this register and all that stuff
so there's tons of state going on inside no matter what but the goal of computer science is to
provide abstractions so that we can look at the program
and not have to worry about the fact that way down deep inside there's something non-functional going on we can
think yes this is a functional program so i'm confident that it's
multi-processor safe and so on okay
um oh yeah implicit definition
so this procedure is how i made the integer stream i called it with from being one
and it gave me the stream of all the integers after i crossed off that stuff in red here's another way to make the integers
um so i have ones here
let me just remind you about ones and i can say
define integers to be cons stream one
onto stream add
it's just map plus ones
integers
oops something didn't work oh stream add isn't defined
all right let's try again um no okay
okay define integers see if this works
stream map loss lens
integers
notice by the way that i didn't get the error message until i actually tried to look at the stream
whoops does this not exist either
wait
okay let's try again define ints
see i got tripped up by memoization
stream one stream map plus
runs hints
see if this works yay finally
okay well there's no recursive procedure in here
this is not a recursive call to ins or anything this is just one call to stream map how
does that work well it works like this
first i'm gonna write down ones
now i'm going to write down ins
i know it starts with one because it says con stream one something
now i also know from
from this expression right here
that inch is sort of ones plus ins
whoops so i'm going to say here's my one and then everything else down here
is going to be the sum of so the second element events is the sum of the first elements of these things
ones and it's okay now that sounds like how can it possibly work i'm using inst to define ants
but it's okay because it is just in time manufacturing business
so we know the first elements already of ones and in so we know that this is one and this is one
so therefore i have enough information to compute the second element of the resultants
namely two and i'm going to write that down over here
well now let's find the next element of the result which is 1 plus 2.
so that's the third element events so let me put it in the third slot over here
and now i'm just barely able to do one plus three and get four and so on
okay so that's how this works and by the way that's how to solve problems on the
midterm when it says what's the value of yada yada
sometimes it says something that has an interleave in it
so we have this is called an implicit definition of a stream uh implicit meaning there's no explicit
recursive call instead there's a call to stream map involved and stream map is the thing
that is recursive because stream map is written just like map
um so let's say it's um
interlav well no it'll be cons
stream [Music] something or other
this is define b
could be interleave a b
where a is some other stream that we know or maybe we know so how do
we do that well okay let's say this is uh 7 just for fun so okay the result
so this is b so a b
the result is b so a has some set of values
b has some set of values
we know the first element of b is seven i did this wrong sorry
um
so for interleave what i want to do is not have boxes on top of each other but have them
sort of staggered the value for a so let's just call these a1
a2 a3 whatever they are right so the first element is 7 because of the
con stream now i know an element of a it's a1
so now i know the second element of b which is a1
and so on okay it might even be more complicated than that where we interleave a with
some function of a and b but in any case this is how you do it
you copy things down here and then so
this is the second element this is going to be the third element and then a2 is going to be the fourth
element and so on okay so that's how you do interleave with sort of alternating
dotted lines to fill in i hope that makes sense to you why that is
okay um talked about that um
talked about that talked about that
talked about that
okay all right did i show you this i don't think so
so
okay so what this says is the user stream procedure says keep on
calling read it's a way for the user to type something and it returns um
it's nice it return returns the stream of everything that
the user typed from now till the end of time okay so it's an infinite stream of
things the user type let's just pretend that this user stream represents um
transactions at an atm and so i'm going to say define
um
bank account to be
con stream some initial deposit
with
um
stream map plus
bank oops bank account and the result of calling
user stream
okay so now let's say um
i say show stream bank and it sits there now what's going to happen because of the way i define this it's going to be
one step behind me all the time so let's say i deposit a hundred dollars
oh no i'm going to have to do the whole thing 10 transactions to get it out sorry
so now i withdraw two hundred dollars and now i add
uh three thousand dollars and now i subtract
um two thousand four hundred dollars and now i subtract a hundred dollars and
now i add three thousand dollars and now i subtract
nine hundred dollars and now i subtract 50 dollars and i subtract 150 dollars
and i subtr whoops i subtract a thousand dollars
wha that wasn't very good
oh um
i bet this isn't going to work right
try again define bank account nothing
now let's define bank account
stream a thousand onto
stream map plus uh
bank bank account
and user stream
see if this works all right so i add 500
i subtract 100 i add a thousand dollars i subtract
fifty dollars i subtract four hundred dollars i subtract
uh 250 dollars i add three thousand dollars i subtract
four thousand dollars um i subtract a hundred dollars let's see
if i can go negative um i subtract five hundred dollars oops there we go
i subtracted five thousand dollars so i started with a thousand then i added 500
and then i subtracted 100 and then i
subtracted four oops no i didn't i added a thousand
and then i subtracted 50 here and then i
subtracted 400 and then i subtracted 250
and then i added 3 000 and then i subtracted 4 000
and then i subtracted 100 and luckily it didn't show me
the result of subtracting 5000 which would be a nasty letter from the bank and a lot of fees
um but the point of this example is that by doing this stream map
let's come up where we can see it by doing this
i am creating in principle right at the beginning
the entire history of my bank account i picked this example about bank accounts because
it's the one that abelson and sussman use at great length about object-oriented programming it's
something that requires a local state variable for what's the balance in my account right now
and you do need that if you use the passage of time in the computer to
model the passage of time in the world if you do it that way there's going to
be a local state variable called balance for each bank account but this way
i can take the entire history of the bank account and it's a constant
it's just there and i can do arithmetic on this so for instance if i wanted to
turn this into an interest paying account i could take bank account and for each element i
could add to it to the next element some percentage of the previous element
and it would be an interest bearing account and so on and i do that as a functional thing i say okay the entire
history of this interest-bearing bank account is equal to the entire history of the non-interest
bearing version modified by this function so it's all entirely functional even
though it's sort of talking about state
so the book points out that this is a functional alternative for solving a
certain class of problems it's not perfect as the book points out because
it is perfect if you only have one bank account but once you start trying to handle two
bank accounts you have to sort of take transactions out of that stream
and each transaction will be not just how much money am i depositing or withdrawing but also to what account
and then you have to sort of direct each
transaction to the right account and that's harder to do in this functional system so
that's the the problem we give up a problem namely the problem of
parallelization of non-functional programs so we talked about that last week if you have a
non-functional program and you have another one that's running in parallel with it and they look at the
same data they can step on each other's feet whereas functional programs can't do that so this functional bank account
world you can't have concurrency bugs but instead you have something else which is
um [Music] simultaneity problems knowing
what happened when is harder in this stream-based system and the book talks about the details so
i want you to read that carefully because it's interesting and important for you to get as something to still remember after the
end of the class something else to still remember after the end of the class
is an important use of the idea of streams and that is sometimes very often in fact we deal
with sets of data which although not infinite
are very large and extend over a long time so
um you have a song on your ipod yeah
and the song is two minutes and 20 seconds long
and the way we get digital music is that we take
a waveform so the sound you know pressure in and out and everything which turns into analog electric signals and
then we sample that very often to be exact
often the number is 44 000 times a second
so what's um 44 000
times um
two minutes is 120 plus what did i say 2 minutes and 20
seconds so 140 seconds
that's somewhat over 6 million samples
okay that's a lot of data
and so very often it's useful to treat things like this as if they were infinite namely as if we
had the whole thing in memory at once even though we don't we're reading the song you know 44 000 times a second
why is it by the way who knows why it's 44 000 times a second
okay sam yeah sampling but but why that number
well it's a great story that's the sampling rate that's used on cds audio cds or always 44 000 times a
second why it's actually the number should be bigger and they understood at the time that cds would
have much higher fidelity if they could get just a little bit higher sampling rate
so what they did the physical size of a cd
was determined by the width of
din deutsche industry something normal something
it's like the german standards organization car radio
okay because they wanted cds to be playable in your car radio so that's why cds are the physical size
that they are at at the time that the standards was made
there was a certain density of information that they could pack into that space
so they could take the physical size and determine how many ones and zeros they could record on the surface of a cd
and then the other variable that goes into it is how long how much time do you want to be
able to record on a cd and it so happens that the president of
sony is a big fan of beethoven's ninth symphony
so he decreed that beethoven's ninth symphony had to fit on one disc
and that's why the sampling rate is what it is on your mpg3s and stuff unless you take
action to make it bigger but that's what it always is on cds okay now um
after that little interesting digression
let's say i have my song or symphony um
and i want to do signal processing to it like you learn in ee 20.
okay so um i'm going to do a very simple kind of
signal processing for you i'm not going to write code i'm just going to draw a picture but the code is really easy if
you understand the picture um so here's my input and the thing that i would like to do is
click suppression you know when you have recorded something on analog media or
ripped off your turntable for those who remember turntables um you put the needle down and it goes
clunk and if there's a scratch on the record it goes
all the time so we want to do click removal and there's a pretty standard way to do that
and here's what it is so here's this song coming in with clicks every once in a while
and the problem is that the magnitude of the click is not always so much bigger than the
magnitude of the music
so let me make sure i'm getting this right what we do is
we differentiate it take this as a function of time
take its derivative is that hard
no we have these samples discrete samples coming in at a fixed time rate
so basically the derivative is just the dis the difference from one sample to the next
multiplied by some constant factor to get it scaled to your unit of time
so it's just finding the difference between consecutive terms now what does that do to the signal
well the derivative of a sine wave is a cosine which is basically a sine so
mostly the derivative of a of a piece of music looks just like
essentially a piece of music it's the same kind of up and down squiggle but
these clicks although they're not necessarily very loud they're pretty abrupt
so when a click comes along you get this
okay so now
we pass that through a limiter we say okay anything louder than this
get rid of so now we have
still a click but much smaller and you can tune how much you're
limiting it right you can look at what the volume of the music is and adjust that
so it's as good as you can get it for this particular piece of music and then what we do is we integrate
is that hard no it's just like differentiation except you add
terms in right you keep a running sum and then what comes out is exactly your
piece of music but with the clicks a lot softer okay
so each piece of this is trivial the limiter it's looking at samples one
at a time and saying how big is it what's that number if the number is bigger than some number we
limit it to that okay the point is
i wrote this which is in principle a program this is just three trivial procedures to write and i
compose them i take the output of the differentiator and i put it into the limiter and i take the output limiter i
put it into the integrator and that's my result each of these programs works as if
it had the entire piece of music in memory right now
okay does it need the entire piece of music in memory right now no it's only looking at
two values at a time one value at a time two values at a time right it only needs
a little bit in memory right now but it doesn't make sense to say
differentiate one value it only makes sense to say differentiate a function so you wouldn't have thought
to write it this way if you were thinking about okay at
times such and such i have this number and at times such and such else i have this number and i'm going to have to
think about the local state and how much do i need and blah blah this way it's really really easy because
you've probably already written a differentiate function in fact instead of doing this in scheme you do it in
matlab or something or mathematica and these things are already written for you
and you can write a little one line click filter so
the representation of signals in time
is an example for which streams are really terrific okay see you friday
UC Berkeley