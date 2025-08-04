Transcript


okay so these last few weeks we've been talking about representation of data
structures and we're still on the topic of representing data and the particular
problem that we're looking at today is data types different kinds of data and
the interaction between data types and the operations that we want to perform on them and there are three big ideas
for the week they are type tagging data directed programming and message passing
so to start with the first problem we're going to solve is this one at the
beginning of this chapter you saw an abstract data type for rational numbers
that was a pair with the numerator in the car and the denominator in the cutter and you also saw an abstract data
type for complex numbers that had the real part in the car and the imaginary
part in the coder of the pair and that all works great if you're only dealing
with rational numbers or you're only dealing with complex numbers but let's say you want to write a program that
works for any old numbers and you come upon a pair whose car is 3 and as cooter
is 4 what is it well you don't know so
the solution to that is type tagging and it's going to seem like a ridiculously
trivial idea to spend time on until we start talking about a little more the
idea is this we represent 3/4 as a pair whose car is the word rational and his
cutter is what it used to be and we
represent the number of 3 plus 4i as
this structure okay so these things
rational and complex or type tags and we have an abstraction for tag data that
you can see up in the top half of the screen so the constructor for tag data
is the attach tag otherwise known as cons and the tight tag is the car and
the contents is the cutter okay as I
said a pretty trivial idea but there are
some more things to say about it that might make it more interesting the first thing to say is that inside a scheme
interpreter it has to do something very like this for its data types
because as you're going to learn in detail in 61c and as they told you
probably starting in third grade inside the computer there's nothing but ones and zeros and you take a pattern of ones
and zeroes and you give it a meaning by some convention so the same pattern of
ones and zeros can be an instruction to the computer like move this from here to
there or it can be an integer and there's slightly different
representations for signed and unsigned integers and why is that because in a
computer word which is 32 bits 32 of those ones and zeroes mostly although
you're starting to see 64 bit ones let's talk about 32 bits because the numbers are easier to grasp
you can represent about 4 billion values so your choice for integers is whether
you want to represent 0 to 4 billion roughly or whether you want to represent
negative 2 billion to positive 2 billion roughly so by getting negative numbers
you lose to the half of the magnitude so there are these two different formats and then there's a
third format for representing numbers that aren't integers that have a fractional part called floating-point
which is extraordinarily complicated in its details and you'll learn a little bit about that in 61 C also so since all
of those things are just patterns of ones and zeroes and since every possible pattern is meaningful as an integer and
pretty much every possible pattern is meaningful as a machine instruction or
as a floating-point number scheme can't tell just by looking at that pattern
which thing it's trying to represent oh and another thing it can be is a pointer
so a pointer is something that says we're in the computer's memory something
is so a pair for example is made up of two pointers so that's yet another data type that the same patterns with ones
and zeros can represent so what scheme does is something very much like this
where it attaches a type tag to every
value and typically not in an interpreter the type tag is not a word
like rational or complex a text word it's a pattern of just a few bits
because they're only you know half a dozen or so types that you need to
represent so they take three or four bits carved out of some place and use that as the type tag for each value so
every interpreter for a list like
language including scheme does type
tagging of the data this way that we're talking about internally some other
languages don't do that and this is why it's worth talking about and not a trivial idea because there are
implications either way so
in that language you learned in high school you say things like integer I
comma J and maybe you say float or
something X comma Y right and you will
have noticed this semester that there isn't anything like that in scheme you don't have to say when you create a
variable I define or let or whatever what kind of value goes in it
okay words you do in these other languages typically languages that are
mostly compiled rather than interpreted make choices like this meaning that you
write your program and you run it through a compiler and out comes a machine language program which you then
run as opposed to something like scheme when you type in an expression and out
comes the value and you type in another expression and you can interact with it so why do they do this in these
languages what it buys them is this computers have these different
representations the conventions about how to interpret the bits built into
their hardware so in whatever computer you're using is going to be an
instruction typically with the name like add and another instruction with a name
something like floating add ok and
because of these declarations if you say I plus J the compiler for Java or C++ or
whatever it is you learned knows that it should do integer ad whereas if you say
X plus y the compiler knows that it should do floating out right and
therefore at compile-time we already know what kind of arithmetic to do and we can
compile this into exactly the right machine instruction scheme doesn't know that when you say something like I plus
J in a scheme program we don't know until the program is running what kind
of thing the value of those variables is going to be right because in scheme you
can make a list of numbers and some of them are integers and some of them aren't and it all just works okay so the
disadvantage that we get from using type tagging from in other words from
associating types with values rather than associating types with variable
names the disadvantage is that our programs run a little slower because the
scheme interpreter sees well doesn't see I plus J it sees plus IJ and it has to
say well let me look at AI and see what its type tag is I'm going to look at Ju see what it's type tag is and then do
whichever of these is right by the way what if you say I plus X what happens
well something more complicated because you can't the machine doesn't know how
to add an integer to a float so what happens is you call us a procedure it says convert typically convert the
integer to a float and now I have float plus float and then I can do the computation and a compiler has to think
about that case also as does the interpreter right but the compiler does
it before you're even running the program so if you're in a situation in
which you're going to write a program and once it's written it's going to be used every day until forever by some
company then it's a good idea to put as much of the work as possible on the
shoulders of the compiler because when the program is running every day it then
doesn't have to do this kind of analysis it's just ready to roll on the other
hand but kind of the other extreme if you're let's say a Steven in a computer science class basically
your programs never go into production you're only interested in a program as
long as it's not working right and once you get a debug to go onto the next exercise
so for you what's important is not the running speed of your program so much as
the running speed of the whole process of reading what you type and figuring out what it means and doing it so we
don't really suffer from this time efficiency problem of using type data
instead of typed variables and we get an advantage the advantage we get is this
it's really easy to do heterogeneous data okay so I can come over here and I
can make a list that contains an integer and
a non-integer not going to remember all those digits public and a word and a
list
and that just all works okay if this were a list of numbers I can write a
little program to add them all up and my program wouldn't have to worry about is
this thing an integer is it not an integer all right so what you have to do
in this kind of language is stuff like
okay since variables have to have their types set ahead of time if I want to
write a procedure to square a number after i1 for integer is and a different one for floats and I have to call the
right one for whatever kind of number I'm actually looking at right now and it's a big pain in the neck okay if you
know that in this program you're only dealing with integers then it's okay we're only dealing with floats but if you're going to try to mix types you end
up doing stuff like this some of those languages because they're designers
aren't idiots and they know that nobody wants to do this invent sort of mechanisms on top of mechanisms to let
you type both of these at once by having essentially a variable for the type that
you then give you know first you say do this for integers and then you say do it
for floats but that's the sort of thing that we get for having types attached to
data is that we can have heterogeneous data we can mix things up and it doesn't
matter okay so that's a little piece of sort of programming language design
questions because one of the things I'd like you to get out of this course is to
be able to answer the question when when you're you know sophomore is the next
year's freshman come along and somebody asks you why isn't there just one best programming language okay this is part
of the answer right the best programming language for writing a program once and
then running it a million times might not be the best programming language for
the process of development and in fact there are companies out there in the
world where they'll use something like Lisp in the early stages of developing a
product because they can come up with new versions and new versions and tweak up these or interface and so on and get
it just right and then finally when everything is just the way it's supposed to be they'll reimplemented and
something like C or C++ or Java so that it runs fast
not so much Java tests that the other ones run pretty fast okay
so that's the story on type tags let me stop and see if your questions a single
question okay who's with me okay good
all right so now we know how to deal with data types and now the question
that comes up is there are certain operations that we want to perform on our data and sometimes it's the same
operation for different types like the example of I plus J versus X plus y there it's a somehow or other we have to
have different versions of plus and know which one to use and that's the problem
we're going to be addressing for the rest of the week but operators that have
two operands like plus are fairly complicated and I like to make things
simple so I'm going to start with a different example of data types and operations and I'm going to make a
little chart to show you what we're doing my types are geometric shapes so I
have think of it this way
square in circle whoops and the
operations I'm going to do our perimeter
and area okay now what goes in the boxes
a formula right for how to do that so
for a square which side s what's the perimeter where else what's the area
that's squared okay for circle of radius R what's the perimeter two PI R and
what's the area PI R squared great
except I hope that you understand by now
that I'm not really going to do it quite like this I'm not going to put formulas
as pieces of text what I want to think about is functions so I'm going to think
s maps to for s s map to s squared R
maps to two PI R and R maps to PI R squared ok so that's what's in my head
so for this simple example of two data types and two operations I have four
procedures okay now think about integer
rational real complex plus minus times
divide integer rational real complex so
there's two data types involved the you know left operand and right operand and
four possibilities for each of those and for operations for a total of 4 times 4
times 4 is 64 functions we have to keep track of ok
so that's already a pain in the neck and that's you know there are more types and more operations than that so that's why
I'm starting with a simple case but I want you to understand that the subtle
mechanisms were going to invent for dealing with this problem are worth
inventing because real problems are more complicated than the one I'm showing you today okay so the first thing is let's
make some data which peptides attached so I have procedures make square what's
that what I want to do is define s for
to be make square for and the value of
that just to be clear is a pair whose car is the tie tag and it could it is
the value I'm going to say mate I'm going to define c4 to be make circle for
and define s5 to be mate square five and
define c5 to be make circle five just to
have a little data ran to play with and now we're going to look at how to
organize all this information about the the methods for doing some operation on
some data type okay and there are three ways we're going to look at doing it and
the first one the book called conventional style it's called that because it's kind of the obvious way to
do it that's what people did for a long time before computer scientists came
around to you know try to improve things namely it goes back to that thing I keep
talking about about nouns versus and when you're thinking about how to do
an action the most obvious thing for people is to organize their thinking
around the verb right so here's how to build a house and within that there's
how to build a house with a wood frame and how to build a house or masonry and how to build a house out of plastic
prefab panels and so on and it's all under the heading of how to build a house okay so up here we have a
procedure area it takes one of these shapes as its argument and it says okay
what kind of thing am I looking at am I looking at a square so that's this
question right here so is the type tag
of the thing I'm looking at the word square if so I'll just return contents
of shape times contents of shape contents is the the number that
represents in this case the side of the square so if I say down here area of s 4
I get 16 their lips area s 5 I get 25
right the side of the square the square of the side of the figure okay if not
then is this a circle if so the area is
PI R squared so if I ask for area of C 4
I get pi times 16 which is about 3 times 16 it just would be 48 this is 50 close
enough Area C 5 I should get something around 75 or 80 yep there we go
okay any questions about how this works
great this is easy one so um on my
picture this is conventional style where
we group things basically in by the columns so everything having to do with
a particular verb find the area all the different ways of doing it for the
different data types are grouped together okay well that's not so bad is
it it's straightforward to write it does do the job of sort of grouping the ways
of doing something together so you can find them you don't have to dig through 64 different little procedures so that's
all fine the only problem with this is what's if I decide later on that I'd
also like to be able to deal with regular hexagons or skiers or triangles or something I'm going to have to go
into code I've already written and edit it I'm going to have to edit my area
procedure and there's the similar perimeter procedure here that has the
same structure and I'm going to have to find all of those things and put in an
extra cond clause for whatever shape I want to add now the trouble about going
back and editing procedures you've already written is that you introduce bugs and you know anytime you write code
you might introduce a bug in your new code but here you run the risk of
introducing bugs into code that used to work for example by getting the parentheses wrong
okay by putting your new claws in the wrong place
like inside one of the existing closers or something like that would break code that used to work so whenever possible
our goal is not to ever have to go back and change working code in order to add
new features that's something to remember about designing a program so
how are we going to do that the first
way we're going to look at is data directed programming so that chart I have over on the chalkboard it's so far
it's just something in my head okay that here's how I'm mentally organizing the
problem I'm trying to solve about different shapes and different operations on the shapes but we can also
say let's take this thing this whole
thing and find a way to encode this
chart as data in the computer and this is called data directed programming data
directed programming means that we're going to write one generic operation
that does everything and the way it knows what to do in particular is by looking things up in an actual two
dimensional table like this now how do we build such a table well we don't do
that for another week 2 weeks 2 week 3
weeks we're going to build tables for now we just give you one way it works is this
can say get know it's good to this dress
it says false meaning I don't have that in my table now I can say put try on a
dress 7e one soda now if I say get Brian a
dress it will tell me whatever I put in the table okay so that's getting put it's a
two-dimensional table that is to say the get operation takes two keys for a row
and a column the put operation takes two keys and a value to put in that place
because that's what we happen to need for this problem that we're solving but
we'll see later on when we talk about tables how to implement them that you can make one dimensional tables or
three-dimensional tables or multi-dimensional tables but this one happens to be a two-dimensional table
and there's only one table right now later on we'll learn how to make lots of
tables but for now there's only one of them and it's just there to begin with
is this functional programming
original programming yes functional programming no I'm not sure come on wake
up you can say I'm not sure okay um I'm
seeing a lot of I'm not sure I'm seeing more nose than yeses which is good it's not functional programming because look
at the tube gets I called the same procedure with the same arguments and I
got different answers okay so the procedure get has a behavior that
depends on what else has happened mainly it depends on the fact that I did this
put if I did it put again with a different value in there then another
get would get yet a third result is that a hand up yeah ah there's a good
question is put functional because it returns okay every time you call it so
it's sort of the constant function of its arguments no because even though its
value is predictable just from the arguments it changes the world in some
way so anything that changes the world like print for example is considered
non-functional as well as things that depend on the changes in the world like
read okay so this is not functional programming however we're going to make
an agreement here in this room that the way we're going to use this table is
right at the beginning of our program we're going to have a bunch of puts and then we're never going to do any puts
anymore okay so we're going to set up this set of how to do what and once it's
set up we're going to leave it alone for this running of the program and later on we might come in and invent another data
type or something but for any particular time for the per we're only going to do puts right at the
beginning and then we're never going to change anything in this table and once we make that agreement we can think of
the gets as being functional okay because we know that it really did
depend on us having done those puts but once we've done them we're always going to get the same answer for the same keys
the same two arguments alright so um here's how this works actually let me
start whoops it's not what was supposed to happen you start by actually loading this stuff
all in
okay so the table mechanism they put and get
doesn't care what values you put in the table like I put in a sentence that was
my address before but for our purposes in solving the problem of generic
operations what we're going to put in the cells is functions right like s maps
to 4f and the Waynes scheme we say s maps to 4s is this right if they lambda
s x 4s okay questions about that somebody's hand was up before okay good
so I have two data types and two operations and that's four different
ways of doing things and here they all are and you should look at the four puts and
look at the thing on the chalkboard and convince yourself that one is a
representation of the other okay so this
should be your first glimmer of what I mean when I talk about data directed programming because this table is data
all right this is a data structure in our computer program and in that data
there's instructions for how to do things so now I can write what you see
underneath the foots on the screen right here which is a general procedure for
doing any operation on any data type here's how it works
starts by saying let's look up in the
table the type tag of my operand and the
name of my operator okay so I have type tag will be square and op will be
perimeter right so we look that up and we get
square perimeter and what we find is lambda s times floor s so now there's
this if what is if proc mean what am i
testing here yeah is there a table entry
or not because remember that get if there isn't the table entry returns
false this by the way speaking of programming language design this is a
little different from the way most things work mostly if he asked for something that's not set up that you
can't do you don't get back false you get an error message your program stops
dead in the water right this table was
designed so that no matter what keys you give it it never gives you an error
instead if if there is no such cell on the table it just gives you false and
you can then test for that and in this case what we do if we get false is we
give an error message but you'll see later on that in some more complicated versions of this if what we get back is
false we try again with different keys
okay so that's why it's useful to have the table return false rather than an
error message but let's say it doesn't return false then what it returns as a procedure and we can call that procedure
on contents of odd not just on odds because objects pair like square dot for
we can't take square dot 4 and multiply that by 4 we have to take the 4 and
multiply it by 4 so contents of odd is the actual number without the type tag
and that's the thing that we're going to use is the argument to proc questions
about that
okay so you see that this operate procedure doesn't know anything about
squares or circles or areas or perimeters we could load up the table with a completely different kind of
problem we could put in arithmetic operators we could put in stuff like magnitude or square root or something
and the operands could be integer rational real complex or whatever and
[Music] operate would work just fine all right
so operator is a truly generic function for doing any operation on any data type
as long as we've set it up in the table so we say something like operate and the
operation I want to do is let say area on C for or operate quote area s for and
the right thing happens okay
um so we got here by doing a lot of stupid detail work about foot foot foot
foot but I'd like you to see that we're in a truly beautiful place that we've
separated out the issue of finding the
particular way to do this function of this operand from the general question
of I want to do an operation on an operand you know please do it for me so
you can build a programming language that reads in a verb and a noun like
some of the earliest role-playing games before they had you know graphical
interfaces with my some things you would type in something like go write or take
or attack troll right and those things
were verb noun and those games were written exactly like this there would be
a general procedure that just says read the verb read the noun and then look up
in a table how to do this kind of thing on that kind of data okay so it's a
complete different universe from what we've been talking about and this idea still works okay we're going to see in a
bit later on probably Friday that we can expand this idea to deal with operators
with two operands like the arithmetic one now we haven't done that yet but it is doable so that's one thing we're
going to do let's see when Tommy gets back oh yeah we're not going to do it
yet um oh yeah
the book by the way this procedure that I've called operate there's one in the book called apply generic which is the
same idea there's is written for two operand operators so it's a little more
complicated but it's so this operate means the same thing as applied generic I'm not quite done here because this
notation that we're using to ask for the
area of the square is a little ugly right it was better when I could say
area s4 and get an answer so we're going to fix that like this
by defining procedures area and perimeter so I can say area s4 I got the
right answer g5 okay but all those
procedures do is call operate so this is what people call syntactic sugar meaning
the real work is done by operate but to make users happy we wrap the call to
operate in a procedure that is nicer for human beings to use okay but the essence
of the job was writing operate this other stuff is just frills on top of that okay now really important don't
please get the idea that the name data directed programming means you have a
two-dimensional table that's used for keeping track of operators and operands
we are using data directed programming for that purpose now you know the
today's class but data directed programming is a much more general idea so back in the old days it used to be
that every company that we're talking about the days when computers were you
know half the size of this auditorium and cost a million dollars so every company that wanted to use a computer
would not only get a computer they would hire a bunch of computer programmers because you couldn't just go to CompUSA
or Best Buy and pick up you know TurboTax or whatever that whole software
selling mechanism didn't exist and instead everybody wrote their own software so for instance computers are
mostly used for boring things like payroll printing out the checks for the employees every month every week or
whatever and each company had their own payroll program okay today that seems
really stupid today you would expect to and pick up something called payroll
software and stick it in your computer and it would just work okay why did company have a separate one well
company a has seven digit employee IDs
Company B has four digits plus a letter employee IDs Company A pays every month
Company B pays every two weeks things like that
little things like that meant that each company wrote their own customized to
their situation payroll software okay what changed that it's still true that
company a has seven digit employee IDs and Company B as four digits plus a
letter it's still true that this one pays monthly in this one pays bi-weekly what's different we use software how do
you deal with stuff like that would you
say it sorry templates sort of yeah templates is a
specific case about editing and stuff work oh I see you mean like Java templates
yeah no I'm talking about the guy in payroll who wouldn't know a Java program
if it bit him but he can still set up his payroll program why give you a hint
preferences yeah so what's preferences
well it's a data file that tells the one generic payroll program how to deal with
the particular needs of this particular company right that's data directed
programming and it was the reason for
the first big dip in the hiring of programmers right used to be every
company with a computer had a programmer or two or three and then it got to where you could be a company and use computers
and not have any programmers on staff because you could use generic software courtesy of data directed programming
okay so it's a big important idea in the world you'll see initialization file who
runs Windows now blue on your computer
there are a bunch of files with names like such-and-such dot ini stands for
initialization those are data directed programming files ok he runs Linux or
Mac OS or any UNIX thing ok in your computer there are a bunch of files
called such-and-such dot RC those are data
directed programming structures the TEL programs how you want them configured so
this this is used by pretty much every program in the world
ok there's an initialization file which you can customize things so the very very very important idea I am now going
to show you the most interesting use of that idea
okay so this is an excerpt from something in the scheme reference
document that's in volume 2 of your course reader this isn't the whole thing it's just a little piece of it and this
is the formal syntax of scheme as this is a description of what a scheme
program looks like and it says what does
an expression look like well it turns out that formally there are exactly
seven kinds of expressions so when we look at the little scheme interpreter
and I said there were four kinds of expressions this is the same idea so the
first one is a variable which we looked at as an expression type literal means
self evaluating procedure call is a procedure call and the other four are
special forms and it turns out according to this scheme standard there are three
sort of primitive special forms lambda and cond and one we haven't seen yet for
assignment and everything else all the other special forms are defined in terms
of those okay so what I want to look at right now is what does a lambda
expression look like it looks like an open parenthesis followed by the word
lambda followed by formals whatever that means followed by body wherever that
means followed by a closed parenthesis so the thing in broke its angle brackets
less than greater than those are sort of meta variables they're not scheme variables they're formal syntax
variables about scheme so we have to know what formalism body means for most
of the formal parameters of the procedure and it consists of open
parenthesis followed by zero or more variables and the zero or more is what
this asterisk means followed by a close paranthesis so that's the syntax for a fixed number of
arguments or a single variable not in parentheses which means the variable
number of arguments notation with no fixed arguments or this hybrid thing we
have open parenthesis followed by one or
more variables which is what this plus sign means followed by a dot followed by
a variable that the rest argument followed by a closed parenthesis and so on okay I'm not going to go through the
rest of it but this is the formal syntax of scheme and back when this formal
notation which is called BNF for backus-naur form when it was first invented it was just for telling people
what the syntax of a programming language was but today you can get a
program that you're not allowed to call a compiler compiler even though that's
what everybody calls it because professor hill finger will get upset so for him you have to call it a parser
generator it takes something like this as input and turns out a compiler for
your language whatever it is so I can crank put this into a compiler compiler and out comes a scheme compiler the
reason professor hilfinger doesn't want you to call it that is that there's a whole other aspect to compiling which
has to do with what are these forms mean so knowing what a lambda expression looks like doesn't tell you what scheme
should do with the lambda expression and that comes from a formal semantics notation which is the other half of it
okay but this half generates the parcel the thing that looks at stuff that you
type in and figures out what kinds of expressions are involved so now you
basically write one compiler that's sort of the universal language compiler and then you just write a BNF for whatever
language it is that you want to compile so this is the ultimate I think in data directed programming a big big important
idea see you Friday
UC Berkeley