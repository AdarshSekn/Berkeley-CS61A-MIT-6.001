Transcript


okay good afternoon um welcome to chapter
4 um you'll recall maybe you'll recall that the name of the course and the name of the book is structure and
interpretation of computer programs and uh we've done the structure
part and now we're starting on the interpretation part um so what is a
computer program look like and what does it mean and now we're looking at how is a computer program understood by the
computer um first the administrative stuff um I understand there's a midterm
two days from now um it will be the same place the other
ones were um there's a group part that comes first and then the individual part
question zero same as the last two times hope everybody gets it this time and
um you're allowed three pages of notes sort of one page per chapter you know
added it on um and if somebody left a YWCA Shadow Day t-shirt here it's over
there um and uh Saturday is Cal day um
for those of you who haven't experienced Cal day before people from all over come to visit and we have a bazillion
different events for them and one of the events that we have um is a scratch lab
for kids um and we'd love to have volunteers to help run it um I guess
especially those of you who are cs10 alumni and therefore no scratch um but
it's not hard to learn scratch if you understand scheme so you can volunteer
anyway um
okay so the big uh topic this week is
the metac circular evaluator um that's a big name
um which I'm not sure I understand even yet I understand the circular part uh
because well no there's two kinds of circularity involved maybe that's why it's called metac circular one kind of
circularity is a mutual recursion which you've seen before in
the calculator program and the scheme one interpreter which is the mutual
recursion between a Val and a Ply so that's one kind of circularity and the
other kind of circularity is that it's a scheme interpreter written in scheme
um we could use a different programming language write in you know an interpreter for python or something but
um there's two reasons why scheme and scheme is a good choice one of them is scheme is the only language that we're
sure you all know um and the second one is as you'll see
scheme is a really really easy language to write an interpreter for um it's probably the easiest one
there is so there's this picture on the board here which I may have shown you I don't
remember when we were talking about scheme one but on the left we have a function
machine so it has an input Hopper and an output shoot and it's the function X
maps to 3x + 7 and I put a five in at the top and I turn the crank and out comes 22 just like you learned about in
Middle School probably um and what's on the right is something really different from
that it's a machine that has two inputs uh the the right input is data just like
in the first machine but the left input is program so it takes a
machine as input and this machine is a universal
calculator it can calculate this one on the left calculates a particular function the one on the right calculates
any function because you find a way to encode the function you want in a form
that we can present to a computer um in our case that's a scheme program so we
would write Lambda ofx um plus time
3x7 and that's an encoding of this machine which we can use as an input to
this um machine that uh following the textbook I've represented using a
yinyang symbol um yin and yang are um a mutual
recursion that's why there's a little dot of Yin and the Yang half and a little dot of Yang in the Y half
um and that is supposed to remind you of the the mutual recursion between eval
and apply um and this machine is a universal machine and um let me remind
you that this idea of universality is the thing that made the
modern computer Revolution possible that long long ago we had machines that could
compute particular functions so back in the days of AR medes they had very
complicated machines full of gears and things and you would turn a crank and see all the planets
rotating um but it's not until the 20th
century that we had the universal calculator despite certain sort of false
starts like babbage's famous uh machine that was a kind of universal calculator
but he never got it built um basically because he didn't have electronics and it's too hard to do mechanically um but
today we have Universal machines and that's what makes it possible for people to build new
Computer Applications really easily you know you can sit in your back room and program
up a new invention um so it's a really really important
idea and that's why it's important why you understand this notion of interpreting a program and of course
there are lots of levels of understanding of that when you get to 61c you'll learn how the actual Hardware
carries out the tiny little instructions step by step that make this all possible
but what we're doing is at a higher level of abstraction understanding how you can write a program that understands
computer programs okay um
up on the screen is a little one
screenful scheme interpreter and this is the whole thing except for a few subprocedures uh and
the few subprocedures take up you know the first half of chapter 4
um and to understand this you look at the little binary tree over there
representing the four kinds of EXP Expressions that exist in scheme um and again this is typical of
um any programming language really so the first kind is um something that's
self-evaluating um the canonical example is numbers but also number sign T and
number sign f are self-evaluating um and there are a few
more things more obscure ones that we haven't really looked at um
next kind the other kind of atomic expression Atomic is just the opposite of list something that isn't the list uh
the other kind of atomic expression is symbols a symbol is something like hello
or X or Pi um and symbols are the names of variables and so we evaluate them by
finding out the value of the variable um and then there's two kinds
of list expressions and which kind it is depends on the car of the list so if the car of the list is
a keyword that is to say it's one of the words Define Lambda Z bang if
cond what I miss Define class I guess if you load the object system in
um and or thank you uh those are the keywords that name special forms and
there's fewer than a dozen of them um and again every programming language
has something like this special syntactic forms they usually don't look so much like procedure calls you can see
that you know they have braces in them and things like that um and in scheme a list that is not a
special form is a procedure call um the difference between a
procedure call and a special form for our purposes the basic difference is
procedure calls are valuated using applicative order which means what hands
up you can tell me what applicative order means
yes the arguments are evaluated first yes so we start by evaluating all the
sub Expressions all the elements of the list and then we actually call the
procedure with the argument values as its arguments um a special form is uh
essentially normal order the special form gets to see not the values of subexpressions but
actually what you type the the sub Expressions themselves that you typed in and the special form gets to decide
which ones it's going to evaluate in which order and so on
um and that's it that's the language okay so as in the two previous evaluators
starting with the calculator one there are three main um procedures
here there's um the read Val print
Loop it says print the prompt um read an expression from the
keyboard or whatever from a file maybe um and then eval that
expression and in scheme one it just said eval read but now with the
environment model we know that you have to evaluate an expression in a particular environment and for the ones
you type in at the scheme prompt it's the global environment always so we eval
whatever you type in the global environment print the result of that and then Loop so readal print Loop
reppel um
eval the structure of eval is a cond um because there are four kinds of
Expressions um so eval takes two arguments an expression X and an environment and we don't know yet what
an environment looks like um if the expression is
self-evaluating then we don't even look at the environment the value of three is always the same no matter what
environment we're in so we just return x if x is a
symbol then we look it up in the current environment so this is where you have to
understand what you learned um at the beginning of chapter 3 in the
environment model that an environment is is a sequence of frames so the current environment
consists of the current frame the one we just created for this procedure call and
that frame points to another frame points to another frame and eventually at the end you have the global
environment everything indirectly points to the global environment um which doesn't point to
anything so an environment is a sequence of frames we start in the first frame
and look for the variable if we find a binding that's it if not we go to the next frame and so on until either we
find a binding or we run out of frames in the latter case it's an
error um so if it's a special
form which we tell by looking at the car of the list at this point it's got to be
a list um if it's a special form then it says here do special form
um that's the big hand wve in this procedure that makes it makes the whole thing fit on a screen when we look at
the real code in just a bit of the metac circular evaluator there's a clause like this for
each special form so it says is this an if expression then eval if
xn is this a defined expression eval definition xn and so
on um so each special form has its own rules
different from all the other ones else if it's not any of those things um
then it's a procedure call actually
um this is a 61a style don't do any error checking approach it could be
something that's not a valid expression maybe you typed in close parenthesis
or something or maybe you typed in
um a vector not a quoted Vector just a vector you said number sign open pen 567
Clos pen which a vector is not a valid expression in scheme although some
scheme dialects um treat them as self-evaluating that's not part of the
standard uh you can't really do it so really we should say um instead of this
else we should say is it a list um and if so treat as a procedure
call else error invalid expression but we don't do any error
checking here so what happens here in this else these next two
lines are really The crucial thing in the metac circular evaluator which is
how we evaluate a procedure call so how do we evaluate a procedure call
the first step before we do anything else is we evaluate all the sub
Expressions so right here we're evaluating the first sub
expression and that's the one that's going to tell us what procedure we're calling
right now more than half the time that expression is just going to be a symbol
which is the name of a procedure that we defined earlier either it's a built-in primitive procedure or you defined it
earlier on so evaluating the car of X will boil down to looking up a symbol
which will turn out to have a value probably in the global frame but sometimes what's in here is a Lambda
expression or maybe it's a call to a procedure that you defined earlier whose
value is a procedure whose return value is a procedure but one way or another
the value of this thing it better be a procedure and
here is where we're evaluating all the argument Expressions okay so cter exp is a list
of all the argument expressions and this map is going to turn that into a list of argument
values I don't mean turn into as in m I just mean create a list of values
corresponding to that list of expressions and how do we do that we evaluate each subexpression in the
current environment in so we can't just say map eval could or X the way we could
in the scheme one interpreter because eval now takes two arguments map wants a
function of one argument namely the subexpression E and so we have to say Lambda of
subexpression evaluate that sub expression in the current environment okay having done that we've
now evaluated everything now we can call apply and it's apply's job to call the
function on those arguments so this map here this one is
what tells us that scheme uses applicative order right because we evaluated the
Expressions before going to apply app apply takes a procedure and a list of
argument values as its two arguments so in the
world of apply and this is important to understand there are no Expressions so this thing that says proc
this isn't an expression whose value is a procedure it's not for example a Lambda expression it's a procedure which
is its own data type and a procedure isn't something you can type in to
scheme you can't have a procedure as an expression procedures are the values of
some Expressions um and then args is a list of the actual argument values whatever
they are so these aren't Expressions either these things are you know whatever they are numbers or lists or
who knows what um but they're values so there's no
evaluation of proc or args they've already been evaluated so apply doesn't
know about the notation of scheme at all all it knows about is the semantics of
what it means to call a function with arguments well what does it mean there
are two possibilities so any procedure that we have is either a primitive procedure or
what the book calls a compound procedure which is one that we created with
Lambda primitive is the ones that are built in compound is the ones that were built with Lambda if it's
primitive uh and this is one of the cheats here um we call it by
Magic uh what that really means is that um in a real scheme system A Primitive
will have been translated into machine language into the you know ones and
zeros stuff that computers actually know how to carry out uh so what we're doing
is calling that little chunk of machine language code um is the way we really handle Primitives um how did I get up
there oops ah
wait let's try this
again okay uh other was oops here we go if it's a compound
procedure one that came from a Lambda expression one of those things with two
bubbles then how do we evaluate it so as always you have to read this from the
inside out when you have a a composition of functions like this so before we look at eval we're going to look at these
inner expressions and one of them is pull the procedure body out of the procedures that's one of the things in
the left bubble is the procedure body and that's a scheme expression
right so that's the way in which Expressions sneak into apply we're not giving it Expressions as arguments but
inside a procedure if it's a procedure created with Lambda there's a procedure
body which is um an expression or actually a sequence of Expressions
really um so this should say eval sequence um but this is the short
version um the second argument to eval is this thing called extend
environment um so we're creating a new environment that's what procedure calls
do and the way how do you make a new environment remember back a month ago
you take the formal parameters which come from the left bubble of the
procedure and you take the actual arguments which was were given to apply
as an argument and you pair them up so if we have three formal parameters we should
have three actual arguments and we make bindings for each of those and that's a new frame and then we use that frame to
extend an environment what environment do we extend okay so here's another important
little detail this does not say EnV in fact apply doesn't know anything about a
current environment what apply knows about is
the right bubble of the procedure inside of proc proc EnV is a selector proc EnV
and formals and body are three selectors for the abstract data type
procedure so now we're pulling out the environment from the right bubble and saying that's the one we're going to
extend so the procedure tells us the environment in which it was created and
that's the one we extend what's the name for that that choice of environment
yeah lexical scoping yeah what's the alternative Dynamic scoping and what
does that mean what's Dynamic scope me
yeah yeah you extend the environment in which the procedure is called so if we wanted to do Dynamic scope apply would
take another argument which is n for the current environment this would say extended environment formals proc ARS en
that would be dynamic scope lexical scope the procedure tells us which environment to extend namely the one in
which it was created okay so what I'd like you to see is that
I'm telling you again in a different form what you learned a month ago about the environment
model you know we had pictures on the board with bubbles and boxes and arrows
all over the place this is an implementation of that that it's exactly what it
is um so I hope that having seen the
environment model will help you understand the metac circular evaluator and also conversely seeing the evaluator
will pin down for you maybe um how the environment model actually
works um I would like you to remark upon the
tininess of this code
now in saying that I'm cheating a little bit because I haven't really handled the special
forms okay and each special form is you know half a screen full of code so by
the time we're finished it's six or seven screen FS instead of just one um
and I haven't shown you how to look up a variable in the environment although
that's pretty straightforward if you know that an environment as a list of
frames um then it's pretty simple for you to write look up in environment
supposing that you have look up in frame as a helper
um but that's basically it oh I'm sorry I'm also cheating a little bit because I
didn't show you read re is actually hang on a sec re is actually a little messy and ugly
because it's dealing with individual characters that you typed it says oh look this character is an open
parenthesis so I have to do blah blah blah this character is a space Etc
um so it's messy but it's intellectually trivial you could write it if you really had to yeah
okay let me try to restate your question both so other people can hear it and to
try to clarify it for me too um when you first learned about the
environment model uh it was presented to you as being
necessary in order to achieve the way we want scheme Expressions to mean what
they mean and in particular um once we introduced mutation into the language
which we did with object-oriented programming it no longer works to say we
just substitute uh values into the body um because the value of a variable
might change halfway through the body so as a consequence of that and as a
consequence of wanting things to be lexically scoped we had to invent this environment model and that's
true now you're seeing the same environment model presented as a
consequence of the way the language is implemented and both of those things are
true um this this is an instance of a general
point that I'll be coming back to at the end of the semester which is in
everything we do in computer science there's a whole bunch of levels of abstraction and at any given level if
you're being an engineer at a particular level what you do is constrained both by
pressure from above you so sort of the needs of the higher levels of
abstraction that they're telling you about out and by pressure from below namely how your level is
implemented okay so what kinds of facilities are available for the implementation of your level and that's
exactly what you're expressing here that you can actually see it both ways if you look at the actual
history of the way this developed
um first there was Lambda calculus which was was an entirely theoretical model
for use by mathematicians and not as a computer programming language it was an attempt
to rest the foundations of mathematics on the idea of function sorry rather
than the more usual treatment in which everything is based on set theory so that was a thing for
mathematicians um then John McCarthy wanted to have a programming language in
which to make assertions about programs among other things to do
artificial intelligence research and he you know came across
this Lambda calculus that Alonzo church had invented and said we can use this as
a programming language um so he took the notion of Lambda came from Church's work um and he
defined a not very good
notation for representing that to a computer
um and then the notation kind of got refined the language hadn't been implemented yet and then one of his grad
students Steve Russell uh said you know if we represent programs this way I can
write a really simple interpreter for it in itself he had started out trying to write a lisp interpreter in one of the
previous languages that existed then which basically meant Fortran um and
everybody was finding that impossibly complicated and Russell had the idea let me try writing a lisp interpreter in
lisp and um he came up with basically
this but a little bit different because they hadn't yet thought about scoping
rules um and so they ended up implementing Dynamic scope which turns
out to be the thing that you naturally invent um if you don't think about it very
hard and I'll be talking more about scope in a bit um probably
Wednesday um and then um people started writing
programs in this language and we're having certain problems because of the use of dynamic scope and so there was a
lot of you know there was five or six years worth of research papers on how to
solve this problem and then and finally they invented lexical scope which
footnote is what Alonzo church had in mind from the beginning so if they had read Church's papers more carefully they
would have gotten there directly but they didn't so there was this back and forth between what the implementers implemented and what the users needed so
the actual history of it is very complicated but you don't have to
recapitulate that history you have the benefit of all that earlier work and so you can see you know right from the
beginning um what kind of the right answer is to these design questions
um I'm not when I say the right answer um I'm not making a claim about the
superiority of scheme over whatever your favorite language is uh I'm just making a claim about the superiority of scheme
over the lisp of 10 years ago or 20 years ago um
so yeah this is exactly the same thing that you learned before and it had better be the case that what we
Implement is what we needed right um so you can view it as the needs
giving rise to the implementation or the implementation giving rise to the behavior and they're both true um that's
an example of what we call a dialectic where you have two kind of opposite things that determine each other it's
another example of circularity in a way okay we
ready all right um so I I'm telling you about the parts
we're leaving out so we left out do special form we left out look up an
environment um we left out extend environment but that's totally
straightforward you could have written that in the first well as soon as you learned about lists on the fourth week
you could have written extended environment um and uh we left out read and we left out
print which is slightly messy not quite as messy as Reed um and most important
of all we left out storage allocation um so when you say map and
inside Map There's a cons how does that cons actually happen that's something we
have not discussed at all it turns out to be um probably the most complicated
piece of the whole system and you will learn about it I believe in
61b but maybe it's 61c they keep going back and forth on this I think
61b okay
um oops
where am I
here all right um oh yeah something for you to think
about you can write an evaluator for any language in any other language
okay they're all completely equivalent in power in the sense of what can we
compute with them they're not equally equivalent in expressive power which is how easy is it
to say what you mean but they're all equivalent in terms of what we can compute
so if I were to say I want my class my introductory freshman computer
programming class to write an interpreter and I want it to be
easy you might imagine that the thing to do would be to give you a very powerful
implementation language like say Ada which is a language that has everything under the
sun in it um or maybe Java you know which is semi everything in it um as the
language that you write The Interpreter in and some really trivial language like
say basic language they used to use on 8bit microcomputers um as the language that
we're implementing so maybe writing a basic interpreter in Java would be the easiest possible interpreter assignment
turns out not to be true turns out the easiest interpreter in the world is a
scheme interpreter written in scheme that seems paradoxical
um because I'm saying on the one hand scheme is the simplest language that there is and on the other hand scheme is
the most powerful language that there is to write an interpreter in and how can it be both the simplest and the most
powerful that's one of the hardest ideas uh for you to take away and the reason
for you to take it away is not so that you become scheme Fanatics um that's not my goal at all
I'm a scheme fanatic but you don't have to be um I would like you to be a Simplicity
fanatic okay I would like you to understand that just as in you know
mechanical engineering or civil engineering or anything else the best solution is the simplest
solution not the most complicated one with a lot of bells and whistles um and that turns out to be
true in programming languages also so if you ever find yourself designing anything like a programming language
and most of you are probably not going to be designing general purpose programming languages but you might well
be designing special purpose programming languages like the language that the
user of some game uses to say how to move next that language might be defined in
terms of gestures with a joystick or something rather than stuff that you type but it's a language it's a special
purpose programming language and if you find yourself designing one make it simple and the way to make it both
simple and Powerful is to have powerful ideas in it like for example but not
only Lambda okay um so scheme is a simple
language because it has a very uniform syntax so all those parentheses that
everybody complains about when they're first introduced to lisp um they have an important purpose which is you don't
don't have to understand anything about the meaning of a program to understand how to divide it up into chunks the
dividing up has been done for you by the parenthesis
um and the other piece of the well other piece of the Simplicity is that that
notation with all the parentheses is both the notation for programs and the
notation for data that's how we represent lists okay if we had a notation in which
programs were full of parentheses and quoted lists were full of square brackets instead that would make our job
harder because we wouldn't be able to take a computer program and view it as
data easily but as it is after Reed has done
its work um the program that we see actually isn't full of parentheses it's
full of box and pointer diagram because that's what Reed gave us Reed is the
thing that translates the characters you type those parentheses and things into box and pointer
form and then eval is the thing that takes that structure of boxes and pointers and assigns a meaning to
it um and then thirdly it turns out that
having a language in which procedures are first class uh makes writing an
interpreter really easy especially as we get into the more advanced variant versions of the evaluator you'll see
that okay
um oh yes now I have to pull out my glasses so I can read
this I'm going to quote to you um a piece of the instructor's manual
on the subject of data abstraction in the evaluator so it's concerning section
4.1.2 which is about exactly how to represent uh expressions and
environments uh as you know list structure so 4.1.2 point out I should point out to
you that this section is boring as has as much of section
4.1.3 and explain why writing the selectors constructors
and predicates that Implement a representation is often
uninteresting it's important to say explicitly what you expect to be boring and what you expect to be interesting so
that students don't ascribe their boredom to the wrong aspect of the material and reject the interesting
ideas for example data abstraction isn't boring although
writing selectors is so in other words the idea that you can have an abstract data type like uh a procedure say where
we have these selectors body and proc en and
formals the fact that we can have such a representation is interesting the
particular writing of you know formals equals CER and body equals cator and
whatever uh that's boring the details of representing
Expressions as given in 4.1.2 and environments in 4.1.3 are mostly boring
but the evaluator certainly isn't okay um I actually think uh this
is one of the few places where I disagree with aelson and Suman I think they go a little overboard on data
abstraction so in the evaluator there are many different abstract data types
that are sequences of some particular kind of thing in the same way that a
farist is a sequence of trees and they do a separate abstract
data type not just for the underlying element types but for each sequence type
so there's an abstract data type which is the sequence of cond Clauses in a
cond expression so there's a select our first con clause and rest of con
Clauses and the same thing for environments there's a selector first frame and a selector rest of frames and
all those things are just car and cutter because whenever you have a sequence of things a linear boom boom boom boom boom
sequence car means the first one and cter means all the rest of them and if
it were me I would have I would have the abstraction for a frame or a con clause
but I wouldn't have a separate abstract data type for each of these sequence things so I think they make it more
boring than it has to be by doing that um okay
um the next thing on the agenda is really to teach you
logo uh because in Project 4 uh you're going to write a logo interpreter you
start with the Met circular evaluator and turn it into an evaluator for a whole different language um but we only
have a few minutes so I'm only barely going to get started doing this
um okay welcome to logo um you can play with logo in the lab uh
let me start by showing you the most important thing which is how to get out of it you say
buy okay so that how you get out um The Prompt is a question mark That's
how you know you're talking to logo and not scheme and um in
scheme every expression returns a value every procedure that you write
returns a value in logo we distinguish certain procedures that return values
from other procedures that don't uh and this is true in a lot lot of different programming languages right if you learn
C or C++ or Java or python or any of those some procedures that you write um
return values and others don't if it's the languages in the C family they very
confusingly use the name function both for the ones that return values and for the ones that don't return values um in
logo the ones that return values are called operations um or more recently sometimes
reporters uh the ones that don't return values are called commands so in scheme if I say three the
answer is three and Logo if I say three I get an error message you don't say
what to do with three now the error message does tell you the value so I can say um some to
three and I get you don't say what to do with five what it wanted me to say is print sum 2
three because print takes one input prints it and returns nothing and a
complete logo command is something that does not return a value so if the thing you call a top level does return a value
that's an error um uh you will have notice that
um this looks a little schemel likee in that it's a prefix notation where the procedure comes first but it doesn't
have parentheses around everything um as you'll see when you're
writing the evaluator that makes things a little complicated because you have to know how many inputs every procedure
wants so I can say something like you can abbreviate print to PR if you want
um some product 2 3
4 Okay so think about what the value that should be printed is well you actually do know the
answer I hope that's the answer you got um but in order for this to work the
logo evaluator had to know the product takes exactly two inputs okay now in scheme product takes
any number the asterisk their times takes any number of inputs and actually you can do that in logo too I could have
said print
sum product to 3 4 like
this and get 2+ 3 + 4 or
print sum product
234 we get 24 so you can make it do the same thing scheme would do with
parentheses and we use them in the same way namely an entire procedure call inside parenthesis but you don't have to
every procedure by default takes a certain number of arguments print takes one sum and product take two each if you
don't put parentheses in
um a big departure is that I can also say print 2+ 3
um gr 2 * 3 +
4 and notice by the way
um that actual logo knows the rule that you learned in elementary school about
multiplication before addition the one that you write isn't going to be that smart um it's just going to go left to
right um this is a um
compromise right infix notation is really problematic because of this
question of Precedence how do I know which to do first when I see two operators like this it's not a problem
with prefix notation prefix notation makes it clear which one you want to do first namely the inner one um infix
notation doesn't make it clear and that's why people throw in parentheses sometimes to say like print
uh 2 + 3 times four if that's what you
mean uh you use parentheses for grouping because of the ambiguity of infix operators so infix
operators are ugly hard to deal with for the computer uh not that easy to deal with for human beings if you can
remember back to third grade um but it's what everybody's accustomed to so we
compromise do and let you use it
um 3:00 okay we'll continue this next time
UC Berkeley