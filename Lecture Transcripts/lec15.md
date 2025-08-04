Transcript


and you wouldn't okay good afternoon
so today is actually if it is sort of part of last week we're still on the
topic of trees in a way I'm on page 306 in the reader if you want to follow
along we're gonna be talking about the scheme one interpreter it's a little
scheme interpreter so there's this progression from the calculator that you
saw a week ago that only does arithmetic and doesn't have variables and now we're
going to look at one that implements the substitution model that you learned about back in Chapter one and then when
we get to chapter four comes the sort of real sort of full strength the way
scheme really works meta-circular evaluator and the reason we're building
up to it is that traditionally students have found the meta circular evaluator hard you know chapter four is said to be
a lot harder than everything else in the course and so we want to get you
prepared gradually for it okay so why
write a scheme interpreter and scheme anyway what's the point of doing that it seems a little weird because you can't
run it unless you already have a scheme interpreter to run it on so why not just use that and there are four reasons one
is having an interpreter to look at to read the code of helps you understand
the model of evaluation so when we say something like scheme uses applicative
order that you learned back in the first week or scheme uses the substitution
model evaluation there's something like that you can really understand what those things are saying by seeing in
detail written out what that means so we're going to be doing that today
second thing is it lets us experiment with modifications to scheme so when we
get to chapter 4 we start with the scheme interpreter and then in the book there are three different and modified
versions of the scheme interpreter that we're going to look at and see how we can change the language by changing not
very much in some cases of the code of the evaluator and why you might want to
make those changes or might not a third point is that even real industrial
scheme systems are largely written in scheme typically there'll be a tiny core
of things having to do with storage allocation that are written in some lower level language like C or Java or
something and then most of the work of being a scheme interpreter is written in
scheme using code that's not so different from what we're going to be doing so this really is how it's done
and there's this bootstrapping process where you know you use some other
interpret or some other system to get going in the first place and then you sort of use your own interpreter to
interpret the scheme code that's part of the interpreter so this is not so
unrealistic what we're doing and lastly looking at an interpreter for a
programming language any implementation of any programming language conveys one of the big big big ideas of computer
science which is universality so I want to start even though it's kind of abstract and up in the air by talking
about universality which is what this picture is about on the Left what you
have is a function machine you probably saw these for the first time in algebra 1 in 7th grade or 8th grade or something
and there's a crank on the side of the machine and you put in numbers and other
numbers pop out the bottom so this is X maps to 3x plus 7 and I put in 5 and I
got 15 plus 7 which I hope is 22 and that's a machine that computes a
particular function machines like this
have been around for 2,000 years that I know about
the ancient Greeks had machines like this that computed particular functions
they used them for things like showing all the heavenly bodies revolving around
the earth back when people thought that and also for navigational problems and
so on so so machinery to compute particular functions of Venus has been around forever but the thing that made
possible the computer era that we live in where you have things like iPods and
GPS and all of these myriad computer devices is going from this model where a
particular problem is built into your machine to this model where there's a
universal function in the book in chapter 4 when we do the meta-circular evaluator they use the yin-yang symbol
to represent the meta-circular evaluator because it does mutual recursion as
we'll see shortly and this universal function takes as its inputs first a
description of a machine so we take this machine we make a description of it in
some programming language like we say lambda of X plus times X 3 7 or the
something equivalent in other languages and that goes in here and then whatever data you want as inputs to that function
and crank crank crank and out comes an output so you only have to build one machine that can do anything so the
thing that's new in the computer era that started oh maybe 70 years ago now
is the notion of a general-purpose computer where the action that you want
to do is just represent it as data just like the numbers you want to work with
are represented as data in the machine and that was a huge idea we've seen that
idea before that's what lambda is when we did higher order
functions we were taking programs actions descriptions of actions and
using them as inputs to other functions like map and filter and so on and that's
the idea of universality so programming languages are a piece of that and it's an important reason for
studying something like an interpreter ok well I should say a programming
language is the software version of this idea it's it's this idea in hardware
that started the computer era but also pretty shortly after that people started
inventing programming languages so instead of having to represent your problem in the language that the machine
knows you can use some more abstract language and that contributed to
universality in the software arena so it's writing one program that
knows how to do any computation that's what an interpreter is ok up on the
screen is the one screen full version of a scheme interpreter and first thing I
want you to notice is that it looks a lot like the calculator program you saw
last week the calculator program had three parts and here they are the first
part is the read eval print loop which basically hasn't changed and the second
part is eval takes an expression which is a piece of text in the programming
language and return is the value of that expression and then finally apply which
is out of the realm of what the programming language looks like so there's no expressions in here apply
takes a procedure and argument values and calls that procedure with those
arguments and returns the value that that procedure returns and those are the pieces of if you sort
of step back and squint any interpreter for any programming language basically has those pieces this is one reason why
lesbians like to say inside every language there's a little Lisp hiding okay so what kinds of expressions are
there in the calculator program let me just remind you an expression was either
a number or it was plus minus times
divide expressions so expression is
defined recursively because these spaces can be filled in with any expression but
those are the only kinds of expressions that there are in the calculator program in scheme we divided up expressions into
two kinds and then each of those into two kinds so an expression is either an
atom or a list now that's sort of a tautology because the definition of atom
is something that isn't a list or more precisely something that isn't a pair so
something in scheme that's built up out of pairs but isn't a list is not an
expression there's no category for improper lists or you know dotted pairs
as people say now there are two kinds of atoms they are self evaluating so that's
numbers same as in the calculator program are self evaluating evaluating but so are for instance hash t and hash
F for true and false the value of hash T and scheme is hash T and so are strings
in double quotation marks our self-evaluating and there are a couple more things that are
self-evaluating and symbols which are
the names of variables that's an ad
sorry I have lousy handwriting what can I say if an expression is a list there
are two kinds and they are procedure
calls and special forms so it's a
special form if the car of the list is a keyword keywords are the names of
special forms there are things like lambda ends up define an if and cond and so on so if the car of a list is a
keyword then the list as a whole is a special form that has special evaluation rules otherwise if it's anything else it
has to be a procedure call so in my
evaluator my tiny evaluator I say well if the expression is self-evaluating
then just return X the expression itself that's what self-evaluating means if
it's a symbol then we just look it up and in the substitution model we're
never going to get to eval with a symbol as the expression unless it's a global
variable because local variables the ones that are formal parameters of procedures get substituted out before we
do the evaluation you'll see that in a bit so it's look up in a list of global
variables this variable name and get the corresponding value if it's a special
form that is if it's a list and it's car is cond if lambda define then do special
form each special form has its own rules for how to do it
otherwise it's a procedure call and so what do we do we call apply with two
arguments and here's where it really gets different from the calculator
program in the calculator program what we gave apply was the name of the
function we gave it the symbols plus sine minus sine asterisk slash but here
we don't do that we eval the the car of the list the operator the thing that
says what function to call and the value of it has to be a function and most of
the time car X is just a symbol which is the name of some procedure we said
either we're calling a primitive procedure like you know square root or something or we defined a procedure and
we're using the name of that defined procedure as the car of the procedure call sometimes though it'll be a lambda
expression or call to some function that
generates lambda expressions like my composed function that I showed you back when we did higher-order functions that
returns a function so you can say open paren open paren compose blah blah close
paren and then call that with an argument close paren again so whatever
it is we evaluate it and that tells us what procedure we're calling and then we
map eval over could or X could or X is any number of arguments starting from
zero so this doesn't say quatre which would be the second element of the list
it says cooter which means everything but the procedure that we're calling so
we map you Val over those things and that gives us a list of argument values
right here where the cursor is blinking this is why scheme is applicative order
because remember what applicative order means it means that we evaluate sub expressions
argument sub expressions before we call the procedure and what we give the procedure is
the values of the arguments the actual argument values not the actual argument expressions as opposed to normal order
if we just said could or expir we'd be doing normal order we'd be giving apply
expressions rather than values but we
don't so schema is a blicket of order okay now how does apply work well there
are two kinds of procedures right there are primitive procedures built into
scheme and then there are the ones that you create with lambda expressions the
book confusingly I think this is one of the few things I don't like about the book uses the word compound for two
different purposes so a compound procedure is their name for procedure
you created with a lambda expression including the implicit lambda expressions in define with parentheses
and let they also use compound to talk
about compound expressions atomic expressions and compound expressions
which means that it's a list that we're evaluating so compound expression versus compound procedure they mean two
different things so I try to avoid using the word compound for either of them so
I'll talk about lambda created procedures or defined procedures for
that and list expressions for that okay
so there are two kinds of procedures the ones that are built-in and the ones that you create with lambda so now if it's a
built-in procedure that we're calling it works by magic do magic
what does that mean well it means what really happens in a real scheme system
is that the primitives are written in
machine language or they've been compiled into machine language and so when we call
primitive we actually are doing a computer or machine language call to
something that's in its own native language you're gonna learn all about machine language by the way in 61c a
year from now probably for most of you a
semester from now if you take me over the summer so we're not very interested
in that part of the evaluation process so I refer to it as magic what we are
gonna do in our scheme interpreter is written in scheme is cheap slightly and
use the primitive procedures provided to us by the underlying scheme so we just
inherit Khan's car code are plus minus square root all of those things from SDK
if we wanted to we could go right each primitive procedure in scheme in terms
of other procedures that have to be a few things that were given at some point you can't write everything in terms of
something else so you never get the job done but we could write a lot of the primitive procedures but there's not much point in doing that you wouldn't
learn anything really from looking at well how did we do plus although
actually a little bit later this week we're going to talk about some aspects of how we do plus but that's not what's
so important what's important is the evaluation process rather than the
primitive procedures so we're just sort of pushing those under the rug but we aren't pushing under the rug the
evaluation of calls to lambda created procedures and in the substitution mount
model what the substitution model says is we call substitute with three
arguments the body of the procedure which is an expression that perhaps uses
its arguments the formal parameters as part of that expression second argument
to substitute is the formal parameters of the procedure so these first two
things come from the proceed itself formal parameters remember are the names for the arguments and then
args which does not come from the procedure it comes from this expression
that we're evaluating where we said what actual argument to use so these are actual argument values and what
substitute is going to do is go through the body of the procedure and wherever
it sees an instance of a formal parameter it will replace that with the
corresponding actual value okay now the
result of that is something that looks just like the body except it doesn't
have any local variables in it so if we say define square of X to be
times X X okay and now I say square five
or what's actually not say Square five let's say just to make it totally clear
square of plus two three back in eval
this plus two three got evaluated the value of it is five and so what
substitute does is it takes this body right here and turns it into or makes a
copy of it that says times five five and now that's an expression that doesn't
have any local variables in it so we passed that as an argument to eval this
is a variable this asterisk is a symbol it's no different from the symbols made
out of letters except that there's a binding for it there's a value
associated with that symbol when you start schema namely the primitive multiplication procedure
so when eval eval is this expression it gets to that place where it says eval
car X and car expose an asterisk so we go through eval recursive
and we get the multiplication primitive so that's the first argument to apply
and then the second argument to apply as the list five-five when we do the multiplication
okay so this happens by magic but the invocation of square wasn't done by
magic it was done by substitute you actually wrote a substitute for homework
a week ago two weeks ago you remember
anyway so you've written substitute so you understand how that works your substitute isn't quite complicated
enough I'll show you that when we get to scheme one there are some tricky things
you have to think of that but basically what you see on the screen here is a
scheme interpreter and it you know fits
on a screen now the reason it fits on a screen of course is that I left out a
lot so things like lookup global value and do special form and substitute all
have to be written and when you put in all those things it gets longer so when you look at the actual code it'll be
pretty long so one of the skills you have to learn if you haven't already is
how to read a large program and basically you do that by taking on faith
every part of the program that you're not focusing on right now so and we do
this when you're looking at what's on the board here you want to know how apply works you just take on faith that
substitute does what it's supposed to do you also take on faith body and formals
which are selector procedures for the procedure abstract data type so in this
program there's going to be a data type called lamda created procedure and
another one called primitive procedure and lamda created procedures have the
selectors body and formals that pull out the pieces of that procedure okay so
what you don't do you resist the temptation to go look up body and figure
out how that works you just say okay I'll do that later for now I'm taking all that on faith because I want to
understand apply that's the trick to understanding a large program is you just believe every part of the program
does its job except the part you're looking at and that's where you focus your attention all right so now here's
the actual scheme one program I should show you how it works do you say load
so what I'll see ya 61 a slash lit 61 a /lib slash scheme 1 you spell it right
it works better that way so it's ok and
you say scheme - 1 and you get the scheme 1 prompt into it you can type
expressions like + 2 3 or I am - x times
X X apply it to 5 and so on
so that's schema one we want to leave scheme one all you do is you type something that isn't a valid expression
like that and you get an error message and you're back in SDK okay so here's
the read eval print loop as in the calculator program there's this call to
flush here which just says even though I haven't printed out a newline character
actually print the stuff anyway because I want the user to see it right
now and then we have read an expression
read is also something that we get from the underlying STK so there's an SDK
procedure called read which we're using here that's the thing that takes the
sequence of characters that you typed it's full of things like digits and letters and spaces and parentheses and
goes through a character by character and turns it into essentially a box and pointer diagram for what you typed and
that's what read returns and then we call leave now of that expression except
we actually call it eval one and we also use apply one the reason for that is
that STK itself has procedures called eval and apply that you are user visible
and we don't want to override its definitions so we call it hours
something different so we Val one of read and then print whatever eval gives
us and then here's the loop part of the read eval print loop call schema and
recursively question is about the repple
so if you're a list may even everybody has a list maven knows the word repple it means this code right here read eval
print loop okay this file has voluminous
comments as you can see comments comments comments comments so you'll be
reading all that because you're going to work with this in homework and lab this
week I believe actually so here's all of
you fowl and it's a little bit bigger than the one screen version so constant
question mark that's the same as self evaluating question mark if it's a self evaluating expression return the
expression if it's a symbol then we call
eval note not eval one but eval the
reason we do this remember I said by the time we actually see a symbol in eval
it's something to evaluate it has to be a global variable not something that's
an argument to a procedure that's running and we let SDK handle our global
variables for us in particular this
means we have access to all the SDK primitives because all of the names of
primitives since they're symbols we pass on to SDK to eval for us that's the main
reason that we have global variables at all is in order to have access to the primitives so that's a little bit of a
cheat but not too much in the meta-circular evaluator in chapter 4 we
don't cheat in quite that way and then
instead of something that says special form question mark X we have a con cause
for each of the special forms that are implemented in scheme 1 there are only
three special forms and they are quote if and lambda quotes
important to get you know data that isn't self-evaluating into our system at all as I hope you know by now when you
say quote Phu the read procedure
translates this into this special form
so the quote symbol is just an abbreviation for this it's especially so
quote is a key word quote foo is a special form the value of quote foo should of course be foo which is the
Katter of the whole expression so expression is quote foo the value of
that is the Katter and that's what we do on this line where the cursor is blinking how about an if expression so
if remember takes three arguments one that's true or false and then what to do
if it's true and what to do if it's false so we use sdks if to make this
decision for us is that a problem is that a circularity are we going to get in trouble we're gonna be doing eval of
this if expression over and over again no because the expression that we're
evaluating is a scheme one if expression this expression that you're looking at
although it's part of the program that interprets scheme one this program runs
in SDK so this is an STK if you're looking at so we use SDKs if to help us
do our if but SDKs if doesn't do all
we don't just take the whole expression and pass on to STK
we can't do that because part of the job here is evaluating sub expressions and
it has to be done with eval one because their scheme one expressions not SDK
expressions but we do use SDKs if what
does SDKs if do well it always evaluates its first argument so we start by eval
warning the first argument - if Cataracs and then depending on whether that comes
at true or false we do either eval one of the Kadett err or eval one of the
candidate err seats at each told you you have to learn how to pronounce these
things and you do notice that we only do
one of these so our scheme one if has the same property as SDKs if that it
doesn't evaluate both the second and the third argument it only evaluates one of them and that's important as you learned
in the first week's homework I think there's the exercise about new if and
why new LIF didn't work if you're going to write recursive procedures you have to not evaluate the recursive case if
you're in the base case so that's why it's important that if is a special form an hour if indeed behaves correctly ok
next comes lambda this may be a little surprising a lambda expressions value is
the lambda expression itself so in a substitution model scheme we can
represent a procedure as the lambda expression because all we need from it is the formal parameters which is the
catter of a lambda expression and the body which is the katha deter CAD did
der sorry the third element of the list
we'll be the body this will not be true
when we get to the meta-circular evaluator in a couple of weeks you're going to learn about a different model
of evaluation called the environment model which is more complicated than the
substitution model and you'll see in the environment model that we can't just
represent a procedure with the lambda expression then we need more information than that but in this interpreter we can
and so we do notice by the way that
define is not one of the special forms here so in this in scheme one we can't
make definitions of new things kind of
interesting so if you want to write recursive procedures you have to do it
using the trick that was the extra for experts a while back of the Y Combinator
where you managed to have a procedure have itself as one of its arguments and
do recursion that way it's the only way to do it in this evaluator unless you invent a defined special form um okay so
if it's not quote or if or lambda expression and it is a list it says pair
question mark here and that's just because it's not a valid expression if it's a pair unless it's a list and we
don't actually bother checking because in general in this class we don't do a lot of error checking that's 61b and pair question mark is
theta of one time whereas list question mark is theta of n time so it's a tiny
optimization probably shouldn't have done it that way anyway there it is so
suppose that the expression we're evaluating is a list and it isn't a
special form in that case it's a procedure call so you've already seen
what we do we call apply one and the first argument to apply one is
eval one of the Carvey expression which is tells us what procedure to call and
that could be a global variable a lot of the time or it could be a lambda
expression the value of which is as we just saw the lambda expression itself
and then we map eval 1 over the coder to get the actual argument values so what
you see here is exactly like what you saw in the tiny 1 screen version before if it isn't any of those things it's an
error ok so then comes a lot of comments
about apply oops
and here is apply
so remember in the one screen version of apply first thing we did was test to see
whether the procedure we're trying to call is a primitive procedure or a lambda created procedure we do the same
thing here it doesn't look as if we do the same thing because it doesn't say
primitive question mark here it says procedure question mark so this is where
you have to bear in mind that scheme
ones primitives are sdks procedures anything that's an SDK procedure we take
to be a primitive procedure for our purposes so you can define a procedure
in STK and then use it as a primitive in scheme one so therefore since our
primitives are procedures of STK to call
them we can just use STK supply and again notice this is not a call to apply
1 which would be scheme ones apply it's a call to apply plain old apply which is
Stks apply this business are bad scheme one versus STK I realize it's confusing
it's going to take you some time to thank us all through its it would be a
little easier if we were writing an interpreter for some other language if
we wrote her an interpreter for you know basic or Python or something Perl if we
did that then it would be clear to you the difference between scheme code and
code in the language you're trying to interpret which would look very different here the language are trying
to interpret is the same as the implementation language they're both scheme they're a little different
because for example scheme one only has three special forms SDK has a lot
or that you know about already a couple that you don't coming up later so there are differences
but there's subtle differences whereas if we were interpreting some other language then the differences would be
much more dramatic and it would be easier for you not to get confused between using for example scheme ones
apply versus SDKs apply that kind of issue wouldn't arise for you so why
don't we do that why don't we pick some other language to interpret to make things less confusing
well because two reasons one is there's
only one language that we know all of you know okay so I don't want to have to
teach you another language just so that we can write an interpreter for it although we're going to do that actually later in the semester when you write a
logo interpreter but we picked logo cuz it's much closer to being scheme and
then some of those other choices would have been so that's coming later but for now we want to use the language you
already know it's a making simpler in that way but there's another reason too and this is really interesting so we
have in an interpreter here's the interpreter it's written in an
implementation language
and what we put into it is in some
potentially other language which is the source language and let's say you're
teaching a class like this and you want
your students to write an interpreter that's going to be as good as possible
but have it be as easy as possible to write so you want to have an interpreter for some language and you want to make
it really easy to write the interpreter okay so what languages would you pick
supposing you had the whole universe of languages available to you what language would you use is the source language in
what language you use is the implementation language it's tempting it's very tempting to say that for the
source language you really want something trivial and babyish so maybe we're going to write an interpreter for
basic because you know that's a tiny little language fits on 8-bit micros
like we used to have before you were born so let's use basic as the source language and for the implementation
language you want a really powerful language that can do anything can handle
text processing and list processing and and do all kinds of computations and and
make it possible to write an intricate program fairly simply and so maybe you
would pick something like Java as your implementation language in order to get
the easiest possible write an interpreter assignment well it turns out that that's wrong it turns out the
easiest possible write an interpreter assignment just trust me about this for
now as you as you grow and learn more languages and actually write interpreters and compilers which you're
going to do if you take 164 which I recommend it's the compilers course you
actually will do things comparable to writing come Tylar for basic in java but that'll be
much much much much much harder the easiest possible interpreter in the
world to write a scheme in scheme that seems a little counterintuitive it seems
like you want this language to be trivial and simple and not very powerful you want this language to be big and
strong and industrial-strength and can do anything how is it that these can be the same language it's because well
partly it's because of lambda which turns out to be very very helpful in
general it's because scheme is a language that can do a lot but it has a
very uniform notation you already know that all the expressions look the same
and if you've programmed in other languages you know one week you learned about the if statement which has of
such-and-such notation and then the next week you learned about the for statement which has a different notation and then
the week after that you learn about the print statement which has yet another notation and so on in scheme there's
only one notation it's parenthesis blah blah blah close parenthesis right no matter what you want to do so scheme is
a very simple language to interpret also
not only is scheme a powerful language in general but it's particularly good
because it's a flavor of Lisp which remember stands for list processing it's
particularly good at lists and what is a
scheme program it's a list the notation
for lists of data you know ABC whatever
it's just like the notation for procedure calls or anything else so
scheme has the tools that it needs to handle scheme code very easily and that
another reason why writing scheming scheme is so simple and that's the reason I promised you back in week 1
that I would tell you why the notation was FXY instead of f paranthesis x comma
y remember I promised you that this is why it's because one chunk of a scheme
program is a list a scheme list so we call eval if the notation were like this
we'd call eval with a big mess instead we call eval with 1 1 expression which
is 1 list and when we can do car and cooter on that expression so that's one
of the things that make scheme so easy and there's a big long story about the history of Lisp in the very very very
early days of Lisp when it was just an idea in the head of John McCarthy he actually used a notation that was more
like this but the reason he wanted to invent a new language was to do
reasoning about programs and so he said well when we're using a program as data
we'll write it this way and I this was called an M expression and I forget what
the M stands for and this was called an S expression for symbolic and for a long time the Lisp documentation had both of
those things in it but when he handed off this idea to one of his grad
students and said here actually you know make a lisp that works and Kretz didn't said oh god this is really hard and what
he happened upon was that there already was that tiny thing that I showed you
the one screen scheme interpreter there was a lisp interpreter like that that McCarthy had written as documentation
for how it should work and he said well if we just use M Express RS expressions
all the time then I can just use that code as a model and so there aren't any
M expressions anymore because it turned out to be so easy to do it this way okay
I have one minute
so here's substitute there's a big comment about substitute and here it is
and as you see it takes a little more than a screen full to do it all when you
read this code don't spend a lot of time on substitute because this is the part that's a lie in terms of how scheme
really works the code is a little tricky and the reason it's tricky has to do
with the following fact what if you have a procedure with an internal definition
inside it so there's the lambda inside the body of another lambda and they both use the same formal parameter X because
it was written by one of those programmers who calls everything X you know well when we do substitution in the
outer one we have to protect the uses of X and the inner one from being
substituted because we don't want to substitute for those until we actually call that inner lambda so a lot of the
complications in here have to do with that and the real scheme as you'll see doesn't do anything like that at all
so I want you to focus your attention mostly on eval and apply as you read this which you're gonna for the lab and
homework thank you
UC Berkeley