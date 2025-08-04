Transcript


okay we're on good afternoon solutions
for midterm two are online now is the time for you to compare your solutions
against the posted ones if you think we miss graded you the deadline is a week
from win 30 a week from today okay this Saturday is dim sum be there
or be square [Music] okay and we're on okay a prime is a
number greater than one whose only factors are itself in one right so up
here there's a little procedure that
embodies that definition because another way to say this is has no factors
between 2 and n minus 1 right so if I
just take all the numbers between 2 and
n minus 1 and I use filter to select the
factors of n the ones such that when you divide n by this candidate factor you
get 0 then I just want to know is the result of that filter empty if so N is a
prime right so just to show you range
we just construct a list of all the integers between first argument and
second argument and so now if I say is 6
prime it says false his seventh I'm true
was a thousand prime false that's pretty
good [Music]
starting to slow down a little bit I've had a million so he went Asian fault
great so how about you guys is a million
Prime know that took you you know a nanosecond and that's because you're a
little smarter than this program because this program first constructs a list of
length nine hundred ninety nine thousand nine hundred ninety eight of all the
numbers from two to nine nine nine nine nine nine and probably it was in the
process of doing that that it died but supposing it could construct such a list it then finds all the factors of a
million so to 5 10 20 50 100 etc finds
all of those and then it says oh did I find any yes I did well because that isn't very efficient
and for large numbers doesn't even work
we usually do it this way so first of
all let me convince you that this actually does work is six of prime nope
seven prime yes
there's a million prime know instantly see just the same as you it does the same thing you did you said wait a
million is divisible by two I'm finished and that's what this procedure does it
has an iterative loop right up here it or either has factor as an argument it
should be called candidate factor and it's a three way cond
it says if factor is equal to n so we've
tried everything from 2 up to n minus 1 none of them were factors so return true
its Prime and yes I could have stopped at the square root of n but I'm just leaving out complexities like that for
the moment so if we're not up to n then
we say what happens when I take the remainder of dividing in by factor what
do I get is it 0 or not if it's 0 then factor is a factor of N and therefore n
is not prime and I return false and if neither of those things is true I
iterate with factor plus 1 ok any
questions about how this works great yes
Oh
what would the order of growth in time be if I use the square root of n as the
limit it would be the square root of n all right and where is this way it takes
in linear time yeah remainder is a constant time
operation for our purposes it's not true if we're dealing with very very large numbers but ordinarily it is now this
isn't magic so if I ask it for a big
number that doesn't have any obvious factors then it's still gonna take a long time before it gives us an answer
and you know in particular if the answer is true it is prime and it you have to
check every possibility up to the end but I don't know any way to avoid that you have to I mean you can be smart by
stopping at square root of n but basically you have to try all the factors up to there to make sure you
know that this isn't the square of four digit prime that you've never heard of
you know so but for large numbers that do have small factors which is most of
them it works very quickly but I don't
like this procedure that procedure I think it's ugly I think you have to look
at it a little and sort of scratch your head a little in order to know what it
does if it if it were called mystery instead of prime question mark I think
it would take I mean not forever but a little while to work out what this thing is testing for whereas whoops whereas
this one I claim is very easy to read
supposing you understand what range does says okay two to n minus one
filter to keep the factors of n there aren't any oh yeah that's what a prime
number is it's something that doesn't have any factors between 2 and n minus 1
so what I would like is to have my cake and eat it too
abafar before I forget sorry this week we are jumping ahead a little
in the book in case you didn't notice that where I'm up to an electro notes is
page 340 on the book we're doing section 3.5 we are gonna do three point four a
couple of weeks from now the reason for doing things out of order isn't just to confuse you it's because the stuff that
we're doing starting today you need for project four whereas section three point
four you don't need for project four are you looking me like that am I wrong
so what oh that's right it's it's the
meta-circular evaluator stuff that you so it's next week that you need for project four we have to get there well
we need this for is what we're actually not doing right which is yeah okay so I
never mind I'm wrong about project four but we are doing things out of order there's a reason for it we worked it all
out it makes perfect sense trust me yes no no well I mean
no it's week 11 in my lecture notes but
if you look in the little reader where the actual homework assignments are it's
week 10 okay so it's only with respect to the textbook that we're jumping
around sorry yeah sorry for the confusion okay so back to computer
science I want to have my cake and eat it too and in order to do that
I'm gonna do this so let's see if it works is 6a Prime yeah what just
happened wait let's try that again is six of
prime know is seven prime yes is a
million prime know when he tells me so right away let's try a million in three
again it's not magic it has to try all those possibilities so it's gonna take a
while but I believe that it's not gonna crash we'll see I'm right it could be
wrong nope didn't crash and it tells me that three is prime okay so here's the
program if I compare that with the
original prime question mark in the bottom half of the screen stream that
screen it's the same almost
so this says now this says stream no
this says filter it says stream filter
this says range and this says stream
range but otherwise it's the same program logic it's make a list of all
the numbers from 2 to n minus 1 use
filter to select the ones that are factors of n and then usually ask the
question is that empty are not empty okay so the code
that we're running which is this code right here it has the structure of the
definition of a prime it doesn't have that ugly let's add another variable X and and have an iterative loop and
conditions it just says 210 minus 1 which ones are
factors of n none of them its prime okay and yet it has the running time of that
other version I showed you that does have the Luke okay so this is having my
cake and eating it too and the question is what's this stream business that
allows me to make this work well
remember that range from 4 to 7 whoops
ooh oh it's predefined okay wait that's
right because my first thing crashed so I started over again okay oops
all right so range from 4 to 7 is the
list of all the numbers from 4 to 7
stream range from four to seven abstractly it's the same thing it's the
integers between four and seven but that's not how it's represented in the computer so what we have is an
abstraction
so abstractly we're talking about sequences okay so we know how to do that
with lists
we know how to do with vectors and we're
learning now about a third way to represent the same abstraction and this
is called streams and let me do a bigger
version of that picture that you can see when I say range from 4 to 7
it starts out looking like the list it's a pair whose car is the first element of
the sequence but what's new is what's in the cutter instead of being you know
more spine pairs what we have is a promise this wiggly thing is called the
promise and what it's promising to do is range 5 7 okay now I understand that you
understand that there's a lot of missing details in here and you get suspicious when something looks Wiggly like that
and rightly so but just taking abstractly you get the idea first
element a promise to compute the rest of the elements later ok that's what a
stream is now why does that help well
I want to know if a million is prime so
I start by computing stream range from
two to nine nine nine nine nine nine
okay what's that it's this pair stream
range three to nine nine nine nine nine nine okay and that's what range
what stream range returns so no matter how big this number is it only makes one
pair and so it returns it in constant time now if I were to cash in this
promise then we would do more computation I could keep cashing in
promises a million minus two times but that's not what I do next the next thing
I do is call filter I say filter a
question mark
say oh because I'm an idiot thank you and anyway why didn't it say
stream stream filter is what I mean the reason there's a question mark cuz
I'm about to write a predicate right here and I'm getting ahead of myself so so the question is does X divide a
million this thing well what does filter
do it goes through elements one by one looking for ones that match right so
what's filter going to return well first of all is this to divide a million yes
it does so I'm gonna get two plus a
promise to filter the rest of that
stream later okay so stream filter returns this stream
with two and this promise to do more filtering and it does that in constant
time right well what do I do with the
result from stream filter I ask is it empty well is it empty no it's got two
in it that's it I'm finished okay so if
the number I'm testing has a small factor like two then I never cash in
this promise and therefore I never cash in this promise and so that's why this
program is able to run fast even though what it looks like it's doing is very
time consuming okay so what we've accomplished here is something very very
important which is a separation of the form of a program from
the actual sequence of events that it generates okay for most of the history
of programming you wrote down first do this then do this then do this then do this and the computer did this this this
and this and that was it okay nothing works like that anymore at
many levels so processors one of the
ways they make processors fast these days is that the processors do
predictive running of your program like for example you have a if-then-else the
processor sort of guesses which way the test is going to go and starts doing one
of the two branches while it's still doing the test that's how modern
computers work so things happen out of order and in order to make that possible
the processor has to think hard about is it okay that I'm doing this before that
or am I gonna you know mess up something by doing it so modern processors are
very very complicated you're going to learn all about it in 61c all you need to know for now is that the tight
coupling between what the program says it does and what it actually does is in
many ways a thing of the past okay so parallelism the multi-core thing
where you might have more than one processor in your computer if you bought your computer in the last few years it
has at least two processors in it maybe four and a clever scheme interpreter if
we're calling a function with two arguments or four arguments will farm
out to the different cores the sub processors the evaluation of the
argument expressions okay so they kind of all happen at once yeah
is st kidding one of those no of course not um now listen a year ago I was
typing into a ASCII text terminal you know connected over a serial line to you
yeah
a stream filter is just for streams okay
yeah you have to make up your mind I will we could have a only slightly more
complicated abstraction where you would be allowed to have either streams or
lists underneath the abstraction barrier that isn't hard but we didn't do it yes yes the stream is the pair it's the
whole thing because because to is part of this stream right what are the factors of a million the first one is 2
so this is definitely part of this dream ok this is part of it also yes ah what's
the datatype of a promise yes actually it is a new abstract data type which
we're going to implement shortly yes
oh so what is stream filter do if 2 is
not a factor right so stream filter we're gonna look at the code in just a second sort of keeps going until either
it finds something that does satisfy the predicate or it reaches the end of the
input stream so that's why crime question mark of a million three doesn't
immediately return something because filter never does find a factor so it
has to keep trying all the way to the end sorry
stream no a stream null is definitely only called once that's right yeah okay
let me move on I think it'll help okay
so how do we make this abstraction work
so the basic interface for lists is cons
car and cutter right and then on top of car encoder you can write other things
like list and append and all that but basically car encoder same is true for
streams car encoder except it's con stream stream car and stream coder okay
let's go ahead and implement those well
let's look at the definition of stream range right here this stream range says
if from is greater than two then we're finished return the empty stream
otherwise cons-stream from recursive call to stream range
right so if it didn't have the word stream in there we'll be clear how that
works right so range from four to seven is cons four on to range from five to
seven okay now if we actually did this recursive call then stream range would
take theta of n time just like range so
somehow a rather it has to be that we're preventing this recursive call from
happening before we do the cons Inc all
right for ordinary scheme procedures remember the actual argument expressions
are evaluated before we call the procedure so if con stream were a regular old
scheme procedure this recursive call to stream range would be evaluated we would
call stream range recursively before we even know that it's a stream we're putting together you know we before we
knew that we were dealing with streams so it has to be that that doesn't happen
and in fact it doesn't what happens is
Kasturi maybe is a special form that
turns into cons a delay B now what is
this girdling con stream is not built
into scheme it's something that we provide that you know the book invents
and you know we have in our startup file delay however is a genuine scheme
feature it - for the same reason must be a special form right because the whole
point is we want to not evaluate B yet delay is what makes promises it's the
constructor for promises that make sense so how does the Leie work I hear you ask
well there's actually a very simple possible implementation of delay now
scheme provides delay as a special form but let's suppose for a moment that it didn't we can treat delay expression as
an abbreviation for lambda no arguments
expression right because when you make a
procedure with lambda is the procedure body evaluated no it's not evaluated
until you call the procedure right good
so this does the job it turns out this does even better at doing the job then
that makes it sound and here's why I've been hand waving a little when I
write down numbers like three and nine nine nine nine nine in this promise
because what really is in the promise is this stream range plus from one to the
thing that's highlighted up there okay that's really what's in the promise so
how does this actually work well
if i delay this expression I get this lambda expression right that's what that
means and now what happens when I evaluate that I get a procedure with no
formal parameters the body is stream
range blah blah blah and what about its environment well it points to a frame in
which from is to and to tio is nine nine
nine nine nine nine right so the plus from one in the body
when we do get around to cashing in this promise if ever from is to plus from one
is three okay so a promise like a
procedure has to remember what variables
it's talking about because we may catch that in in some totally different
environment right where they're either there may not be any from or two at all
or there might be completely different numbers because we can hold off on cashing that promise in as late as we
want and meanwhile we're doing some other calculation that as you know from equals a thousand or something and then
I cashed this promise in from a better be to so that the promise really is
three two nine nine nine nine nine nine okay isn't it beautiful how Lim that
just does all that really nice okay so
that's how we make streams
well stream car is just car stream
cutter of s is force could er of s so
cutter of s isn't the rest of the sequence it's a promise
to get the rest of the sequence so if I actually ask for the stream cutter that's when we actually cash in the
promise and that's what force does force is the opposite of delay well if
promises are just procedures so if delay is just lambda of no
arguments I can define the force of a
promise to be open paren promise closed
paren okay people who don't like to think about
what parentheses actually mean you'd better this is not the same as just
saying promise this is saying promise is a procedure I am invoking it with no
arguments and that's how you cash in a promise that you made with lambda okay
yes why do we have a force pretty want
to we just do this promises are an abstract data type why do we ever have
selectors and constructors for abstract data types there's actually another
answer which is that I'm a little bit about the implementation what we really do will see later is a
little bit more complicated than this for efficiency reasons yes can you screw
up the lambda by using set bang sure the set bang has to have access to this
frame so it has to be done from somewhere that has access to that frame
lexically you know inside the place where from and to were defined unless
your promise has free variables in it remember free variable is it's something
that isn't given a value inside this lambda expression so in effect it means
global variables so if your promise refers to some global variable if
instead of saying plus from one I said plus free Baz one where frivolity find
at the scheme prompt then yeah in between making the promise and cashing
it in I could change the value of that global variable and that would change what it is that I'm promising to do so
this is the tip of an iceberg and the
iceberg is rearranging the sequence of events in a program which is what we're
doing here right we're pretending things happen in one order well we may call the
2 to n minus 1 and then we check for all the factors and then we say did we find
any and what's really happening is a different order of events rearranging
the order like that doesn't work very well if you're doing mutation that's correct so this is a technique for
functional programming okay I have to
rush get where I want to be
that whoops parentheses oh yeah right
of course that doesn't work I'm trying to use ones to define ones I the first
thing that happens is cons one ones and there is no ones but here's what I
should have said ah stop that
on stream one ones it worked
how's that possible well because cons-stream doesn't
actually evaluate its second input yet
now what happens when I cash in that promise oh now ones is defined so I can say
stream car of ones and of course that's just one I can also say stream car of
stream cooter of ones that's one also in
fact I can say show stream ones show
stream is a little helper procedure to let you see what you're doing here it's
an infinite data structure it has infinitely many ones yes why doesn't it
gone forever shows it does go on forever show stream stops after a certain number
of elements okay that dot dot dot is actually in the text of show stream it
says quote dot that thought you can say whether way show stream is abbreviated
SS and you can give it a second argument if you want for how many terms to go
before it stops right obviously if I just showed all of them you know
wouldn't work wouldn't work very well okay let me just draw an environment
diagram in case you're totally at a loss here oops
ones is the result of calling Kahn
stream so it's a pair whose car is one
and whose cutter we now know what a promise is it's a procedure with no
formal parameters and the body is just once that's it when I cash in the
promise I look up ones in this environment I find it it's this pair so I keep getting this pair over and over
again okay but wait there's more
there you are all the integers inside this little box all the integers there
they are how does that work well the first one is 1 and to find all the other
ones I add one to the previous element
alright because they shift over then you line them up that Kahn stream one kind
of moves things over by one in turns the adding I'm not going to do that in huge
detail right now because in the book and we need to move on to the world's greatest example which we're not there
yet now that I have all the integers I can say things like show stream
let's have all the even integers okay now nice alright now what we're working
up toward is all the prime numbers and
to do that we're going to use something called the sieve of eratosthenes who's
seen the sieve ameritapanese before not enough of you everybody go back and
complain to your high school here's how this Eratosthenes works we
take we start by writing down all the integers leaving out one so this is
going to take me a moment
there they are all the integers okay now your service of Eratosthenes works you
take the first number that's available and you draw a circle around it that
means its Prime now you cross out all its multiples
okay iterate first number circle it it's
prime cross out all its multiples
I'm okay
etc everything else it turns out up here is prime okay that's the sort of Eratosthenes
so this says given a stream like all
those integers over there circle the
first one there's to say include the first one in the result so I can stream
that first one onto then what I take stream Qatar which is everything
after that one that I just circled I cross out all the multiples of stream
car so I keep all the non multiples of stream car and then I sieve that that's
the program
you know the class before this one is a chemistry class and I'm always really
envious because they get to blow things up and make things different colors you
know and pull coins out of their students years and all that I never get
to do any of that stuff except for this lecture
isn't that amazing all the prime numbers in this little box
and once we have all the prime numbers we can start doing cryptography and you know all those exciting things that
people do with prime numbers and there they are all right before your eyes really amazing the abstraction that we
have where the abstraction diagram it's behind something but up above the abstraction barrier we have infinite
lists and not just trivial infinite lists like 1 1 1 1 1 you could make you
know by set covering something interesting infinite lists like all the
prime numbers below the abstraction barrier what we have is reordering of events in
time we have a program that looks as if it's doing one thing so if you read that
sieve program it says start with all the integers except one now my result is
going to be Kahn stream the first one two on two recursive call for all the
odd ones the non multiples of two what does the recursive call do it takes
three concentrating three look it looks as if it's making all the integers and
doing just what I was doing over there forever it really isn't it's doing something you
know much more mundane if you look at the sequence of events but the sequence of events is hideous the result is
beautiful okay so you whenever a day comes next Friday
UC Berkeley