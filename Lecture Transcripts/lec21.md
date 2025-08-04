Transcript


thank you I was um doing some system
administration and lost track of
time
okay so I'm going to start this up
where's the button there it
is uh oh oh bye whoever you are
right oh I'm sorry I missed you visiting high school
students
bye oh Lord oh
great Okay so
what we want to do is implement the stuff we did last week
in plan old scheme okay so we want a
system in which well in particular we're worried about local state
so we want a system sort of like
this we have a class and we have an
instance and another instance
and another class and it has instances
too and there are Global variables accessible to everybody
there are class variables Associated to any instance of uh accessible sorry to
any instance of that class and then there are instance variables that each one has on its own and we want to see
how that works
um how far did you get you
got nowhere okay all right then we'll H start up already
okay um so the starting
point is to notice that the substitution model that you've learned up to this
point U is not going to work once you can do set
bang because if we take this zero and substitute it in
here then the set bang isn't actually going to do any good I'm sorry if we substitute in here in particular the set
bang no matter what the set bang makes of that this is going to just return zero every single time so we need a
different model of evaluation that takes into account the
possibility of changing the value of a variable and makes of a local variable
and makes that possible and um I'm going to plug this
in yes I want to rent
it okay
okay so this is um our first definition of a counter like the count class that
we saw last time you would send it a next message and it would count up
and the way this works is that there's a global variable
counter whose value is now zero I can call whoops
count count count and every time I call count
it increases the value of that Global variable so this is just a straightforward use of set
bang and um it shouldn't be a surprise to you that this works but it's not good
enough for that model that we want in which we have private values of the
counter one for each instance of the class um so
now all right this is the one that Jordy was
writing so here's an attempt Mt to make a local value um for each counter there's
still only one counter but I'm making uh counter I guess we have count and counter backwards um instead of counter
being a global variable I'm going to make counter be local to this
procedure so that's the idea here so now we're paying no there is a global variable counter which I can't get rid
of but forget about it cuz we're not using it so now if I say
count one I call count again I still get one
no matter how many times I call count I'm going to get one why is that well
every time we call count it makes a brand new variable
counter this is the use of let that we're accustomed to where we create a
variable just long enough to run the body of a procedure and then that variable's gone and the next time you
call the procedure it creates a brand new local variable well that gives us local
variables but not persistent ones that we can use to remember the count from one call to the next so here's the
version that works
um so first let's look
it this has a different name result so we don't get confused with the counter
Global variable now if I say count
count count you see that it does count but result is not a global variable it
doesn't exist globally and this works in a very
strange way that isn't going to make any sense until we've been talking about it for a while namely notice there's no
parentheses around count here so this is not a definition with an
implicit Lambda the Lambda that creates the count procedure is this
one and it comes inside the let that creates the variable which is going to
be its local state variable so that seems really weird what does it mean to put a l inside a
let um if you think of the procedure as just
being the text of the Lambda expression which is how it worked in the scheme one
interpreter that you saw a few weeks ago remember when you said Lambda blah blah blah the value of that expression was
just the Lambda expression itself and in that kind of world because we were using
the substitution model in that kind of world this doesn't make any sense because
um it's how do you find the result variable that isn't defined inside that
Lambda and what's new in the environment model of evaluation which is what this
week is about is that um a
procedure isn't just the stuff in the Lambda expression it's the stuff in the
Lambda expression Plus some way of
finding um free variables in the Lambda expression what's a free variable it's
one that isn't a formal parameter of the Lambda so it's not defined inside the
Lambda comes from outside the Lambda up to now outside the Lambda just
meant Global and that's how it is actually in a lot of programming languages all those
C like languages cc++ Java they don't have the idea of procedures inside
procedures so there's just procedure local variables and Global variables and that's
it um but we have the idea of of a Lambda
expression inside another Lambda expression and that's what you're seeing here because remember a
let is an abbreviation for a Lambda expression and then a call to that
procedure so this thing that's up on the screen is equivalent
to um Lambda of
result and then Lambda of nothing uh Z bang blah blah
blah and
um call that with a zero as it's AR
arent right so the let means this so in this Lambda expression the
outer one the green yeah no I'm sorry the outer one the outer Lambda expression
result as a formal parameter so it's bound so when you see a result in
here in this expression it's bound so we know what result means it means this
variable but if you're only looking at the inner Lambda there's no way to know what result means
if all you have is the Lambda expression so we're going to see later on as we look at the details of the environment
model that a procedure it's drawn like this it has a
left bubble and a right bubble and the left bubble essentially points to the Lambda
expression and the right bubble essentially points to
bindings for the variable that are free in that Lambda expression so there's
something here that says result equals
zero okay so both of these things are part of the procedure and so when that procedure
says set bang result result plus one we know which result we mean and we can
turn that to a one and then next time turn it into a two and so on okay so I
know it isn't clear yet how we get here but is it clear what we're trying to
achieve right that when you create that inner procedure the one that's
highlighted up there it remembers where to find the value of
result right that's the goal and if we can do that then we can
have different counters that each have their own result so far we don't so far we only have one counter because we're
working up to this a step at a time but we want to see how this kind of
expression turns into the count procedure which is just that highlighted
stuff except knowing which version of result to use so if we had a lot of
these counters if we said define count two and then the same thing in fact that might be worth doing
never thought of that before let's define count two to
be all
thiss
copy paste okay so now we still have count and it's now up to four
we also have count two but starting at one here's the original count up to
five okay so we have two counters Each of which has sort of the same code but two different result
variables right because we did that let twice one when defining count and then
again when defining count two okay if you're feeling iffy about this
um it's not surprising stick with us the problem is
oh and I should have said right at the beginning I apologize for the huge amount of reading in this week's
assignment which is the O of the line handout and 2.1 and 3.1 and
3.2 uh the reason for doing so much this week is um I used to do them one at a
time and I've learned that students can't understand 3.1 until they've read
3.2 and they can't understand 3.2 until they've read 3.1 so there's a little bit of a problem
here and so what you're going to do basically if you haven't done it already is read both sections
twice okay read 3.1 read 3.2 then read 3.1 again and it'll make more sense this
time and then read 3.2 again and it'll really be clear okay um so we're
cramming a lot into this week 3.1 is the thing we're doing right now about what
it is that we're trying to achieve namely how can we get persistent local
state variables right let me
actually I'm going to write that down
peristent low go State
variables okay you know what a variable is uh you actually have heard the term
State variable lots of times starting with um the iterative fast X remember
that homework problem they said you have to use a an extra State variable to keep track of where the computation is up to
so it's sort of a memory of what we've done up to this point
um so what's special is that we want two things that used to be contradictory we
want persistent and we want local Global variables have always been
persistent you define it it's there forever local variables until now well
until last week I guess have always been kind of ephemeral they come into being when
you're r a procedure and they disappear again as soon as that procedure finishes so we want something that is
like The Best of Both Worlds it has the sort of cleanliness
advantage of localities that it's restricted to a particular piece of code
and the Persistence of global variables
um and we now see how to achieve that with the Lambda inside the let but what
we don't yet know is how that works how that manages to make a persistent local
variable and that's what we're going to see the rest of this week um or you are without me okay uh
now what we're going to do is we have how to make a single
counter and now we're going to look at how to implement essentially a class
so I have this thing make count make count is sort of the equivalent to
Define class count although it's much simpler than what a defined class turns
into so every time we call make count it's going to make a counter and notice that there are
parentheses around make count so the let that you see up at the top of the screen
is part of the body of make count it's inside the make count procedure so it works like this
Define C1 to be oops
make count toine C2 to be make
count and I just call C1
okay that's that's one counter and now I can call C2 it starts from
one counts up now if I go back to C1 it'll say five okay so C1 and C2 or two
counters make count is sort of a counter Factory and the way make count works is
that every time you call make count it does this thing about a Lambda inside a let so the value that make count returns
is the value of this innermost Lambda expression so each counter
is a procedure created by this Lambda expression but I can't any longer say is
this procedure because now we know that a procedure isn't just the information
in the Lambda expression namely the formal parameters on the body it's also
what we're going to call an environment meaning what are all the variables outside of this
procedure to which this procedure has access so how do we resolve free
references that is references to variable names that aren't formal parameters of the
Lambda um and the answer is we look them up in the
environment uh and the environment gives us the value actually technically if you're a programming language person I'm
not supposed to say the environment contains the value what I'm supposed to
say is that um the
environment binds the name to a box and you can change what's in the in the
boxes a zero or a one or a two or whatever um but this is a level of
complexity that we really don't worry about in this class it's not going to
matter because you're not trying to write a very efficient um
compiler for language okay um so that's make count uh if I move up
here and come down a bit this is make count with all the lambdas made
explicit so this Lambda comes from the fact fact that
make count was in parentheses when I said define make count so Define with
parentheses uh implies a Lambda and this one has no formal parameters because it
was open parenthesis make count and then there weren't any formal parameter names just close
parenthesis this
Lambda comes from the let let result be zero Okay so so notice that this second
Lambda is the only one that has two open parentheses in front of
it now in talking about this I don't want
you to put in your head a sentence that
starts you have to use two open parentheses when okay instead I would like you to
understand what each of these parentheses is the limits so we just happen to be creating
a Lambda expression this one so this open
parenthesis the inner one ends here and that whole thing is a Lambda
expression so it creates a procedure namely the let
procedure right the outer Lambda was make count the second Lambda is the let
procedure and then this open parenthesis goes with the Lambda the
inner Lambda expression that I just showed you and the zero and this closed
parenthesis okay so the outer parenthesis right here oops this
one says call this function with the
argument zero okay and that's the let a let is an
abbreviation for two things a Lambda expression and an invocation of that
procedure so that's why there are two parentheses here because the letter abbreviates two steps make a procedure
invoke it okay um this inner
Lambda doesn't have two parentheses or around it it just has one and this is
the value that the second procedure returns and therefore it's the value
that the first procedure returns um so this inner Lambda is a
particular counter it's C1 or C2 is this inner Lambda or a procedure
generated by this inner Lambda now um
the way we get two different counters out of the same piece of code is
C1 is this procedure and
C2 is this procedure they point to the same Lambda
expression but they have two different different variables
result two different environments Each of which has its own result variable
okay so same procedure text but different procedures with different
persistent local state variables
okay um okay moving on
all right now we're at the point where we have to actually yes
go uh you're talking about these parentheses okay what goes here in a
Lambda expression is its formal parameters the names of its arguments so
if you have open print Clos print that means it's a procedure that doesn't take make any arguments like down here when I
called C1 I didn't give it any arguments right does that answer the
question I'm not sure what you mean what when you say it Returns what it are you talking about the Lambda every Lambda
returns a procedure and every procedure has a formal parameter list and a body the
formal parameter list can have any number of formal parameters including
none what's the purpose using the purpose of Lambda is to create a procedure we want to be able to invoke
C1 right so down here when I wrote this what does this
mean when you say that it means whoops sorry I clicked a button bit without
meaning to so what does that
mean no I mean what does that what does it mean when you type a scheme open parenthesis C1 close par what yeah
invoke C1 so C1 has to be a procedure right where does that procedure come
from it comes from here now why does it come from that one
well this outer one that's the procedure make count so the outer one actually
includes everything all the way down to the end like this okay that's the procedure make count I invoked that one
at the beginning when I said define C1 to be the result of invoking make count
okay so that's why that first one isn't
C1 this one isn't C1 because when you call make count
it doesn't just say return the value of this Lambda expression it says call this
Lambda expression with the argument zero and then return whatever that returns okay well what so that's the let
so what does the let return it Returns the value of its
body which is this Lambda expression so this is the thing that we Define C1 to
be is the value of this Lambda expression okay the important new thing
is that C1 isn't just this Lambda expression when you evaluate a Lambda expression you get one of these things
with two bubbles the first of which is essentially the Lambda expression itself
the second of which is this other thing called an environment that we're going to talk
about okay yes
what if you had the Lambda result and you didn't have this Lambda here then when you called make count it
would do all of this stuff you don't want to do this when you call make count you want to do this when
you call C1 right yeah
yeah good question the question is um why is the coup why is making a
procedure coupled to making an environment um actually technically you'll see that
that's not the case when we actually talk about how the model works uh making an environment comes from calling a
procedure but the real the real answer to your question which is a deep good
question is that environments are not visible things in
the language okay it's not a data type with selectors like what's the value of this
variable or anything a scheme user does not see environments in fact we've been
using environments all along um completely invisibly to us so what we
see is not environments what we see is procedures it didn't have to be that way
you could imagine designing a programming language the way you said um all I can tell you is 50 years of lisp
experience have shown us that this is a system that's really really really
useful okay so one of the things that lets us do is this business of making persistent local state variables we get
that free and and that's a thing I think I said this last week but I want to emphasize it again in the context of
this week all those other
languages they think that you need special objectoriented features in your
language in order to do object-oriented programming so there was C and C wasn't
objectoriented so they made it C++ adding
objectoriented syntax to the language so that you could Define classes and things
uh we did the same thing last week we made sort of scheme Plus+ but the point is you don't have to that scheme wasn't
especially designed to be objectoriented it was just designed to do the right
thing and object orientedness happens to turn out to come out
free um when you do that um so if you talk to old Lis pans about
object-oriented programming they all wave their hands and say oh objects are just
closures what a closure is is some way of representing which variable do you
mean by this variable name in this place and that's an environment so all an
object is they're saying is an environment and it's true all an object is an environment that
contains instantiation variables instance variables class variables
methods all that stuff have to be in the environment and that's an object right
um I don't actually offhand know of a language in which environments are
actually user visible do you is there a language like
that yeah um recent versions of
scheme actually actually do have environments as a data type but they only give you the global
environment and uh if you're lucky no no not even not even if you're
lucky they give you the global environment and the even more global environment that has the initial values before you do any defines those are the
only things that you get um you can't get any sort of local individual environments and the reason for that
actually has entirely um reasons about um compiler
efficiency or rather the efficiency of compiled code if you keep the user hands off the
environments then you can compile scheme
programs on the basis that the compiler knows before the program is even
run uh what variables are in what environments where to look for a particular variable as seen in a
particular context so um when you compile something
like our count thing and it says result in here the compiled code doesn't say
look up the name result it says take the first variable of two environments back
from here or something like that um and that makes things much
faster whereas if users can change environments on the Fly um then the compiler can't make those
assumptions and it programs are a lot slower so that's really why they do it this way but it turns out to be good
enough because we can use a procedure to
represent an environment and that's what let does basically let says I need to
make an environment with this sort of local variable in it um and you could
imagine having a make environment primitive that would do that and that would be used by
but instead we just say make a procedure that has this local variable in it and then call the procedure and
that's you know it's sort of um two features for the price of one in a way
okay but good question all right let me move on because we have hardly any time entirely due to my stupidity in not
watching the clock but uh we're kind of in a rush so let me move on okay so
we're going to talk about the environment model of evaluation
um in the course reader on page 320 you don't have to look at it now but in
there is all on one page the complete rules for the environment model of
evaluation okay so that's sort of your reference document for how environments
work um so let me me remind
you about the substitution
model what do we do when we see a procedure
call First Step recursively call Ev Val to evaluate all the sub Expressions the
first one tells you what procedure we're calling and the other ones tell you what the arguments are right so we always
deal with actual argument values when we call the procedure not uh actual
argument Expressions because we've evaluated them so that's what makes scheme an applicative order language and
that's still true in the environment model
Second Step
apply the procedure to the argument
list still true
the difference comes in what apply does in the substitution model so here's
step 2A it
says
substitute Arguments for
parameters in in the body right so we take the body of the
procedure which is an expression or a bunch of expressions and we turn that into a new version of the body in which
all the formal parameters have been replaced with values so now we don't have any
variables for the formal parameters anymore and
then eval the modified body
okay so that's the substitution model everybody clear about this
questions this you've known forever since week one okay here's the
difference 2
a make an environment
with the parameters bound to the
arguments bound to means like pointing to having that value okay so we make this new kind of
thing called an environment and then 2B
says eval the
body not some different version of the body but just the
body in the new
environment so what is eval in all about
well substitution model we say eval an
expression in the environment model we say
eval an expression in an environment okay so in the in the real
scheme interpreter eval takes two arguments not just one and the second
argument is an environment in which um all the variables have values
okay and we look up variables in the environment to find out what their value
is and we also look them up in order to change the value if you do a set Bank okay
so um that means for example that we have to change the readal print
Loop so that when you type in an expression it says
eval read right
call to read so this is the expression that you typed in and in the substitution model there'
just be a closed parenthesis here but instead we have the
global environment this is not a variable that
users of scheme see this is a variable in the scheme um implementation itself
so if you read the code for the chapter 4 uh scheme evaluator which comes up in
a month um it looks like this so there's a variable called the global in but
we're going to add to that and here's the other crucial
point because when we make a new environment there's two steps one step
is to make a box which is called a frame in which we have something like
result equals zero so that's a frame and this frame has a pointer to some
existing environment like let's say the global
environment okay does that picture start to look like that picture a little bit
okay Wednesday and Friday you're going to see how this model which is really very simple fits on a page gives us that
picture in effect okay uh I will see you in a week um but don't skip lecture on
that account it'll be important
UC Berkeley 