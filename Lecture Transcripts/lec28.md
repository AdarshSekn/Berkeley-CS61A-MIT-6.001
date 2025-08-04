Transcript


okay good afternoon
let's go now you guys aren't as much fun as the fifth graders you're not in costume okay up on the screen is where
we left off last time with this beautiful example of all the prime numbers inside your computer and I want
to look more closely at this business of infinite streams and start by saying
number when I first did that prime question mark example I define a little helper function called range it looks
like that and then we just made a tiny change to it that's all basically I
changed cons to constraint and yet that
tiny little change makes an enormous difference in the way the program runs
right in the order of events that happens in the computer if you're trying
to trace through the program and if you
don't understand how Kahn stream works you're gonna get a completely wrong idea
of the order in which things happen but that's okay as long as you're doing
functional programming because although you're completely wrong idea isn't the
truth about the sequence of events it gives you the same answer as what really
happens and in functional programming we only care about the answer we don't really care about the intermediate steps
because something that happens in this step isn't going to affect something that happens in that step and then we
can make what looks like a huge change in the program namely this
we can make it a procedure with no base case and it still works in fact I don't
even need the variable 2 anymore I can say define its from from to be kind
stream from it's from plus from 1 and
then I can say show stream for example and it's from 27 and I get the infinite
stream of integers starting from 27 and Counting up so inform what we have here
is a recursion with no base case
something a little bit like this but not quite so dramatic happened when we did
tree recursion when I wrote tree map and there was what looked like a recursive
call but it wasn't a direct recursive
call that wasn't tree map calling tree map recursively it was tree map calling
regular old map with a function that had tree map in at lambda of child tree map
bah-bah-bah and because of that instead of one recursive invocation
we got a variable number 0 through however many you want however many
children in this node has recursive calls so that's a program arrangement in
which the sequence of events is not directly obvious by reading the code you
have to think hard about it but if you forget about the sequence of events and just think about what answer am i
getting it's much much easier to understand treemap and the same thing is true here
never mind the sequence of events oh this says it's from 27 is the same as
Kahn stream 27 its from 28 and that's true right if you want to make the
infinite set of all the integers starting from 27 that's 27 plus all the
integers starting from 28 and so our program gets the right answer and we
don't have to sit and think about wait a minute what possible sequence of events can there be to make this work
because it's a recursion with no base case is it a recursion with no base case
well obviously not exactly what really happens is Kahn stream is a special form
it doesn't evaluate that second argument the recursive is a so-called recursive
call and so that call doesn't happen until we force the promise by saying
stream cutter of this dream every time we say force by saying stream cutter
which does it for us we move one step along in the computation and then we
find that under constraint so what would be the second step is not forced at this
moment but is waiting as a promise for another stream cutter to happen sorry
I'm deathly ill okay so a beautiful
thing a recursion with at a base case and it works because of this funny way of thinking about things I wanted also
to go through this business of implicit
definition of streams and look at how we got this value for integers because that's something that people find
confusing so I think last time I
convinced you that one's which room it by saying Kahn
stream one ones is an infinite stream of
ones right well what about integers well
we know what the first number in integers is because the definition says Kahn stream one something or other so
here's a one and for reasons that will
become apparent in a moment I'm gonna write down integers again starting one
space to the left cuz what's the second number in integers well it's the stream
car of 1 plus the stream car of integers that's two Oh what's the third number in
integers it's the second one plus the second integer what's the fourth number
in integers it's the third one plus the third integer so we come up with the
integers on a sort of just-in-time basis it's like being a Japanese car manufacturer we we construct integers
just in time for the next plus to happen okay
any questions about that
so again as with trees the right way to
think about this stuff is you spend a little bit of time carefully tracing
through things the way I just did to convince yourself that programming in
this style can work at all and then once you've convinced yourself you don't do
any tracing at all you say okay suppose I have the infinite set of ones and the
infinite set of integers and I write them down one underneath the other and I add them up what do I get
the answer is I get 2 3 4 5 etc and if I can stream a 1 in front of that I have
the integers okay so you think about it
pretending that you really do create all of them at once ya know the question is
about how stream map works do you remember how plain old map works it says
plus call the function on the car and then a recursive call for the to map for
the cutters it's the same here so I'm taking advantage of a feature that's in map also which is that you can actually
have more than one data list argument
you can give map let's say for argument's all together a function and three lists and then the function should
take three arguments and we take all the cars and we give those to the function
and then we take all the catters give those to the function and so on yeah right each recursive call to map
makes one call to plus with car of its
argument what with car of all of its arguments okay now all of its arguments are going
to be first the entire stream and then next recursive call that'll be the
cutters of the entire streams the stream cutters so in each recursive call to
we call stream coder on all the stream arguments and that gives us one more
value okay and then we use those values calling whatever the function is in this
case plus plus is nice because it takes any number of arguments so we can do
tricks like this easily you don't need a special plus with two arguments or a
special map with two arguments it all just works okay other questions all
right so a reminder as somebody said last time if you do mutation in the
functions that generated streams defense generate streams peculiar things will
happen but you won't like and there's
some homework exercises in which you do that on purpose to see what happens try
to figure out what happens and the whole point of those homework exercises is to convince you never to try it again
the only use streams with functional
programs yeah
what are the advantages and disadvantages of streams versus local state thank you that's a great question
to put that question in another way why are streams in Chapter three right
because chapter 3 is about mutation but even before that chapter 3 is about
modeling inside the computer a system that changes over time and one way to
model a system that changes over time is it is object-oriented programming with local state variables and methods that
you know that set bang them right this is another way and let me show you how
that works
okay show stream just to make an
interesting stream map and 2x times X X
user stream okay so I type all that and
I hope I typed enough closed parenthesis yeah I did and it sits there and I type
a number like 10 interesting still sits
there did I do something wrong
nope huh why didn't that work I think
that should have worked Oh because I'm an idiot
oops Oh maybe they're not gonna come out and to like finish everything
oh oh look at that
uh-huh okay thank you let's try this again
so it comes of making up examples on the fly
ah interesting okay so nothing printed out
until sorry whoops
yeah I needed write ten things to get it to come out I was hoping they would print a little at a time but they didn't
if I just say go string use your stream
let's see what this does
yeah oh well anyway you get the idea which is the user stream procedure
returns the stream of everything that the user is going to type from now on
okay well now suppose we we want to
represent your bank account so I'm going to say define my account and I'm going
to start with a hundred dollar initial deposit
okay so I have $100 deposit and I'm going to deposit $1,000 then I withdraw
$100 then I deposit $10 then I withdraw
$7 then I deposit another thousand dollars
okay so the stream my account is the
stream of all the balances that my account is ever going to have from now
to infinity and we can write programs using it as if we had it all at once so
for example when I defined my account up here I'm assuming that I have all of
user stream all the deposits and withdrawals that I'm gonna make until
the end of time and I say okay the running balance on my account
is start with the initial balance and add the deposits and subtract the
withdrawals it's a deposit is a positive number of withdrawals a negative number and I add
those things in and that gives me my entire bank account for all time so you
see that this is a way of modeling time varying state functionally I can do
functional programming with this thing so here's another example
oops Wow
that's what I meant okay so this is an infinite stream of
random digits and if I want to do some
program that involves randomness instead of going through it step-by-step instead
of asking for one random number each time I can take missus given and of
course the programming that makes random stream work is not exactly really functional if you look inside because
random isn't but random stream is
because I'm only going to call it one so I'm gonna say define random digits to be
random stream call random stream and now
I can I hope just show some random
digits so if I do that again I get the
same set of random numbers so this infinite stream from now on if I just
take it as something I set up at the beginning of the program it's always the
same value and I can use this value in a program that says take all these random
numbers and do something or other with each one calling map you know in a way that uses random stream okay so yeah why
do I you have to call well I'm not exactly calling a stream thank you for asking what I'm doing is writing a
procedure whose output is this stream and the reason I have to do it that way
is if I just define if I said well let's
do it define friends Conn stream random ten brands like that
okay what am I going to get
okay midterm three question what am I going to get
yes yeah
yeah I'm going to get one random number repeated infinitely many times because
it's the same thing I did with ones it's con stream a particular value onto this
same stream whereas when I write a procedure if you compare that with this
definition every time I cash in a stream
cutter I'm calling random stream again and so
I'm calling random again okay and the same is true with user stream I have to
keep calling read otherwise I'll just read one number and get that over and over again okay so it's sort of the
price I have to pay for introducing non-functional elements underneath the table yeah oh why did we end in
it's gonna be the same stream every time if it doesn't exactly if I call well if
I call random stream over and over I get
different ones but I said define random
digits and then I call random stream
okay so now that fixes my first one it kind of tethers the whole thing so I'm
having one particular set of calls to random so if I show stream random digits
so to do that again I'm not calling random stream again I'm
just Reedus playing the same variable random digits that contains the call the random stream
I've already made yeah oh yeah good
point you're absolutely right I've forgotten to teach you something which is I lied
about how it works I told you that
stream car is just car which is true and then I said yeah when we call stream
cooter we just take the cutter which is a promise and force it but really what
we do is that the first time we call
stream cutter of a particular pair we remember the value that we got and
that's done for efficiency reasons suppose that we're computing some stream that's computationally expensive we
don't want to recompute the same value remember um way back at the beginning of
the semester we talked about applicative versus normal order scheme uses applicative order and we looked at the
case x x ax and then we you know define square x times X X and what if you call
square of something that's computationally expensive in applicative order you only compute the argument
value once and in normal order at least
in naive normal order you have to compute twice well we avoid that using
memoization because now we know a way to avoid it which is this idea of memoization right and by using
memoization we can have the reordering effects of normal order and we also have
the efficiency of only computing things once right okay so what he's saying is I
don't have to write memorise right there instead what I do and you're absolutely right is the definition of force does
the memoization okay so when you call force of a promise and in SDK you can
actually see that because you get you know number sign promise blah blah blah
or number sign forced promise value you know so it shows you that it remembers
whether you've done the forcing or not somebody over there you gave up you know
answered it okay yes you're next
okay question is if I only want my current bank account balance why do I
need the stream of all my future balances and again the answer is
functional programming has all these wonderful properties that you can reorder things to your heart's content
you can paralyze things and everything still works whereas we're gonna shortly
look at some of the complexities that come up when you try reordering things or parallelizing things that do mutation
so this is a way to have our cake and eat it too the problem with functional
programming is that it doesn't have any sense of time in it it tells you the
answer to some question okay well if what you want to know is your bank
balance right now I can't exactly say that in functional language because
there's no notion of right now in functional programming I only get that when I have sort of a sequence of steps
and I go through and I change the balance and now I can say okay what's the balance after that change but if I
have all your balances from now on until forever then I'm back in the world of
functional programming I can do computation for instance I can say suppose this account is a savings
account alright so it gets such as such percent interest compounded monthly or
daily or however often it is I can write a little program that takes user stream
and the initial value computes the value by adding in the deposits and then
computes the value plus interest compounded and I can do that
functionally I can say map a function
that takes this value multiplies it by 1.001 or whatever it is and that's the
next value and I can apply that function to I can interleave that with your
deposits and withdrawals I have to in order to get it exactly right after new something a little more complicated which is keep
for each deposit and withdrawal the timestamp so I know when to do the
interest calculation relative to all the other things that are going on but again
the the sort of one sentence point of all that is that I can model something
that changes over time namely your account balance and still do functional programming because if you kind of
squint your eyes and forget about the impossibility of it and say okay here I
can predict the future here's the stream of all your account balances every minute from now till the end of time
okay well now I can do functional programming on that because that's a something that doesn't change over time
right your instantaneous balance does change over time but the whole trajectory doesn't it's a little bit
like the relativistic view of
trajectories where instead of having three dimensions and a snapshot where
here's the ball I'm throwing and here's where it is now here's where it is now here's what is now history is now
instead of that we have a four dimensional plot of a graph and that graph represents the entire trajectory
of the ball all right so you do that in physics 7c I guess and we're doing
something like that with your bank balance okay because for the same reason it simplifies the thinking about it in
doing further calculations there was a hand up yeah
yeah yes question is didn't we have to
change delay and not just change force well sort of what we're gonna do is
delay will produce a data structure that
has a true or false flag has this been forced yet and then either the function
of no arguments that computes the promise or the value that we got right
yes right ah how did we implement constant
if it's not part of standard scheme we used macros a feature of scheme that we
don't really get into in this class but you're welcome to read up about essentially it's a way of saying I'm
defining this thing to be a syntactic keyword the same as Khan does this in fact a keyword or lambda as the site's
it syntactic keyword and when you see an expression that starts with this key word we basically call a function that
turns it into a different expression and then we evaluate that so we just turn
country maybe in to cause a delay B and then evaluate that okay and that's
something the scheme lets you do just for situations like this other questions yes
oh right memorize verses random digits other
thing we're looking at up on the screen remember what show stream does it takes
the stream that you give it starting from the beginning of the stream that you give it and it keeps calling stream
cutter ten times or however many times you tell it or until it runs out and
then call stream car to get the values in those pairs well if delay didn't memo eyes then
calling stream cutter again would
computer new random number so really technically if we didn't memorize I'm pretty sure this is true
what I would get is the first element of random digits would be the same every
time but all the other ones would be different because I would call random
stream again and that means I call random again but because of memoization
once I've forced once I forced the
promises in the first pair and the second pair and the third pair and so on those promises remember the value that I
got so the second time I call show stream it says ok give me stream could
er of this stream and the promise says oh yeah I've already been forced and the value I
got was the stream six six three okay and similarly the next one says oh yeah
I have this dream six three eight blah blah blah and so on okay yeah
right since they're not forced in the sense I'm the homework problems that you're going to do about this actually
put a print in the function that you
call in the coder of the stream and the promises that we're making and so it
prints out the first time you force that promise and not afterwards and so when
you do those exercises you'll see how it plays out okay yes
when you force a procedure promise not when you delay it we delay it it just
sets up the data structure with the flag so that it can tell it's force that checks is this the first time I'm
forcing this promise or is it you know have I already forced it does that clarify you're right I interrupted you
in the middle is that answer what you wanted answered if not ask it again when
you delay you don't delay I mean you could delay procedure but you can delay any expression you want when you delay
the expression it makes it an abstract data type called a promise and the
pieces of the promise are lambda of no arguments your expression so that
remembers what expression you're trying to delay and also remembers the context
in which you're doing the delaying so we know the values of variables right and the other thing that's in that promise
data structure is a value that starts out as false and later becomes true that
says have I been forced yet and the first time you force that promise it
makes a new data structure where the flag is now true and instead of the land
of no arguments expression what we remember is the value that we got the first time we forced it okay yeah the
code for how promises are memorized is in the books you can read all the
details there but that's the essence of it thank you just what I wanted to know
okay what happened I said
oh yeah so delaying stuff lets us build these
cool infinite data structures and it's efficient because of memoization so why
doesn't scheme just use normal order let's go back to that question we asked in week one and the answer back in week
one before we learned about memoization was that it would be inefficient because we'd have to recompute things but now we
see that we can memorize expressions so why doesn't scheme just use normal order
now let's not always see the same answer yes yeah
memory usage good answer because we have to remember all those values that we forced but no there's a there's a yeah I
know that we it's true that we have a lot of things sitting around memory and you have to be careful about that but
there's an even better answer than that yes yes scheme is a language that tries
to support multiple programming paradigms so as you've seen we can do
functional programming in scheme but we can also do object-oriented programming and scheme which involves mutation if we
did normal order mutation would not work very well because we would make a
promise we would change the value of some variable that that promise needs to
use then we would cash in the promise and get the wrong answer okay so once
you're allowing mutation you're stuck with applicative order but there are
languages in the world that are purely functional programming languages a
couple of the well-known ones are ml and Haskell or two purely functional
languages there is no mutation operation and indeed those used normal order and
so plain old lists can be infinitely long you don't have to say stream you
know to invoke this special thing we invented you just comes that way so if you do if you have a purely functional
language then it makes sense to have it be normal order but if you're going to
have a mixed-mode language that lets you
do functional and non functional programming then you'd better use applicative order or else people are
going to be surprised by the results of reorderings they weren't expecting all
right so this is this is all stuff to keep in the back of your mind when
you're thinking about the question of why is there more than one programming
language you know why isn't everybody figured out already that scheme is the
best one and get rid of all the other ones you're supposed to laugh yeah and
one of the aunt well one of the answers to that is that some people aren't very smart but another answer is that there's
more than one way to program and different language and all the languages
are equivalent in the sense that if you can write a program in one language you can write it somehow or other in any of
the other languages I mean it's possible to design languages that aren't that powerful but every programming language
you've heard of is equivalent in what computations it can do to every other
language but some things are easier in
some languages than others because they promote particular styles of programming and that's why there's still room in the
world for different languages ok at least that's one answer to why there's a little different languages and
it hasn't all shake it out yet and by the way sometimes the reasons they're
big you know powerful idea programming language things like normal order
evaluation or funk programming and sometimes they're a little you know good at handling UNIX
file system files or good at drawing
animations with multiple characters up on the screen or that kind of thing where there's some interface to the real
world that they did a good job of in a particular language and that's why people use it not anyway okay I'm
varying information and did that infinite streams did that memorization did that reordering did that okay any
more questions last chance I don't see any okay have a
good weekend
UC Berkeley