Transcript


okay good afternoon so this is where we left off last time on the board is the
chart of the problem we're trying to solve having lots of different data types and lots of different operators
and that gives rise to M times in different ways to do things and trying
to keep a handle on all of that and we've looked at two different organizing
principles the first one was take vertical slices through this table and
this the book calls conventional programming again because this is how
you do it if you don't think very hard because of that noun-verb distinction
that everybody has in their brains so we organized around the verbs and we write
a procedure area that has built into it all the area formulas for every possible shape that's not so good because if we
want to add a new shape we have to go edit a bazillion procedures and we're bound to introduce bugs and things that
used to work so instead we have this idea of data directed programming and up
in the top half of the screen you see data directed programming as we're using it to solve this problem and just to
remind you in the bottom half of the screen we see a chunk of a completely
different way of using data directed programming in order to automate the
writing of compilers for programming languages so instead of having to write each compiler for scratch from scratch
we write one generalized compiler it's
it's an extreme example of generalizing patterns that I talked about back in
week 2 when we introduced higher-order functions and started with generalizing the pattern of finding areas of shapes
by introducing an extra variable that does what the shape is this is an extreme example of generalizing patterns
where we just build one compiler that can compile any language by virtue of an
auxiliary data file like this one in the bottom half of the screen
that describes the syntax of whatever particular language we're trying to compile and so these days every
specification for every programming language has an appendix that says here's the BNF for this language and it
looks something like what you see on the screen there I just should point out
that we're kind of privileged in having procedures as a datatype in our language
because we can put in the table a direct
executable representation of what it is we want to do in this other kind of data
directed programming exemplified by what's on the bottom half of the screen you have to write some more software to
take this notation which is just you know strings of characters and turn it
into something executable that actually compiles your program and for us the
only function like that we need is the little five line operate procedure where
the cursor is blinking that looks up the thing in the table and if it finds
something it just invokes whatever it finds directly on the operand okay so
that's kind of nice and it makes data directed programming particularly easy for us so easy that it probably doesn't
feel like much of a big idea and now is the other reason I wanted to show you the BNF egg to impress upon you not only
that it's a more general idea than just solving this particular problem but that
it really is a big complicated you know it was a big step forward in thinking
about computing when they invented it okay so if you look at this chart and
you see okay there's one way to take the whole chart as data and there's another way to do this by making vertical slices
it's bound to occur to you what happens if we make horizontal
slices through the table it sounds like
a pretty strange thing to do but once you have this idea of slices what about
that kind of slice that's our next big idea
it's called message-passing and let me
show you how it works first of all just
through the reminder we had these two procedures area and perimeter then merely call the operate procedure as a
kind of syntactic sugar notation
something that's purely notational that we don't need to do the job but it just looks more like what uses one that's
called syntactic sugar and it led to the famous aphorism by Alan Perlis that
syntactic sugar leads to cancer of the semicolon - those of you who've
programmed in other languages will understand so it's
so in order to do message passing we're going to change the way we create
individual shapes in our system of notation so for conventional and for
message passing style we just use the idea of tagged data so we had something
that looks like this square that's the type tag and for that's the side of the
square okay and that would be a shape and now what we're doing is we're going
to represent shapes as procedures so if I say define s for do you make square
for what's the value of s for well it's
a procedure it is to be exact this
procedure with four substituted for side
similarly now I can say define s five
makes where hardest part about this is
spelling square and I get a different
procedure it doesn't look so very different but it's a little bit different and it does behave differently
because here we've substituted five for side and the three places where it
appears here ok so you've seen something like this before back when we introduced
pairs and I said and the book said we actually don't need to have pairs as a
primitive feature of our language because we can implement pairs using lambda and Burma so we said defined cons
of a B to be lambda of message if the message is car returned a if the messages could or return B we're doing
the same thing here we're representing a square as a procedure that takes a
message as an it and then it says if the message is
area and here's the formula for the area if the message is perimeter here's the
formula for the perimeter and similarly oops make circle is the same thing it's
also creating one of these message passing procedures except that the
formulas are different they have PI in them so instead of our side squared it's
PI R square pi radius squared and instead of side times for it's two times five times radius okay any questions so
far about how we're representing shapes so
I'd like you to convince yourself first of all that this way of representing shapes is in fact a horizontal slice
through this conceptual table that what we represent a square as something that
knows all the formulas for all the operators on squares in this simple
example there are only two of the Marianne perimeter and we represent a circle as a horizontal slice on the
circle line that knows all the formulas for circles so now we have to do is
figure out what happens how are we going
to make it work for me to say area s 5 and still get the answer that I want and
the way that that works is really kind of beautiful here it is a much simpler
version of operate the first operate wasn't very complicated but this one's
even simpler because an object now which
is the square or a circle or whatever is executable it's a procedure and so we
just invoke it with the operator which is a word as its argument
so when I say area s5 what I'm really
saying is operate quote area s5 and that
in turn is saying invoke s5 with area as
its argument okay so all these three things that I've said on the bottom half
of the screen are the same questions
yeah okay how is area defined I
inherited this old definition of area
left over from data directed programming I don't have to change anything except for the operate procedure that's kind of
cute good question though any other questions okay moving on um
why on earth would we want to do this so one answer is now adding a new shape
is easy if I want to do with hexagons I don't have to go and modify the existing
procedures at all I just write one new procedure make hexagons that has all the
formulas for hexagons in it so if I'm adding a lot of datatypes and I'm not
adding a lot of operators this might be the way to go conventional programming it's easy to
add new operators you don't have to modify any existing code you just write a new operator procedure and this is the
opposite but a much more interesting answer about message passing is that
we're going to see next week the message passing is at the heart of something you've heard of and may be used called
object-oriented programming which is the next big programming paradigm so this is
something we have to understand as a precursor to that who's used object-oriented programming
before audio who knows anything about how its implemented how you know they
write a Java code my TAS do ok that's good so even those of you who use the
object-oriented programming before are not going to be bored as we start exploring it next week because we're
going to teach you how it's implemented and actually turns out not to be very mysterious so one of the goals of this
course is to demystify the different programming paradigm help you understand how they work okay so that's message
passing the next thing we're going to do is go back to data directed programming
for a bit and talk about a problem that we've so far swept under the rug which
is a lot of times you have operators with two operands like for example - I'm
choosing - rather than plus because it's non commutative so it makes the issues a little clearer so let's say I want to
add a minus column to this table I'm
going to leave these blank squares and circles you know do - on but what we do
do - on is numbers numbers for purposes of today's discussion come in four
flavors integer rational real complex ok
so if I have four kinds of numbers how many rows do I have to add to the table
depends how I do it is the answer the most straightforward answer is 16
because there's nothing that says that the two operands are going to be the
same type I can do integer - integer integer - rational integer - real
integer - complex rational - integer rational - rational rational - real and
so on four kinds of first operand times four kinds of second operand is 16 lines
we have to add to the table and furthermore the labels over on the left
column here can't be just integer we have to say what both of the types are
so we're going to start using lists instead of words as the label for the
rows of this table so we're going to say something like integer integer and the
next row might be blessed integer
rational and so on okay 15 of these down
to complex complex if we do this of course we're going to be uniform in the
way our table works so we're going to use lists even if for the operators with
one operand so that our operate procedure which in the book is called
apply generic and works for this two operand case has a consistent theory
about what it's looking for okay so if types are these words integer rational
real complex and we put them together in a list that is called a type signature
and those of you have used languages
that call themselves object-oriented but don't believe in message passing
will will be familiar with that term that the procedure that you write has a type signature which is all the types
that you declare for all the arguments of that procedure ok so that's a type
signature it can be you know it could be three operands the system is extensible
to solve any problem by the way speaking of numbers of operands is another little
table in the literature mostly you will
see something with one operand called a unary operator something with two
operands called a binary operator so
almost everybody calls them the problem with this nomenclature is that you all know that binary means
something completely different in the context of computers it means ones and zeros and there's
nothing about an operator like plus that has two operands that has anything to do
with ones and zeros you might not know that you nuri also has a similar related
meaning in computer science you might not know that because base one seems like a strange idea but there actually
is such a thing and you'll learn about it in I guess 170 or maybe 70 so these
names aren't very good they're confusing and so cool people call these Mon attic
and die attic operators these names were proposed by
Ken Iverson who invented the important but obscure programming language APL and
they're great names and they don't have any other confusing meanings okay so now
we're doing dyadic operators and so we have these type signatures so just for -
we need 16 of them and if we want to do
plus minus times divide that 64 cells in this table to keep track of that's a
real pain in the neck and people mostly would rather avoid that kind of work and
we can avoid that kind of work if we're observant and we notice that numbers
have a special property namely there's
the integers all integers are rational
right so the integers are a subset of the rationals all rationals are real
lots more real than rationals but every rational number is a real number and furthermore oops
every real number is a complex number right now
notice by drawing this chart in this way I have done something that many
programming language designers don't seem to understand so they think that 3
& 3.0 are two different entities but
that's not true three point zero is an integer
maybe it's represented differently in the computer but that's the computers problem not yours
mathematically three point zero is the same number is three and your language
ought to think in those terms because the purpose of computer science is to
enable you to solve problems with computers without thinking about computers without knowing anything about
computers just thinking in the language of the problem you're trying to solve so
that's sort of the forward march of computer science is you having to think less and less about how they represent
things inside the machine instead spend time thinking about the problem you're
trying to solve okay so we're going to take advantage of the fact that these four numeric types happen to form a
nested sequence of bigger and bigger sets and we're going to do it this way
first we're going to find our truck there we go we're only going to have
four rows four numbers in the table so we're going to forget about type signatures and we're just going to have
integer rational real complex and if you
remember the way they build up these types in the book 4-2 subtract two
integers we just use schemes - and for
rational numbers we had something called - rat and for reals we just use schemes
- and then for complex we had something like complex - or maybe it was just C -
all right well what if we get an integer
- a rational what are we doing that case well the next thing we're going to do
besides plus minus times divide we're going to have two more columns in our
table one is called raise and one is
called level okay level is going to be
used to tell us about this subset relationship what's the subset of what
and the way it's going to do that is we're not even going to put procedures
in here we're just going to put one two three four okay bigger number bigger set
okay raise
as for each level how do we convert this to the next level up okay
so this is going to be in maps to make
rat in one right to get an integer to a
rational number we do integer divided by one that's irrational okay the raised
procedure for rational has to raise it to a real number and how do we do that we do rational number maps to divide the
numerator of our by the denominator of our okay so this gives us a
floating-point representation of that integer because this is the scheme
built-in divide actually when I say that I'm lying we went to some pains to make
sure that when you say slash what you get is not an exact rational because many versions of scheme probably most by
now actually you support exact rationals as a built in type but ours doesn't on
purpose so that I can give this lecture to raise the real number to a complex
number what do I do
x maps to make complex x0 right so it's
X plus 0 I or if you're an electrical engineer X plus 0 J complex we leave
this slot empty there's nothing in here because there's nothing to raise complexity that's as far as we get okay
so now we're calling a dyadic operator
we get two operands we extract their types and that gives us a type signature
so what our operate procedure has to deal with is still to begin with the
type signature then what it's going to do is for each word in that type
signature it's going to look up level so if we have let's say an integer and a
rational we get back one and two respectively okay
whichever of those numbers is smaller we look up raised for that data type and
apply it to the value that we have so if what we have is an integer well let's say an integer plus a complex just to
make it more interesting so I have integer and a complex the answers are 1 & 4 1 is smaller so I call raise on my
integer and that gives me an exact rational like let's say it's 5 I get 5
over 1 okay well now I recursively call
apply generic which is the books name for what I've called operate here and
now I have a rational and a complex so we look at their types I'm sorry yeah we
look at their types rational complex and then we map level on that type signature and we get 2 for the type the novels are
still not equal so I do the same thing I find the small level which is the rational number and I
call raise on it and that converts it to
a real number so I started with five and then I had five over one and now I have
the thing that Prince is 5.0 which is five in real representation and now I
recursively call a pledge and Eric and I have a real and a complex and I look at
their levels and that's three and four still not the same so I take the smaller
one which is three and I raise that operand again now it's a real number
that I'm raising so I say make complex five point zero zero and I get now the
answer five point zero plus zero I and now I call make I call apply
generic again and we look at the levels of the two types the two types are now
complex complex so their levels are four four they're the same so now I can go
ahead and look up how to subtract two complex numbers and apply that procedure
to the two numbers okay questions about that yeah
okay good question his question is what if instead of just raising one level at
a time I make procedures for every pair of types that raise the smaller one to
the higher one we could do that it would give us three plus two plus one six
procedures - right instead of three that's not the end of the world so it's
compared to three but it's a little more elegant since since these things are
subsets of each other to kind of take advantage of that but we could do it that way you're right so we could we could have pipe
signatures in the table only for the raise operator and I would directly
raise integer to complex or whatever that would actually be better in one way
because this mechanism that I've just described to you has a drawback and that
is if I take the exact rational number one third or even it turns out the exact
rational number one tenth and convert that to real number computer form I get
an inexact answer right with one third that's true even for you no ordinary
decimal elementary-school arithmetic you get zero point three three three three three three three three etc right and so
if we represent it internally as zero point three three three three three three that's not exactly right you will
learn a little bit in 61c about the fact that not exactly right answers cause a
lot of trouble because you're thinking well three point I'm sorry zero point
three three three three three three three that's close enough that's more precision than I care about but that's
true if you only ever do one operation on your data tip what happens in a numeric especially in
scientific computation is you you you know multiply that one-third by
something and you add something else and you divide by something else you had something else and you subtract a third
you know and you get something that's like way wrong well I'm sorry no you
don't you get something that's way wrong if you do something like taking the tangent of one of these in exact values
why because the tangent function has a huge slope right everybody remember that
from high school loop and then goes back down here and goes bloop again right so
except for right near those zero crossings a teeny little error in the argument to tangent turns into a huge
error in the return value from tension okay and and if you use that in a more
complicated computation and that error propagates before you know it you have zero digits of precision avoiding that
is the job of a field called numerical analysis which very few people actually
choose to go into but it's important that some people go into it because
otherwise our next generation of computers will just produce crazy wrong answers which is what used to happen
until professor Khan in our department
sort of laid the groundwork for dealing
with imprecision and computers in a systematic way okay so yeah it would be
a little bit better if we wanted something like if what we really wanted to do is raise our rational number to
complex it would be better if we could make it one-third plus zero I we're live
in exact 1/3 as the real part that's a little bit tricky because it's no longer
the case that the components real part and imaginary part of our complex numbers
are just plain old numbers which is what the implementation of complex numbers in
the book assumes Edison's that you can just do plain old plus minus times
divide on real part or imaginary part of a complex number so now we have to take
a real part and imaginary part and do this complicated thing just in case the real part is an exact rational rather
than an inexact real okay so the the
sort of bottom line answer I've given a very long answer to this very simple question the bottom line answer is
there's no way to do it that is perfect in every respect you can do it
absolutely perfectly as far as the results are concerned by having sixteen
rows on the table for all the different type signatures but that drives your programmer crazy so instead we want to
take some shortcut and the simplest shortcut is this one I presented here
where we just have one raised operator that raises by one level and we keep calling that until we get to the same
level but a slightly more complicated way would have six raised operators and
you would look at the type signature to decide which one to use and then four of
each of the arithmetic operators plus minus times divide okay
okay so one more thing on this on this subject of raising and that is we're
really lucky that these numeric types form a nest of subsets of each other as
they do that isn't the case in every situation and the book gives the example
of shapes where as part of the universe
of shapes we have quadrilateral and then
there are various special kinds of quadrilateral like for example
parallelogram and trapezoid I think it
makes much more sense if you consider parallelograms to be trapezoids but none of the books do that for reasons that
escape me and there's other ones like kite that are special and then underneath parallelogram there's a thing
called a rectangle and then there's a different thing called a rhombus which
in case you've forgotten high school geometry is a parallelogram in which all the side lengths are the same and then
is this thing called square which is both a rectangle and a rhombus there's
equal sides and right angles so what should the Rays operator do for a square
well it depends when we want to combine it with what does it mean by the way to combine shapes
what kind of operation would you ever want to do that combine shapes answer
you're writing a computer program that does some kind of graphics and sometimes
you have a shape like this and then you
want to put another shape overlapping with it
and you'd like the result to be this
okay so you see this one on top of that one in order to do that you need to get a
handle on this shape which is the set
difference between the rectangle on the square so it's rectangle minus square in
a certain sense is what this shape is in the set theory kind of - though not the
numeric kind of - but in order to do that is the square this is a rectangle
have to raise it it's also perfectly possible that I might have had a rhombus
over here and I want to overlay that with a square and now I have to do a
somewhat different calculation to get the result that I want okay so this this picture that I'm drawing on the top
board now is something that actually comes up in writing computer programs if they have anything to do with graphics
well if they have anything to do with versatile graphics for many ordinary
purposes we solve the problem by having no shapes other than rectangle and that
by the way is also a solution to the numeric problem we could decide to have no numbers other than complex so if you
type in 3 we represent that in the computer is three point zero plus zero
point zero I if we do that then there's
never any issue about types at all and I have to go through this the cost of that again is that you can't have exact
rational pieces to a complex number you lose precision that you could have kept
so systems that use numbers just a
little bit might decide to do this thing about only complex numbers internally if you're
writing something like Mathematica or MATLAB which some of you will have used
where numbers are really really crucial to the your work and you want to get the very best answer you possibly can then
you really do have to have exact rationals as a data type and you have to go through all of this that we're
talking about okay questions you know have I forgotten
to say anything no see you next week
UC Berkeley