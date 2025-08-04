Transcript


wow where is everybody I guess they're all studying
for the midterm or else they tried studying for the midterm and gave up one or the other
um okay so we're having a midterm this evening 2050 vlsb be there b square
um and we're going to talk some more about logo um for two reasons one is
that you're doing a programming project implementing it um and the other is to
illustrate um some of the questions of programming language design so we're
going to say how come scheme is this way and logo is that way um
and most of the answers about those differences come down to the fact that
um scheme is a language for adults and logo is a language for kids um which is
partly saying scheme is a language for professionals like you guys and uh logo is a language for um
amateurs inors you know um so we'll see how that affects the different decisions
that were made although part sometimes there isn't a good reason it's just you know history
of what was going on at the time um
okay so I mentioned at the end of last time that in logo there are certain
procedures that return values and they're called operations the other procedures that don't return values you
call them for some action that they're doing like printing something or changing the value of something um and
they don't return a value so let me just run down their big points um scheme has
a single name space that is any symbol is only ever the name of one
thing um and that has to do with the fact that everything in scheme is first class so
anything including a procedure in particular could be the value of a variable um logo like earlier lisp
dialects um and also like common lisp by the way which is the sort of industrial
strength lisp that people use out in the real world when they use Lis at all today um has two name spaces uh one for
procedures and one for everything else um
so um why is that important well often like every day when we're
writing scheme code uh we want to have a formal parameter that's list or word or
sentence right and we don't we call it LST or seent or uh
WD um because in scheme if we called it list
or sentence or word that would um make the Constructor procedure for that data
type unusable inside the procedure that had that formal parameter in logo that's
not the case so I can have if you look down here jumping ahead a bit I can have
my pig latin procedure has a formal parameter word and it
also has is using the procedure word which is the Constructor for
words okay um so two name spaces one for procedures one for everything else
actually in logo and traditional logo anyway there's a third name space the
same symbol can also be the name of something called a property list
um which we aren't going to worry about here
um scheme is lexically scoped logo is dynamically scoped I'll talk more later
about the implications of those choices um scheme has first class procedures
logo doesn't so that's a huge difference right first class procedures is at the
heart of everything we've been doing all semester um but it turns out that if you
have a lexic I'm sorry have a dynamically scoped language then you can just quote an
expression and that expression is just as good as a procedure to compute that
expression what do I mean by that so let's think about Dynamic and lexical scope of it lexical scope means that
when you make a procedure with Lambda there are two parts to the procedure the
left bubble which has the information contained in the Lambda expression
itself namely the parameters and the body and then there's the right bubble
that says where was this procedure defined so that we know what environment
to extend um when we call this procedure right
that's lexical scope we talked about environment diagrams a lot I hope you know that you're going to need to know
tonight um in a dynamically scoped language when
you call a procedure you make a frame binding the formals to the actual argument values and then you extend the
current environment so there's no right bubble in a procedure well if there's no right
bubble then a procedure really boils down to just the text of the
procedure um so in scheme a Lambda the the procedure created by Lambda carries
with it values for certain variables right the variables that um are
inherited from Outer Scopes like if you have a let outside of Lambda um but none
of that is true in logo if we did have first class procedures if we had Lambda
the procedure that was created by the Lambda would just be the text of the procedure the way it was in the scheme
one interpreter scheme one wasn't dynamically scoped but it used the substitution model and so
um what was in the procedure was essentially a modified version of the text of the Lambda with substitution
having been done already before we even saw the Lambda
um and so we're going to see in a bit that in logo we can just use Expressions
the way we use First Class procedures in scheme so we can make higher order functions based on just
Expressions um and finally um as we saw last time
scheme you always put parentheses around every procedure call parentheses are
never optional they always mean something and what they usually mean is we're calling this procedure with those
arguments um and that means in particular that you can tell the difference between a procedure
name that we're calling and a procedure name that's providing the argument to
some other procedure like map and the way you can tell is if the name has a left parenthesis right in front of it
then it's being called and if not not um in logo we don't fully
parenthesize things and so in order to keep straight the difference between arguments and procedure calls uh we have
to know the arity which is the fancy term for how many arguments does this
take of every procedure so every procedure has a default aity
some procedures can have variable arity if you use parentheses around the calls
as in scheme okay so this is um in scheme
everything has very very simple uniform rules in logo there are a lot of
compromises and there are compromises because um of what people expect right
so people expect to be able to do infix arithmetic um people don't like lots of parentheses
if you can remember back a few months when you started this course and you saw a list code you said right all these
parentheses um so in logo we don't give people a chance to say that because they
don't see all those parentheses but instead the logo interpreter has to know the arity of every procedure okay so let
me show you a couple of simple examples um let's print um second of
um am I loving my um so how does second work well it
has a formal parameter so two is
like uh Define plus Lambda right so it says Crea a procedure
so 2 second the reason it's two is um um think about telling a human being how to
do something so you would say um to differentiate a
polinomial blah blah blah blah blah right um to get from here to soda Hall
go out the door turn right okay so that's the sense of two that we're using
I'm telling you how to do something so to Second and then comes formal parameters and they have colons in front
of them um and we'll talk about the in in a bit for right now it's just in the
title line here it's just a piece of syntax to remind you that this is a formal parameter and not the name of the
function um so to Second dots thing and oh yeah that's how we pronounce colon we
logo i' say dots um so you'll hear me say that a lot so this part you'll
recognize first of but first of dots thing in scheme it would be open pin first open pin but first thing close
print close print um but this means the same as that because logo interpreter
knows that first and but first each take one input and if you have just a symbol by
itself that means you're calling a procedure it's a procedure name and you're invoking it uh if you have a
colon in front of something it means uh we're looking for the value of a
variable what's new to you is this output um output is a
command everybody gets confused about this output is a command that you can
only use inside a procedure definition and it turns the procedure that it's in
to an operation so output itself is a command but second is an operation
because it says output in it an output takes one input one argument and it says
the procedure that I'm in should return this value okay so if I just said first of
but first of Dos thing it would be like saying first of but first of um
help I would get an error message you don't say what to do with well the same thing is true inside a procedure body if
you want your procedure to Output that you have to say so and one of the reasons for that is
instead of saying output here I could have said print in which case my procedure would
be a command it would print something and not return a value so my twice procedure
does that twice um
man prince it's input twice okay notice by the way that there
aren't any brackets around the printed value we'll talk about that in a
second okay so twice does not return a value I couldn't say print twice no air
man if I did that let's try
that I get the error twice didn't output to
print oops okay so I'm doing print that means whatever comes next should provide
the input to print what comes next is a procedure call so logo runs the procedure it prints no or Man twice and
then twice is supposed to Output a value that print can print but it
doesn't Okay so I get the message twice didn't output to print by the way um
remember the first time you saw a scheme error message and you could barely see what the actual error was because there
was this whole back Trace underneath it that didn't understand and was a little
intimidating and furthermore if you did see the error message it said something like Unbound variable and you had no
idea what Unbound meant um one of the things that distinguishes logo as a
language is that we put huge amounts of effort into the error
messages the error messages are supposed to be non-intimidating
um and in general we try to phrase things
so that it doesn't sound like you're a bad kid having done this so it doesn't say you gave a command where an
operation was needed it's it's twice his fault right twice was supposed to Output to print and it didn't um so we really
think about things like that in logo error messages um uh in fact
um I'll tell you a story Foo
I don't know how to Foo so two things about that message one
is I'd like you to notice this very subtle extra space in here that's supposed to be a reminder of
how to fix this problem by saying tofu do blah blah blah blah blah
right um secondly it's I don't know how right it's not not your fault I don't
know um although some people there's actually that's a little controversial people write academic papers about this
subject um some people worry about anthromorph azing
anthropomorph whatever the computer um so I you know gives kids the
expectation that the computer is smarter than it is so Some people prefer um you
didn't say how to Foo so that's a a question of a little bit of controversy
among kid computer language writers but the real story is
um the original version of logo had a different error message in this
situation and the message was Fu has no meaning
and this lasted until my friend Paul Goldenberg who was one of the early logo researchers and the world's best teacher
um and a great guy was working with um fifth graders I think or seventh
grader somewhere in that ranch um and one day this little girl came up to him
in tears because she had typed into logo
love and the computer said love has no meaning the next day there was this
error message okay um yeah I don't know how to love well
it's better than love has no meaning right and computers don't you know computers don't know how to love you
they know how to hate you that's a different story okay um moving on
oops ah I said oh whoops that's the
problem so here's um pigle so I say
print pigle quote logo
logo quot sche te skay all that um how
does it work well
if vowel P first word if the first letter of word is a
vowel and then there's these square brackets inside the square brackets it
says output word dots word quote ay so here word is the Constructor
procedure with two inputs the first input is our uh our actual argument
whatever corresponds to the formal parameter name word and then quoted ay so notice that
you do the quoting with a the double quote character the one that you used to think of as quote before you came here
um but there's only one of it it's doesn't come in pairs um so it acts like
the scheme single quote uh but use the double quote character for quoting
um but the interesting part is these square brackets square brackets in logo
mean the same as quote parenthesis in scheme namely I'm both delimiting and
quoting a list you can have brackets inside brackets and those are just like
parentheses in scheme but the outermost one implies a quotation
mark if you don't want to if you don't want to quote something then you don't need any delimiter at all you just do it
right so I guess I should write this on the
board about a dozen special forms in
scheme there's only one special form
in logo and that's two for defining
procedures everything else is an ordinary procedure that evaluates its
arguments now you will remember back in week one of the course you proved that
if had to be a special form right that doesn't seem to be true
in logo why not well because quoting
the thing that you want to do is good enough if we get around to saying evalve
this expression which is essentially what if does um it will inherit the argument of the
caller of if right so if could be a userdefined procedure in fact in a bit
I'll show you how to write if without having any conditionals in the language
at all it's very cute but we're not ready for that yet um so this is what I
mean by saying that an expression in logo uh
is like having a procedure in scheme so if we wanted to do this the equivalent
to this in scheme we would write an if that said if parenthesis vowel P first
of word close parenthesis um open pen Lambda left pen right pen output blah
blah blah blah blah right we would have to make a procedure to be the second input to if um if in
logo takes two inputs by the way uh thing to test what to do if it's true if
you want the three input kind like the scheme one that's called if else one word if else test what to do if it's
true what to do if it's false okay um
so another thing to note about this is if we do evaluate this output
expression output ends the procedure so this line after that doesn't have to be
part of an else Clause because the the then Clause here um ends the procedures
and as you execute an output the procedure is done um if that's not the case if first
word is a consonant then we say output recursive call to piggle word but first
of dots word first of dots word which is the same way we did it in scheme
okay um here's vowel P letter uh output member P um dots letter quote a
IOU let's say see if something is a vow by the way what is this member P vowel P about uh P stands for predicate
um there have been huge huge screaming arguments among logo designers about how
to represent predicates um there are basically three contenders one is question mark As in
scheme one is VP as in the most traditional logos and the most traditional lisps lisp always originally
used P um which has survived in the language of hackers um if you're hungry
and you want somebody to come eat with you you go up to them and say food pee and they know what you mean even if they
program in a list that has question marks um so P for predicate or question
mark for question or uh the third Contender with some British versions of
logo used Q um and the if Q is a kind of
compromised candidate because one of the problems with question mark as you may have observed if you want to say a
scheme program to someone um there's a procedure called
list that's the Constructor for lists and there's another procedure called list which is the predicate for is this
thing a list and it's so you end up saying list question mark you know uh list p is a lot
easier um but Q is pronounceable so you can say
list Q uh but it's an uncommon letter you're not likely to have a name that
ends in Q by accident um so that's the advantage of Q it's actually not a bad choice but
nobody uses it outside of Britain
um I was always um a p fan mainly
because of this list problem um but also I claim every
procedure that returns a value is answering a question so when you say plus 23 in
scheme or some 23 in logo you're asking a question what's the sum of two and three how much is 2 plus three question
mark right in English you'd have a question mark for that the same as you do for predicates which are yes or no
questions um so I think that to uh make the idea of predicate
um ex have mean the same thing as the idea of question is confusing and that's
why I like P it's more specialized um people who don't like P point out that
um there are primitive logo procedures whose name end in p that aren't
predicates like stop is one um and so people who would question mark fans
would make fun of us P fans by talking about the Primitive Stope um um there a
mispronunciation of stop um so in the design
of um Apple logo uh in which I participated in about
a trillion design meetings at which there was H scam arguments about this I ended up winning we used
P the argument that convinced people in the end was one that I made as a joke I
said anyway look the scheme prompt is a question mark So if you say you know
word p word I'm sorry if you say word question mark it looks as if you're
delimiting something like you know the upside down question mark in Spanish at the beginning you know and they said oh
yeah huh oops oh well um
hey yeah um and so that's how I won the argument
okay uh let's move along here um so yeah uh essentially no special
forms except for two in particular if isn't a special form and so almost all the time you see square brackets
here that by the way was also controversial in the original original
lisp if was a special form and the notation was if test then
what to do if it's true and then you could say else if you wanted to and have another thing just like you know all
those other programming languages um and I hated special forms so I made them do
it this way and the problem with doing it this way is people always ask how
come this is in square brackets but this isn't in square
brackets and because you understand about evaluation right and that we want
if to evaluate this other thing only under certain conditions and all of that
um you know why there are brackets on the second one but not the first one but it's a little hard to explain that to a
kid and so that was another thing we would argue about um it's also hard to
explain a million special case rules to a kid so there are advantages to uniformity also um okay uh oops
so here's just the standard um but first your way down a sentence
kind of recursion I say um print Pig
Latin
um another girl
not a great example oh well um all right
print there lots of
consonants that's better um so how does this work it has a
base case if the sentence is empty output the empty sentence otherwise output
fput that's cons it stands for first putut so put this at the beginning of
that um there's also in logo lput which you would have liked when
you're trying to reverse a list the first time um so
fput call piggle on the first word of the sentence and call Pig Latin on the
butt first of the sentence so it's just like cons um
I could have said here of course instead of fput sentence and it would have done the
same thing right it would have had the same result and that's what I would do if I were writing this for a kid but
here I'm writing it to teach you about fput okay
um factorial 10 and factorial
six whatever okay so that's the same factorial program you know and love
except that it's using infix arithmetic here um infix arithmetic has a problem
about figuring out precedence so you have to think carefully about for
example why doesn't this take the factorial of N and subtract one from
it or n times the factorial of N and subtract one from it and the answer is
that infix operators have higher precedence than prefix
operators sometimes that's what you want and sometimes it isn't but then you can change it with parentheses but it's the
problem with infix is that you have to think about order of
operations um
oops oh word
uh there hello hello hello hello hello hello hello hello hello
hello um so this doesn't actually work by constructing this long word um it
works by calling type um type is like display type is to scheme
display as print is to scheme print namely it prints the stuff and
doesn't start a new line um and then here after we've done
that numb times we print the empty sentence and that gets us onto the next
line okay um oh and here's uh at Old stopy if
number is equal to zero then stop and then we don't do all the rest of this
stuff okay
um I could instead have said if number greater than zero left bracket and then
all the rest of this thing right bracket that would work that would have worked too but this is more traditional logo
style that if base case is reached stop otherwise do these things uh and finally
a recursive call this is of course a tail call um and uh the Berkeley logo
interpreter does recognize tail calls and do tail call elimination um although it's a real pain in the butt um because
of the difference between commands and operations that confuses things a lot in The
Interpreter um
ah okay
check this out oh the Third Kind of print is show
show is just like print except if the thing you're printing as a list it puts square brackets around it um the reason
print doesn't is that the main use of lists in logo is for sentences for like
English sentences you're writing a program that carries on a conversation with the user you don't want to see
brackets around everything the computer says you want it to look like you know having a conversation so when you do
want the brackets because you're really trying to delimit something or emphasize that it's a list you can use show so I'm
going to say show
map function
over list of numbers
okay so this dollar sign time dollar sign that's the square function this is not the way you would
do it in scheme in scheme you would say Lambda of X time XX so this is kind of an automatic
formal parameter and the reason for that um is
so remember those pedian stages that Alan Kay talked about the the doing stage and the sort of visual stage and
then the symbolic stage U so visual stage kids which means up through age
12ish um can't do Algebra um you can tell them about
variables and they'll sort of get it um but if you say you know x + 4 =
7 young kids will have trouble knowing what you're asking them whereas if you
say Box + 4 = 7 then every third grader can do
this um because it's it's a visual language if you have a box like this
it's clear that something goes in the box right whereas with X that's not obvious so visual dominant kids need a
visual cue about the variableness of something
um so because of that U this is my invention what you're looking at right
now actually it's one of the things I'm proud of about logo um I wanted to have
box in the language but un unfortunately box is not an asky character so the
character I picked is question mark so if you see oh you're a kid and you see
something that says question mark times question
mark okay I figure that's about as close as I can get in asky text
to something that's going to make it visually obvious that you're supposed to put something in here so we're asking
the question what times what right okay
um so that's where this notation comes from but the cool part is how we can
write this program and the fact that it relies on Dynamic
scope so um let me move up um
there okay um the reason I'm using dollar sign here rather than question mark is that um uh the apply function is
actually primitive in Berkeley logo so question mark is kind of Taken um and I wanted to show you how it's
implementable so map function over a list if the list is empty output the empty list just like scheme
output con
call the function with first of dots list as its
argument so that's what's going to be the first element of the result and the
thing we're consing that on to is map the function over the butt first the list
okay so that's map everybody understand that if if you if call works the way it should then map will work the way it
should right um now in scheme I could have just
said fun of first of list but fun isn't exactly a procedure
we don't have first class procedures so I have to invent this thing call which is a little bit like apply except that
there's instead of a list of arguments we just give it the argument the real one that is built into logo actually is
very much like apply it would it does take a list of arguments but I wanted to make it simple in this example that I'm
showing you so to call function argument value um if function is a word never
mind that function isn't a word uh it was that list question mark times
question it was dollar sign times dollar sign so I say output run. Fun Run is a
logo primitive it's eval um now why doesn't it take an
environment because it evales in the current environment okay implicitly it has the
current environment as the evaluation one so how can we evaluate dollar sign times dollar sign well because I wrote a
procedure dollar sign what does dollar sign do it outputs dots ARG
value is there a local is there a global variable dosar value no if I say
print that's AR value has no
value means Unbound um is ARG value local to the
dollar sign procedure no is this dollar sign procedure defined
inside of something lexically inside that has a ARG value no but there is ARG
value in the current environment because the current environment of dollar sign
extends the environment from the call to call okay because that's Dynamic scope
so this dollar sign procedure can refer to an argument to call so call and
dollar sign work together to provide this sort of boxlike um capability for indicating argument
slots without explicit use of a formal parameter um and I think that's the
kid-friendly way to do it those of you took 6 S10 uh will recall um seeing um
blocks with empty input slots used as inputs to higher RoR functions it's the
same idea um except in BYOB it really does
look like a box it's just like that um but you know logo were limited to text
okay um huh I'm actually more or less on schedule for a change see what haven't I
done here um nothing at the end okay great
so you guys are so lucky because you're getting this course from
me uh everybody else every other computer science person on Earth will
tell you Dynamic scope is just a mistake lexical scope is the right
thing and the reason they all say that is that they're
envisioning uh industrial computer programming right we have a lot of people working on a computer program and
it has to work every time it's got to be bug free and it has to be fast because
it's going to be used over and over and over again right uh in education
um the program isn't going to be used over and over and over again as soon as it works you go on to the next exercise
right um it doesn't matter that much if it's it's fast as long as it's not excruciatingly slow um and so the values
are different and so if you're writing a language for kids I claim you want it
dynamically scoped parenthesis BYOB isn't it's lexically scoped um and later on people who are BYOB fans we can talk
about why that is but I don't want to confuse things right now um small talk is dynamically scoped Alan
K's language for kids okay Lex scope is good because as
you know if you have lexical scope and you also have Lambda then you get free object-oriented
programming right because you you can have local state variables by putting a Lambda inside a let right or in other
words a Lambda inside a Lambda basically um and lexical scope plus Lambda gives
you that now most lexically scoped languages don't have Lambda although that's starting to
change it I think for people my age this is really very amusing it's one of those
amusing things um 50 years ago 60 years ago when lisp was invented everybody
immediately started making fun of it 50 years later everybody's still making fun
of lisp but now their favorite language also has Lambda right so it's like we're
losing the the Battle of what the language should be called but we're
winning the Battle of how it should work anyway um so lexical scope allows local
state variables Dynamic scope allows first class
Expressions okay so the example I just showed you with map
um depends on Dynamic scope because it means that an
expression is as good as a procedure would be given Dynamic scope
whereas in scheme uh you know quote times XX is a very different thing from
Lambda of X X XX but in logo they're not so different okay lexical scope prevents
name capture bugs what does that mean um suppose I say
um kind of a silly example uh
Define no not scheme logo
make quote Pi make is a combination of Define and setb it just set the variable
to this value if it didn't exist make a global one it's not a special form so I
have to quote the variable name
3.141592654 okay now I say um to
to Pumpkin
dop um [Music] print I don't know
area five two area dos
radius output abbreviation for output put um dots Pi time dots radius time dots
radius n okay so now if I say print um area
five uh that's 25 time Pi basically 25 *
3 would be 75 it's a little more than that okay now if I say um
wait now if I say pumpkin
four uh the area of a circle of radius five has become
100 right not out here print uh area five
this still works but um
because pumpkin happens to have pi as a formal
parameter this procedure area which thinks it's using the global variable Pi
is actually using this local Pi that's called name capture pumpkin is capturing
the name Pi that area expected to mean something else okay so that's a source of bugs in
dynamically scoped languages and it's true it is although sometimes it's a behavior that you want remember the time
that the legislature of wherever that was almost uh did declare pi equal to 4 you
know that story some idiot State Legislature Lor
um decided that arithmetic was too complicated with pi having this screwy value um and it would be so much easier
to do engineering computations if Pi were four so he introduced the build declaring pi to be four and luckily some
staus from the University of whatever state it was happened to be visiting uh
the legislature that day about a completely different issue um and you know hit the roof and didn't let them
pass the law um anyway so name capture bugs on the other hand it lets you have
what's what I'm calling semiglobal variables what I mean by that is um
I'm a kid I want to draw a picture and the picture has a house and you know a door and a window
and whatever and there's a path leading up to the house and there's a nice fractal tree next to the driveway and
there's a car on the street and all that stuff okay and now I'd like to be able
to do this in different sizes so um
I'm going to have a procedure um to
picture dots size and then it's going to say
House Road tree
car end okay typical kid
procedure in house I'm going to use I'm going to say two
house and then I can say you know forward do size
Etc move that many steps if I wanted to do this in scheme all of these
procedures would have to take size as an argument right um in logo I don't have
to do that that's what I mean by a semiglobal variable and it's just sometimes very convenient uh and kids
you know understand it perfectly well finally um H good thing it's finally
because we have one minute left um a lexically scoped language makes for
faster compiled code because the compiler
knows which variable which binding is meant by any
variable name reference without running the program because the variable name refers
to a variable of this procedure if there is one like that otherwise the enclosing
procedure in the definition otherwise the enclosing procedure of that out to the front so the compiled program
doesn't have any variable names in it at all it says something like look at the
third slot in the fourth frame back from this one and that's just a few machine
instructions to point to jump around to there um a dynamically scoped language uh the
same variable reference can mean two different variables as we saw about this variable reference depending on the
context in which the procedure is called so you have to look up the names at runtime and that slows things down on
the other hand if something goes wrong and your program has an error and I
don't have time to actually show you this but um you can have the program
stop at the point point of the error give you a logo prompt but in the
environment where the error happened and because of dynamic scope
you can see the variables of the procedure where the error was found the
variables of the procedure that called it the variables of the procedure that called that because the actual mistake
in your program I'm sure you've had this happen the bug in your program might be in a different procedure from the one
that actually had some primitive blow up right maybe your procedure a called
procedure B with an invalid value and B called C and C called some primitive that blew up right so in order to find
the bug you have to look at the variables of procedure a and with Dynamic scope you can it's just there
lexically scoped languages have to give you this complicated uh interactive
development environment thing where you use mechanisms outside of the language
to look around uh the environment okay see you Friday I'll see you tonight
sorry then Friday
UC Berkeley