Transcript


okay good afternoon I hope all these empty seats
are people sleeping it off rather than people who dropped the course um okay so
two administrative things one of them is um this coming Monday is a holiday um so
your assignments that would be due Monday or due Tuesday at noon instead I think we have that correct in one place
and incorrect in another place on the reader but anyway it's due Tuesday
um your midterm one grades are in G look up a bunch of people have come up to ask me about how this all works so first of
all um if you don't already know this uh if you log into your class account and
you say G look up all one word like that um it'll tell you your grades and you
should do that periodically in case something that you turned in doesn't get graded after a week or two you know you
should complain about it um if you do G lookup you will see two
grades one labeled mt1 and one labeled G
mt1 um mt1 is your individual midterm score it's out of 40
points GMT one is your group score which I forget how many points JY nine out of
nine points thank you okay um
when we do grade computations at the end of the semester we take a weighted sum of mt1
and G mt1 um and you can see the weights and you
look up also and if you add up a perfect mt1 score and a perfect G mt1 score and
you multiply by those fractions and you add them up it still comes out to 40 points the idea of the waiting is that
for those nine points that you did twice um we count 2/3 individual one/
third group in practice what that means is um
your group midterm is likely to pull you up by a point or maybe two points it's
not going to make an enormous difference in your grade but a little teeny one um
for purposes of should I drop the course or not my advice is just look at your individual grade um because that's the
best measure of where you are at this moment in the course
um so big thank you to the Tas for getting the grading done before the drop
deadline um and I think that's it for administrative
things I think I've said everything I have to say about the Exam scoring um okay today what we're looking at is a
scheme interpreter written in scheme um so just first off why isn't that a
stupid thing to do because you know you can't run it unless you already have a scheme interpreter um and it's going to
run slower than the one you already have so what's the point um and the point of
course is pedagogic it's for you to learn what an interpreter looks like but
also it means later in the semester we can play with variant versions of scheme
we can say what if we take scheme and add this feature to it or change the way it does that um and we'll see some of
that later on in the semester so it lets you do that it also makes a point I'll
talk more about this when we get to chapter four where the book starts doing interpreters um it makes a point about
uh universality of a programmable computer that um we can
write one computer program namely The Interpreter that can do any
computation by taking as data a formal description of the algorithm that you
want to use so the scheme interpreter takes a scheme program as part of its
input data and it turns that into whatever result you want and that's really an
amazing thing to be able to do right Universal programs um you guys all grew up with this uh I
just barely grew up with it I I was born just about the time they were building
computers that could do that for the first time um a little later I missed it
by a decade I guess all right um up on the screen is the one screenful version of a
scheme interpreter in scheme and we're going to start by going through this um it should really not
scare away anybody I think because it's very simple and you can see all of it um
so up at the top is the re Val print loop it's just like what you remember
from the calculator program it reads an expression it calls eval on that
expression um and then it prints the result okay and then it loops
so read eval print Loop um and then we have eval and apply the same as the big pieces of the
calculator program except because this is scheme instead of calculator language
it's more complicated we have things like variables so in scheme there are four kinds of
expressions and you can sort of divide them up into two groups like this so
here's expressions
and there are Atomic expressions and there are lists Atomic means you don't divide it up further into pieces you
just look at it as one thing so now there's two kinds of each of those the atomic
Expressions come in self- evaluating this we saw before in the calculator
program where it was the numbers we're self-evaluating in scheme there are a
few other self-evaluating things like number sign T and number sign f are
self-evaluating um strings in double quotation marks are
self-evaluating there are few other things that we're not really getting into um so they're self- evaluating
Atomic expressions and then the thing that's new
is that there are symbols which are the names of variables and those are not
self-evaluating the value of a variable is you know whatever its stored value is
um but it is atomic when we see a variable we're sort of at a base case of
the recursion in eval um so we have the variable as just
a thing to look up and find out what its value is um and then there are lists those come
in two kinds also and they are the most usual
kind there's a procedure call procedure invocation those mean the same thing so
usually when you see stuff in parentheses it's procedure argument argument argument and we're calling that
procedure with those arguments and the other thing that's in parentheses is what
special
forms and what's special about special forms is that they don't follow the rule
of applicative order namely we don't have to evaluate all the sub Expressions
first um and each special form has its own rules for what it evaluates and when
and under what circumstances um so our
eval here in tiny scheme oops here we
go has a cond with four cases and in the real one when you look
at the code there'll actually be five cases the last one is else
error um but basically here I'm trying to simplify things as much as possible
so we're dividing things into four cases if the expression is self- evaluating then we return exp which is the
expression itself so you call eval on five you get five okay next
case it's a symbol and we look it up okay in this
evaluator which uses the substitution model of evaluation that you learned in chapter one if eval sees a variable
it has to be a global variable because it is something that
was defined with a Define form at the scheme
prompt because anything that's an internal definition or that's a
um formal parameter of a procedure has been substituted
out right by the time we call you Val because remember back from chapter one how do we call a procedure
we substitute actual argument values for the formal parameters in the body of the procedure that gives us an expression
that's just like the body of the procedure but without any local variables so the variables that we see
mostly almost entirely are the names of primitive procedures you know you say cons blah
blah or you say plus blah blah those things are not
self-evaluating you know the the value of the word Co NS is not the word Co NS
it's the list con the pair Constructor procedure right and the value of plus
sign is not plus sign it's the addition procedure and so on so in this evaluator
almost every time we see a variable it's going to be the name of a primitive yes
okay he's saying why don't we eliminate the category of self- evaluating and just say five is a
variable that whose value happens to be five
um I guess that would make it harder rather than easier because you know
there are infinitely many numbers right and we're not really going to have a table someplace that says the
value of five is five so what you're going to end up doing is making this same distinction inside your variable
lookup procedure and it's more obvious to put it out here
okay um okay moving right along there are two cases
left um it's a special form and this is the main thing that
makes the real scheme evaluator in scheme bigger than one screenfold which
is that each special form has its own algorithm its own rules for how it's
evaluated and therefore each special form has an a procedure to evaluate it
so when we look at the real thing in a few minutes we're going to see things like eval if eval Lambda you know those
things right uh for all of the special forms that we have which is not going to be by the way all the special forms in
scheme this is a subset of scheme that we're
interpreting right now but each special form does its own thing it takes the
expression and does whatever it wants with it and finally uh if it isn't one of
those things uh then it has to be a procedure call and on this line and the line after
it oops what did I just do I said mid F I meant to say control
F
what okay I'm
confused oh I meant caps
lock what
well right I'm in insert mode is that what
you're saying oh but I'm kind of
weird no
all
right okay I'm not going to touch it um okay so this line right here and
the line after it this expression are the heart of what we're learning from
studying this evaluator today it's not all there's a lot of details that we're going to learn but this is
really the most essential piece of it which is how do we evaluate a procedure
call so how do we evaluate a procedure call well we evaluate all the sub
Expressions including the first one it might be a Lambda expression or something so you have to evaluate it and
we apply we we use apply to call the
procedure which is the value of the first sub expression with the argument values that
are the values of all the rest of the Expressions okay so apply you'll remember from the calculator program I
hope apply takes two arguments a procedure and a list of actual argument
values well how we get the procedure is we eval the car of the
procedure call because car of the procedure call its first element is the
subexpression whose value is the procedure that we want right the sub
expression itself is for example maybe a symbol like plus sign or
cons or it might be a Lambda expression or it might be the call to
some procedure that you wrote whose value is a procedure but one way or
another the value of that first expression has to to be a procedure and then we take cter exp which is the list
of actual argument expressions and we evaluate each of
those by using map we say map eval over cter
X so what kind of recursion is this tree recursion right because
there's more than one recursive call to eval happening in for each call to
eval right if we call a procedure with three arguments we're going to do
actually Four recursive calls to eval one for the procedure and three for the
arguments okay so we do that and then we're in the the world of apply remember
in the world of apply there aren't any Expressions there's just values so apply doesn't know anything
about scheme notation all it knows about is how to call a procedure well as it turns out there are
two kinds of procedures and they are primitive procedures the ones that are built in to
The Interpreter and procedures you create with
Lambda including in the actual scheme lambdas that are hidden inside a Define
with parentheses around the name and lambdas that are hidden inside let
Expressions right but one way or another there's a Lambda that makes the procedure so if we come down
here
oops what do we do if it's a primitive procedure magic we do magic primitive
procedures happen by Magic what that means um in a real scheme interpreter
is that uh primitive procedures are little chunks of machine language code
things that have been compiled into the native language of the computer hardware that carry out whatever it is
that the Primitive is supposed to do um for our
purposes uh I put it as magic because what that means is we're not interested
we we just don't know how Primitives work that's for another day okay
um the interesting part of apply is what
happens if it's a Lambda created
procedure well if it's a Lambda created procedure um it comes from a Lambda
expression which looks like Lambda of XY
z um I don't know plus x * y
z okay that's a Lambda expression and it
has formal parameters and it
has a body um and we have selectors Formals in
body um that pull out the formal parameters and the the body of a l of a
procedure because when we evaluate this Lambda expression we're going to create an abstract data type
procedure and that abstract data type has formals and body as selectors um and
the other thing that we have is actual argument values and that's in args which is the second argument to
apply okay so the substitution model of evaluation says
substitute the formal parameter I'm sorry substitute the actual argument values for the formal parameters in the
body and then evaluate the resulting expression and that's what this says
substitute here this thing that takes three arguments body of proc formals of proc and args you wrote that for
homework some time ago right who remembers ready
substitute Yay good so those of you who don't remember writing substitute wake
up um those of you who do remember you understand how this evaluator Works
basically um I'm saying this with my fingers
slightly crossed because the substitute that you wrote for homework is not quite
adequate um to use in this interpreter because of the following special
wrinkle suppose I say Lambda of
X Plus
X LDA X time
X3 plus
X5 okay let's say I call this with the argument
10 footnote this is a really stupid way to
write code first of of all you shouldn't have
a variable called X unless you're writing a program that's doing you know graphing of functions and you have an X
this way and a y that way then you can get away with calling something X but usually you should use meaningful
variable names and second of all more important if you have a Lambda of X you
don't want to also have another Lambda of X inside here it's only going to confuse you but let's try to unconfuse
you by grabbing the yellow chalk that I see over over
here bad planning for lecturing so I'm calling boom this whole
three line Lambda expression with 10 as the actual
argument so we're going to substitute 10 for X in the
body what is the body of the Lambda it's this
that's the body okay so I substitute this x with
10 I substitute this x
10 what about this one and this
one should I put tens here should I say Lambda of 10 *
103 no I certainly don't want to say Lambda of 10 that's just nonsense
already but I don't want to substitute this one
either because for this inner procedure
call here's its body
and what we're going to substitute into that body is the value of +
105 so this x is
15 right so we do 15 * 3 is 45 + 10 is
55 that's the value of the expression and when I did that first
substitute into the yellow body this X was what we call protected
from substitution by this x okay so the actual substitute function
that we're going to look at in a little bit is a little more complicated than the one that you wrote because of that
now having said all that the next thing I want to say is
don't put a lot of effort into learning how substitute works because in
a couple of weeks we are about to learn that scheme doesn't really work this
way that scheme doesn't really do evaluation by substitution we're going to learn a more sophisticated thing
called the environment model of evaluation which is how scheme really works substitution model it turns out is
adequate for functional programming um but it's not adequate for some other ways of programming uh we'll
talk about why that is later for now all I want to say is um just you know take
on faith that substitute does the right thing and don't get caught up in the
code of it but you should understand this line where the cursor is
blinking where we take the body of the procedure and in that body we replace
each occurrence of a formal parameter with the corresponding actual argument value apply gets values so there's no
more Expressions here when we're in apply except for the expression that substitute
returns okay that's the expression that's this modified version of the procedure body in which we've
substituted out the formal parameters and replace them with the actual arguments and we have to eval that
expression and that's what it means to call the procedure so the line we were looking at before where eval calls apply
and this line right here where apply calls eval these two things together are the heart of The
Interpreter okay and they constitute a mutual recursion and therefore a tree
recursion now what is it about scheme Expressions that makes tree recursion make sense here the and tree recursion
works for hierarchies right two dimensional hierarchies we're talking about that this whole week what's the
hierarchy in a scheme expression well well scheme Expressions can have
subexpressions right and those subexpressions can have subexpressions and so on so it's not
surprising that there's a tree recursion involved in doing eval and the other thing is Expressions
can call procedures those procedures have bodies which are expressions and so that also uh gives rise to mutual and
therefore tree recursion okay
um this is worth some study it's reprinted in my lecture notes um it's
nice because you know you can see it all at the same time there it is and yet um
if you understand this you really are about three4 of the way to understanding
how a scheme interpreter works and if you understand a vow and you understand a ply and you know what a
reppel is which is the easy part um then you know how a scheme interpreter Works what you don't know
yet you don't know how the special forms are handled and you don't know certain
things that we're totally leaving out of the discussion um you don't know how The Primitives
work so you have no idea for example what it means for a computer to do arithmetic yet that you're just taking
on faith that computers can add up numbers yeah
Define as a special form okay because its first argument is
not evaluated right it evaluates its second argument um which is typically a Lambda
expression
uh now I lost my train of thought ah um
oh yeah things you don't things you don't know so we're taking arithmetic for granted um you're going to take
arithmetic for granted in 61b also in 61c you learn how computers do
arithmetic okay because that's a very low-level thing to learn in our curriculum we start at high levels of
abstraction and work our way down to the nitty-gritty of what the hardware is actually doing so that's something
you're not going to learn until later another thing that you'll start getting a glimmer of in uh
61b and a bigger look at in 61c but you're not going to totally
understand uh until you take operating systems 162
is memory allocation in the computer so when I say cons to make a
new pair uh somehow my scheme interpreter has to find someplace in memory to put
that pair um how that works is actually pretty complicated uh and we are totally taking
it for granted that's a way in which we're cheating by writing scheme in scheme and another reason for example
why I'd much rather write scheme in scheme than try to write scheme in some other language where I would have to
make explicit more of these uh choices um so we're ignoring Primitives we're
ignoring memory allocation uh we're not ignoring special forms we just haven't gotten to them yet but we will okay
everybody with me okay here
goes now do I have
oops no
all right here's the scheme one evaluator
um here's the reiv Val print Loop The crucial part is this line right here
that says print of eval one of Reed uh eval is called eval one and apply is
called apply one in this scheme one interpreter again because STK has
primitive procedures eval and apply that we don't want to clobber okay um when you read this code
which you should do um it talks a lot about how this all
works so it says right here the thing that I said about four kinds of Expressions says the value of a
self-evaluating thing is the value itself um then it says something a
little interesting unlike real scheme an STK procedure is here considered a
constant expression
um what that that's a little weird because you can't type in a
procedure but um one of the ways in which we cheat in
this interpreter is we take all the procedures that SDK
knows about and treat them as our Primitives so STK Primitives are scheme
one Primitives and also things that you defined in STK are scheme one
Primitives and as the comment says because of the way that plays out um
when we look at a symbol that's a global variable um we find the value associated
with it it's a procedure we end up eving the procedure so we just treat that as
um as self-evaluating even though you can't type in a procedure uh it's sometimes in
a recursive call we're going to want evalid procedure so um that's
that it's a little bit of a cloue um so in the substitution model we only see
global variables not local ones in this evaluator there is no Define and so the
only Global symbols are the ones that name primitive
procedures um since that's true instead of actually building a symbol table
where we can walk through looking for a name and find the value associated with it we just cheat and ask STK for the
value of symbols you'll see that in just a moment um
quote is a special form if is a special
form in this evaluator not in the real scheme but in this evaluator the value
of a Lambda expression is the expression itself so we use Lambda Expressions as
the abstract data type to represent non-primitive
procedures why is that well what do we need to know from a procedure we need to
know the form normal parameters on the body and those things are in the Lambda expression so I'm just going to take the
Lambda expression itself and say that's the procedure okay
um and again all this stuff I'm going over very quickly because you have access to this file which will tell you
all about it um so here is the real eval one
um so a self- evaluating expression a constant the value is the expression
itself if the expression is a symbol don't be confused here we're not
calling eval one on that symbol that would be an infinite loop we're calling STK
zal so when we get down to sort of the base case of an evaluation which is
something Atomic that isn't self-evaluating we say Okay SDK what's the value of this
and that value will typically Be A Primitive procedure that's the only thing we really use globals for
um quote is a special form um this is what happens remember
when you type a quotation mark an apostrophe um into the scheme
interpreter the read procedure that we called up here turns that apostrophe
into to open p quote blah blah blah close PR okay so that is a special form quote
and we're returning here CER of X why cater
because I typed in quote Fu like
this the read procedure turned this to quote F like
this and the value of this expression should be Fu which is the second element
of a list if we look at this quote expression as data it's car is the word
quote it's cater is the word Fu so that's what we want we return it's cater cater means second
element what if it's an if expression okay
now I have to convince you that this is not cheating namely we're calling stk's
if um to evaluate the pieces of this and
we're taking advantage of the way stk's if Works which let me remind you it's a special form too it evaluates the first
argument which is this it's not cater of X it's eval one of cater of exp so we we
evaluate the first argument to the if we get true or false if we get
true then we're going to eval one the second argument if not we're going to
eval one the third argument now why isn't this cheating
um imagine that uh for
homework you have to write an interpreter for Java in
scheme okay that would be a little much for homework maybe a
project um well
Java has a notation that looks like this
no it doesn't if x is equal to
zero do some stuff
else these are braces do some other stuff timey col
okay so that's what if looks like in Java
how's your Java interpreter going to evaluate that well the first thing it's going to
do is some sort of parsing work some grammatical work to extract the
interesting pieces of that the interesting pieces
are this stuff in parentheses which is the expression whose value should be true or false so
you grab that and you grab this stuff which is what to do if it's true then
you grab this stuff which is what to do if it's false the word else is not interesting these braces are not
interesting this semicolon is not interesting so we grab these things out of this syntax and then what do you do
you're writing a Java interpreter in scheme well you have an if right you say
if Java eval of that first thing then Java eval the second thing
otherwise Java eval the third thing and you wouldn't feel like you're cheating right it you'd feel perfectly
okay about using a scheme if as the implementation technique for a Java
if well we're doing the same job except we're writing a scheme interpreter in
scheme it's not cheating to use
stk's conditional mechanism as a way way of implementing our conditional
mechanism just to make that point clearer we could if we wanted to change
the syntax of scheme if okay so I'm going to
write schemat a new language schemat and in the schemat
language you say if blah blah blah then blah blah blah
else blah blah blah all these things in parentheses
okay so now Along Comes an if expression we see the first word is if okay it's the if special form how am I going to
implement this well I'm going to
say if now this is STK code
if evaluator
of catar X then I want to evaluate this right
this is the car the CER the cator the cator
right otherwise I want to eval the cator
which unfortunately doesn't exist so I'll say as a primitive I mean so I'll
say evaluator of list ref
x 0 1 2 3 4
5 okay so now I've written a piece of code that evaluates something that isn't
a scheme expression in scheme you can't say that if blah else then blah else
blah and scheme you have to say if blah blah blah so this code is different from the
code up on the screen for eval if because it evaluates a different piece of the
expression writing schema lator like this feels a little bit less like
cheating because I'm using stk's IF to evaluate something that is not a scheme
if okay it's a little bit more like a Java if you know we could even put braces in
and you know make it more interesting um more like a Java if well if it's not
cheating for schema later it's not cheating for scheme one either it's
really okay to use stk's conditional mechanism as part of the algorithm for
implementing scheme 1's conditional mechanism okay now what we do have to do
is make sure that we use scheme one
techniques to evaluate each of those pieces when it's time to do so so that
has to be an eval one in there and not an STK eval for each of those three
arguments to the if any questions about
that okay thumbs who's with
me okay it's really very frustrating when people don't vote because then I
feel like not only are they not with me but they've given up so if you don't want to depress me I'd
rather see that than nothing um
okay there's only one other special form in this little scheme interpreter
and that's Lambda and as I said a little while ago
in this trivial scheme interpreter um the value of a Lambda expression is
the expression itself because that's how we're going to represent um non-primitive procedures yeah so Mis
interpret it's the Lambda expression
itself not as opposed to the body the body is part of the Lambda expression okay and we could pick some other so if
I were being really elegant about this
instead of saying exp at the end of that line it would say make
procedure Lambda formales of X Lambda body of X and make procedure would
return a list of length three whose car is the word procedure whose cater is the
formals and whose cator is the body but it so happens that I have
almost exactly that except instead of procedure at the front it says Lambda the front so I'm just going to use that
okay when we get to the real um environment model of
evaluation you will see then that in the real scheme um the result of a Lambda
expression is something more than just what's in the Lambda expression itself and then there's going to be a
difference between Lambda Expressions which are input and procedures which are kind of output of this evaluation
process okay but in our simple evaluation they're the same so if it's a
list I I really should call list here rather than pair but pair is Theta of
one and list is Theta of n um so I cheated and called pair if it's
if it's a list that isn't a special form what is it a procedure call right so
we're going to call this procedure um
by calling apply one and the arguments here here we're
doing exactly what I did in that tiny one screen version
exactly it's a Ply one of eval AAR which is the procedure we're calling and map
eval over the cter which is turning actual argument Expressions into actual argument values okay so by now this
little piece of code right here where the cursor is blinking should seem like an old familiar friend you've known
since childhood namely 20 minutes ago
okay questions so
far okay we only have three minutes for apply so let's do that quickly uh
there's a bunch of comments on apply that you can read at your leisure here's the
[Music] code and again the tiny version had two
branches here there's three branches the third is else error
so oops thank
you all right so right here we call procedure question mark notice that this
is an STK procedure question mark right it's not procedure one question mark
so is this an STK procedure that's asking the question is
this a scheme one primitive because let me remind you that every procedure in
STK we're taking as primitive right so we get sort of at one
blow stk's entire repertoire Primitives plus any procedures you may have defined
an SDK well if if it's a primitive procedure
how do we invoke it and in in tiny it said do magic and
here's how we do the magic in our case we call stks
apply right so if it's an STK procedure then SDK knows how to call it and we
just let SDK do that it's important that by the time we get to apply there's no
more notation only values because STK doesn't know about scheme one
Expressions it does know about values because they're the same values right there's procedures and numbers and lists
and words and sentences and all those things um and by the time where it apply
that's what we have we have values rather than the Expressions that produce them so we can just call SDK Supply and
it'll all work because args has already been translated from the actual argument
Expressions to the actual argument values so we're giving apply the right thing the second case is is this a
Lambda expression because when we saw a Lambda expression we returned whoops
how' I do that sorry we returned X itself as the
value and so it's a Lambda it's a a list that starts with Lambda and then the
parameters then the body so now what I do here why did I get louder over of a sudden I don't know have I been have you
been not hearing me all this time is that why nobody's hands are up anyway
okay this again is exactly what we saw in the tiny
version we call eval on the result of substituting the actual Arguments for
the formal parameters in the body our version of substitute takes an extra fourth argument which is given here as
an empty list and what that's going to be is a list of variabl that we shouldn't substitute for because we're
inside a Lambda that's inside a Lambda that funny case that I talked about over there don't even think about that never
mind how substitute works because it's not part of the real scheme what you should understand from apply one is that
an STK procedure is a scheme one primitive and that Lambda expressions
are how we represent scheme one non- Primitives okay if it's a
primitive then and we have STK call it if it's a Lambda created procedure we
evaluate its body after substitution okay the rest of this code is sort of
data abstraction a little bit and then substitute which is a big mess and then
at the end of this code there are some examples of using it because um since we
don't have Define uh if we want recursive procedures like factorial um we have to
make them using the Y combinator which was the answer to the extra for experts
about how do you do recursion without Define um you don't have to do that
necessarily if you're doing non-recursive things then you can do it all very straightforwardly okay sorry
for running over so you Wednesday of next week and you do have lab Tuesday or
Wednesday