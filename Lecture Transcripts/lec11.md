Transcript


okay good afternoon um midterm Wednesday review session
Sunday um I think that's all under control what we're doing today is looking at an example program which is a
little four function calculator um and we're looking at this
program for two reasons um says up on the board first is it's an example of
processing deep lists that is lists of lists of list lists um because in this
calculator program um I can say plus time 3
4 Time 5 + 6 7 as deep as I want to
go and it'll figure out the answer so if you look at that expression as a scheme
expression it's you know it's not it's exactly like what you've seen before but now I want you to look at it as data and
it's a list list of lists of lists in some cases okay so we are looking at how
to handle such a situation and
um great t-shirt
um also down the road we're going to be
um looking at a scheme interpreter written in scheme and uh traditionally
this has been a big obstacle for students it's sort of all of a sudden we're looking at this big complicated
program and so we now build up to it in Little Steps and this is our first little step um so unlike an actual
scheme interpreter this one has no variables um no procedures as first
class things in fact it only has four procedures you can call Al together plus
minus times and divide um but it's schem like in its notation so you say you know
plus 6 7 you don't say 6 plus 7 um and it does composition of functions in
exactly the way that scheme does so although this is very very very
simplified um most aspects of it are pretty realistic and the big overarching
picture that I want you to get is up on the third board it's that there are three pieces to an interpreter it has a
y in parenthesis there because it's any interpreter not just a scheme interpreter basically any interpreter
for any language is going to have pretty much the structure that you're about to see and there are three parts to it um
the first one is a very simple part it is
this um the re valve print Loop um if you're a lisp person you say
reppel and everybody knows what you mean you mean this um it's a loop because the last thing in
it is a tail call to itself so this runs forever um and it's a read Val print
Loop because of this line um and remember that things in in
scheme happen kind of inside out so when scheme sees this first it calls the read
procedure and the job of Reed is to turn things with parentheses
into basically box and pointer diagrams into pairs
um so the read procedure gets um this
example like this as just a string of characters and it looks at them and says
oh this is an open parenthesis that means this person is starting a list and so on and it creates the box and pointer
diagram the same as you should be able to do and then the result of read is
given to eval um it's actually called Cal eval uh so that it doesn't get
confused with eval that's an actual STK primitive um so this is Cal eval but it's the
evaluator the core of the evaluator um and it takes an expression as its
argument and what it returns is the value of that expression and what do we do with that
value we print it we call Print um so that's why you actually see
a 77 there so read read the expression that you typed eval calculated the 77
and then print printed 77 okay um so questions about the
reppel great easy right this is the easy part
eval is not so bad either it's pretty small it's small partly because of the
restrictions on what kind of expression we can have so in scheme um there are basically
four kinds of expressions and they are self-
evaluating which are things like numbers and booleans right you type in number
sign T um its value is number sign t uh you
type in 23 its value is 23 those are self- evaluating
um which we have in the calculator namely numbers there are variables which
we don't have in the calculator so that's a complexity left
out there are uh function calls which we
have they're limited to four functions but they're there and there are special forms which
we don't have and when we look at an actual scheme interpreter we'll see that a lot of the complexity goes into the
special forms in eval um so this eval is just a three-way
con Clause if the expression is a
number then we return X which is the expression so the expression is its own
value that's why it's called self- evaluating um if it's a
list then it's a procedure call that's what a list means call a
procedure and we're going to call Cal apply which I'll talk about in a second
to actually apply that function to arguments if it's anything other than a number or a list it's a bad expression
it's an error okay so every list is a procedure call because there are no special
forms um so this is a very very simple version of EV Val but something like
this is at the heart of every evaluator because what's an evaluator's job it takes the stuff that you type in and
figures out what that stuff means and that's eval job figuring out what the notation
means if we were writing an interpreter for a language like
Java EV Val's job would be way more complicated because there are a
bazillion different notations and and they're not uniform and what you can put in one context is different from what
you can put in another context and so eval is really really complicated um in
lisp interpreter um eval is much simpler partly because
one complete expression uh is one
list okay so the the form of Expressions matches the form of the data that the
language knows how to deal with so language was designed in order to be able to evaluate its own programs very
straightforwardly um and this is why lisbians say um at
the heart of every programming language there's a Lis interpreter trying to get out um because basically what you have
to do is evaluate expressions that are mostly procedure calls and a few other things and um it's just that there's a
lot of syntax in the way of doing that so here the syntax doesn't get in the way all right so we have a very simple
eval but um it's not totally simple
because right in here
there's something that is much more complicated than it might look um it's
sort of a recursive call but it isn't a recursive call exactly because there's
no open parenthesis in front of caly Val instead we're using caly Val which is
this procedure that we're in the middle of as an argument to map map is going to call caly Val
typically more than once right however many sub Expressions there are however
many arguments there are to your operator we're going to call uh caly Val
once for each of them so in this expression down at the bottom we called
caly Val on this whole thing caly Val says okay first thing I
have to do is call caly Val recursively for times 34 and also call caly Val
recursively for Time 5 + 67 now the call for times
34 has to evaluate three that's a trivial job but it has to be done we
have to recognize that this is self- evaluating and we have to recognize that four is self- evaluating we have to
recognize that five is self- evaluating and then we have to say oh look here's another list so that means another caly
Val for a function call and for that one we have to evaluate the six and the
Seven okay so that's a total of one two three
four five six seven eight nine calls to caly Val to compute the value of this
expression okay so this um call to map
here is more than just a simple recursive call it's a multi-way recursive call
and this is the secret to dealing with deep lists right here if you have a data structure that's
a list of lists of lists of lists to whatever depth you want then uh to deal
with it you have to make a recursive call for each element of the top level
list and then for each element of subl lists and so on all the way down um
so what's the base case for this kind of multi-way
recursion well it's the base case of map which is what what's the base case of
map yeah yeah empty list okay map some
function empty list just returns an empty list okay so um that's
one base casee for this process is that
um we've evaluated all the arguments the map was given you know three arguments
or something and it did a recursive call for the first one recursive call for the second one recursive call for the third
one and oops I have an empty list finished okay so that's the base case the other base case is right up
here where if the expression isn't list there's no recursion it's self-
evaluating okay so that's two kinds of Base cases the way you can think about it is
um the map base case think of as being sort of horizontal you had this expression this expression this
expression and you reach the end and the number base cases like
vertical you've done a recursion and then a recursion inside that and a recursion inside that and now we're
looking at three we don't have to do any more recursive calls but that doesn't
mean when we get to this three that doesn't mean that the whole problem is solved um I'm betting that
despite our discussion about recursive versus iterative processes a lot of you have in your head the notion that when
you reach a base case everything is finished okay that's not the case here
when you reach this base case of the three we aren't going down any further but now we have to to look at the
three's sibling the four and then we pop up and take care of the times three four and now we have to
look at a five and so there's a lot of work still to be done when we reach the three even when we reach an end of list
based case so when we've processed the three and we've processed the four and
now we come to the end of this list that's a base case for map but we still have this piece to deal with okay so
base case doesn't mean the whole job is over it just means we're not doing any more recursions down this particular
Road okay questions about that
yeah how does it know to call Cal when it
sees the plus oh thank you I messed up
Let There it knows because it's not schem it's in Cal thank you good
call
um hard day okay um
so what's the second argument to map it's cter of X and this is um we're
getting toward one of the ways well the principal way actually in which the calculator is different from a real
scheme interpreter which is we're not going to see a recursive call for car of
X car of X has to be one of the four symbols plus sign minus sign asterisk
slash and uh we're going to use that to represent the function in the call to
apply in a real scheme interpreter it could be a symbol that's
the name of a procedure but it also could be a Lambda expression or another procedure call that returns a procedure
or any all kinds of things to provide the function so we have to eval the car
also but here we're not going to we're only evaluating the elements of the cutter which are the arguments to in
this case plus um and then we're going to call Cal apply with two
arguments namely a symbol plusus SL I mean
asterisk slash right and a list of actual argument
values okay because cter exp is actual argument expressions
all right so cter exp looks like
this but map caly Val cter exp the result of that is the list
12 and whatever 5 x 13 is
65 75 something like that um no 6
so the list of two numbers which are the actual argument values so this
structure in which we recursively evaluate the arguments before we call
apply is the implementation of applicative
order got it applicative order means first you evaluate the argument
expressions and then you call the function and that's what we're doing here if we took got the call to map and
just called calply with CarX and cter X we'd be doing normal order
evaluation where we give the actual argument Expressions to the
function okay so this is a a I'm sort of obsessing on a small point but there's a
meta point that I'm making which is that by reading the code of an interpreter
you can really see the answers to the questions of you know what is the language that this interpreter
interprets and here what we're seeing is that the language is applicative order
because of this way the cal cal apply is done any questions about
that okay who's with me thumbs up thumbs
down okay so all the people who aren't is that thumbs down come on I want to see every hand up
thumbs up thumbs down every hand you
two okay a couple of sideways is but it's not too bad all right so just for the sideways people
let me say it once more and then we'll move on um there are a bunch of different
properties of a programming language that determine what it is to be a
program in that language we've looked at a bunch of properties so one of the properties of scheme is it
has first class procedures another property of scheme is
um well it's applicative order and another property of scheme is um it does
have variables and so on okay lots of different things that make scheme scheme
and every one of those things manifests itself in The Interpreter
so we can look at The Interpreter and ask questions like how would I change
this interpreter if I wanted just like scheme only normal order right and the answer is you would
not call map in here but just use C or exp as the second argument to
apply and then we would be giving apply actual argument Expressions rather than
actual argument values okay which is what normal order
means actually I'm saying this with my fingers crossed because in a real
language like scheme it's a little bit more complicated how normal order works and we are going to get to that but
basically this is applicative versus normal order right here okay so we call
apply with exactly two arguments the first argument is the
function that we want to apply apply is you know a fancy name for call
a function and the second argument to apply is a list of argument
values even if there's only one argument or no arguments it's always a
list that's so that it has a uniform definition so function arguments and in
the definition of calply down here you see that that it takes function
and arguments as its arguments
okay here's the place where the calculator program diverges from what
scheme does it's not just a simplification it's actually a difference and that is in actual scheme
interpreter it's the procedure itself because procedures in scheme are first class so that function AR
would be the procedure that adds numbers or the procedure that subtracts numbers or the
procedure Etc in this calculator we don't have procedures as first class values which
is a big simplification and so instead the first argument to apply is the symbol that
names the function we want to use so it's the plus sign or the minus sign um Etc it's a little bit like the
distinction between applicative and normal order except that instead of being about the arguments it's about the
operator the function that we're calling and uh we give the name of the
function rather than the function itself because there's no way to represent that in our calculator um in a week we're
going to look at a still somewhat simplified scheme interpreter that does
have first class procedures and you'll see how that works differently so this caly Val is actually a little more
complicated than the real one because it has a cond with five cases is this plus
is this minus is this times is this divide else error
okay so that means if I say something like um you know square root of
four I get that operator square root okay
um and that ER call to error by the way I guess we haven't explicitly talked
about this error is a scheme primitive that prints an error message and gets
you back to the scheme red valve print Loop because STK is an interpreter just like this STK
has a reppel and an Val and an apply just the same as this except for scheme
instead of for the calculator language so we really are looking at something pretty real here except for um this
business about four different con Clauses for four different
operators so um plus and times are easy we treat all the arguments the same way
um minus and divide is a little more complicated
um we can't call them with no arguments if we call them with one
argument then then we return either the additive inverse or the multiplicative
inverse of that one number so either minus car of ARS so if there's only one
argument args is still a list and the one argument is car args so here I'm
taking the additive inverse minus car args and here I'm taking the
multiplicative inverse um divide real scheme divide does the same thing so this is like saying one divided by car
RS okay um
otherwise what scheme does scheme actually allows multiple Arguments for minus and slash even though it's kind of
silly and um it treats the first one differently
from all the other ones basically so it takes the first argument minus the second argument that result minus the
third argument that result minus the fourth argument so the way I represented that here is take
everything except the first argument and add them all
up and then subtract that from the first
argument probably would have worked to let scheme handle this but I'm making explicit what the semantics the meaning
of minus and slash actually are for these funny cases where there's multiple
arguments more than two two arguments is straightforward but this handles two arguments
also okay questions
yes uh what's the point of the one or the zero in the accumulate procedure um
accumulate takes an accumulator function like times
in this example and a base case value so what's the starting point for the
accumulation so it starts with in this case one and then it multiplies that by the first
argument and multiplies that by the second argument and so on does that answer question um if you took
CS3 L you may have seen a version of accumulate that doesn't have an explicit
base case argument and instead uh you have to call it with functions it knows about basically it has a bunch of Base
cases built in
um okay any more questions about apply
yeah um yeah if I say BR star close brand
indeed I get one and that's because um if you call accumulate and
args is empty it just returns its base case
value isn't that isn't that bad no
why yeah this is what scheme does it um if you call times with no arguments it's
a slightly funny thing to do um but if you do it um the identity element is the right
thing to return um should I convince you of that is that or
you believe it it's shaking all right it won't take very long I'll convince
you oops now let's use this one it's
cleaner okay no even even better okay the value of this is 60
right okay I'm going to cross off the
five now the value is 60 ID 5 which is
12 yeah I'm going to cross off the four I'm going to get 12 / 4 which is
three right now I'm going to across off the
three so in order to behave consistently it has to return the identity on
um nobody ever calls it like that open pen star closed pen but what does happen
is people call apply multiply to a a list of arguments
that happens to be empty yeah
why not trigger an error um it's not an error mathematically ask a mathematician
any mathematician has never seen scheme before will predict that behavior
yeah oh sorry um good question but badly timed
um he's asking what's this flush here um this is
a little stupid operating system thing um every operating system
basically um when you output text to be
displayed it doesn't actually do the displaying until you output an End of
Line character so it puts up a whole line at a time in the case of a prompt we want to
print the prompt and then sit on the same line so the FL procedure says even
though I I haven't sent you an End of Line put this out anyway okay that's what it
means um yeah other
questions okay let's see what I haven't said
yet oh yeah while we're back here read and print the
pro they're primitive procedures and they're not functions they're not
functional um read is not functional because every time you call it you get
with the same arguments namely none you get a different answer right so that
doesn't satisfy definition of a function which is that your answer shouldn't depend on anything except the arguments
and print is not functional because it changes the state of the world namely it
changes what's up on your screen okay anything that does that is not functional functions just compute
and return values so even though we're doing functional programming in scheme
the scheme interpreter itself is not entirely a functional program however the guts of it eval and
apply are functional those those things all they do is they take arguments and they
return values and you can predict the return value from the arguments except
for the fact that you can Define variables okay so that's a little bit of
nonfunctionality um in evaluating expressions but these a valent apply the ones in the calculator are totally
functional because you can't Define variables so the state of the world doesn't affect what they return
um so that's an interesting little bit of trivia um read and print themselves
are slightly messy you know you have to say okay let me look at the next
character is it a quotation mark do this special thing is it a space do this special thing is it an open or close
parenthesis do these other special things and otherwise sort of accumulate characters until you get to a space or
parenthesis and then look at what you've got are they all digits and so on so
it's not um a huge intellectual leap the way you
know higher order functions probably were for you but it's messy and has a
lot of detail to it and we're not bothering to look at it we're just taking it as given because it doesn't
really repay the effort to read it but um it you could read it you could write
read and Print in scheme um given The Primitives the more primitive Primitives
um read character and print character and read and Print Work in
terms of those
um okay a little piece of vocabulary
syntax is the technical term for the form of a program what a program looks
like so scheme syntax is open parenthesis procedure argument argument
argument closed parenthesis that's what a function call looks like um semantics is what that thing
means so open parenthesis blah blah blah what that means is call this procedure with these argument values after you've
recursively evaluated the argument Expressions okay um so if you look deep
enough programming languages I was about to say all programming languages have the same semantics that's clearly not
true some programming languages for example are in normal order I mean real programming languages that people use
some of them are like that um but more or less you're going to see the
same kinds of things in the semantics of every language you're going to see some
way to make a conditional decision something like if or con you're going to
see some way to have a loop like a tail call um you're going to see some way to
call functions um you're going to see some way to define variables you know all of
those things um they're the same kinds of categories of meaning the syntax of different programming languages is very
very different from each other if you've studied another programming language you'll know that um if you took cs10
last semester uh the syntax of the language you Ed was all full of pictures
instead of text it's very very different um but you know if you studi Java and
high school or Community College or C++ or something uh that looks much more
different from scheme then the meaning is different from scheme okay so syntax
and semantics 's of vocabulary there um big important point we are here
dealing with two different programming languages okay the calculator is a
program written in scheme the language that the calculator implements is a programming language
really trivial one but a programming language that isn't scheme okay
so when I say for example that there are no variables in the calculator language
right so if I say you know Foo that's an error
um if I say plus sign now let's be clear about this if I
say plus sign in parentheses that's zero if I just say plus sign that's an error
the error message is bad expression plus sign okay that wouldn't be true in in
SDK if I say plus sign I get a value back it's a it's the addition
procedure okay so two different languages um up
here uh we have variables we have um for example here's X is a
variable so even though the calculator language doesn't have any Vari abl in it
you know if I typ type X into the calculator program error bad
expression but I can type X into STK well if I do it right now I get an error message also because the variable is
local to caly Val but um I can say caly Val that's a variable and its values of
procedure right um so two different languages two different prompts there's the St K prompt prompt which looks like
that and then there's the Cal prompt which looks like this okay these languages are different enough that I
don't think any of you is going to get confused about this point so we can't write for example an
if expression or a cond expression in calc language but we can use cond as we
do up on the screen here in scheme in defining what the calculator language is
okay I'm belaboring this probably obvious point because pretty soon we're
going to be looking at scheme interpreters written in scheme and that's going to make it a
little more confusing so I want you to get this point clear in your head while the languages look pretty different from
each other that when you have a scheme interpreter and scheme there are two
languages involved there's
STK scheme and there's my scheme interpreter scheme right and they're
going to be a little bit different from each other so we didn't Implement every single feature of of real scheme in our
interpreters um we just took you know the ones we thought were important and
um so the languages are different but they look very very very
similar and so if we allow for example cond
expressions in our scheme interpreter and if
the procedure that implements cond Expressions uses a
cond many of you are going to think the first time you see that oh wait this is cheating right how can you use con
Define con and the answer is we're not cheating at all we're using STK cond to
Define our interpreter con okay so try
and keep that straight while it's simple as preparation for um the next big
step okay and other thing about EV and apply and this is this is why I brought
up syntax versus semantics eval lives in both of these worlds in a
sense eval is the program that turns the syntax into the semantics it knows the form of a program
that you type and it turns that form into something meaningful that's a
request to compute some value okay so it takes an expression a piece of syntax as
argument and returns a value apply doesn't know anything about syntax and
this is why apply is separate a separate a whole separate thing from eval when we
think about it um
because the two arguments to apply in the real interpreter are a
procedure and argument values so it's not the notation for a
procedure it's not like Lambda blah blah blah it's a procedure and values that it takes so
it's all in the world of values its work is entirely about semantics and not about syntax so any piece of syntax
that's in the language is going to be taken care of by eval uh except for I should say the
pieces of syntax that are handled by read which is mainly the parentheses but also quotation marks
okay um oh yeah one last
thing okay yeah it doesn't isn't true here um
eval calls apply right here
right when we get to an actual scheme apply we're going to see that apply
calls eval think for a moment about why that's true back to scheme now what does it mean to call a
procedure it means compute the actual argument
values substitute the actual argument values for the formal paramet
in the body right and then
evaluate the resulting expression so when you call a procedure
a Val is going to end up calling apply so this is a Val and apply calling each other back and
forth and um that's a pretty complicated control flow if you try to draw one of
those diagrams like they did for Fibonacci numbers with trees and arrows going up and down and everything um it
gets pretty complicated ated and it needs to be complicated because of the complexity of deep lists as a form of
expression right so when you have a list of list of list of lists and so each of
the so what that is is a function call that involves function calls to complete the arguments and those things invol
more function calls and so on um you need uh this thing that's called
Mutual recursion Handler it Mutual recursion is going to be a big part of what we look at next week when we talk
talk about trees as a data type so I wanted to leave you with this sort of preview of Coming Attractions and we'll
see it uh in the scheme interpreter at the end of next week any last
questions only once ah
yes wait hang on stop okay syntax and semantics
okay um his question and it's a good question so don't be in a hurry to leave
is um why doesn't apply carabat syntax um because syntax is important in
function calls just like um semantics say so here's why
okay here's a scheme function
call here's the same thing in almost every other programming language
right
um right there's another procedure call function call F of three and four and in
almost any other programming language it's F parenthesis 3 comma 4 close parenthesis
okay does apply know which of these things you
typed no apply knows that you want to call the function
f and you want its argument values to be three and four okay that's what we tell
apply getting from this string of characters open pen F Space 3 Space 4
Clos pen or F pen 3 comma 4 Clos pen getting from that to the arguments to
apply is EV Val's job so eval takes this semantic stuff and gets rid of it so
we're left I'm sorry the syntactic stuff and gets rid of it so we're left with the semantics of calling a function does
that answer the question okay great see you next week
