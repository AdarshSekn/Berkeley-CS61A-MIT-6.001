Transcript


um welcome to chapter two um chapter one was all about
abstractions for flow of control in a program chapter two is about data
abstraction um and the mechanisms we have for that so um that'll be a little
bit of a change of pace um and I'm going to start by trying to
introduce the idea of what data abstraction is so um up on the screen
you see a very simplified version of uh counting the number of points in a hand
like in the 21 project simplified leaving out Aces and picture cards um so
I could just keep the thing strip down to its Essence um namely uh if the hand
is empty then its Point count is zero otherwise we
add um oops oh
yeah but last of last of hand so but last is um leaving off the
suit so it's the rank of a card of the last card in the
hand um I'm doing it right to left only because it makes the example work out
nicely um and we add that to a recursive call to Total hand for the rest of the
cards so take one card take how many points it is add that to the number of points in the rest of the hand okay
simple um the trouble with this is probably completely
apparent um is oops doing that there's this call to buttl right here which
means the rank of the card as opposed to the suit of the card and there's this
call to but last here which means something completely different namely the rest of the
cards okay so the form of the program doesn't
really help you understand that and in particular if you imagine that this procedure is just one of a thousand
procedures in a big complicated program and for some reason um you decide uh
that you're going to read the hand from left to right instead of right to left um
you want to change some of those butt lasts to butt first but not others so
you have to find the ones that are about hands and not the ones that are B cards and that makes things a little complicated let me just
um show you that it works it does so it's 3 + 10 + 4 is
17 um so now what I'm going to
do is rewrite it a little bit um this is basically exactly the
same code the same algorithm but what I've done is defin some synonyms for last and but last so
here instead of but last it says card rank namely the rank of the
card how many points is it worth and this here instead of last we have one
card out of the hand and here we have a recursive call on
remaining cards of hand so not only is this much easier to read but if I change
my mind about how I'm going to go through hands or about how I'm going to represent cards instead of having to go
through all thousand procedures looking for every buttl and trying to decide
which kind of buttl it is I can just change uh these definitions either um
the ones here that are about cards or the ones underneath it that are about hands of
cards okay
yeah if I made an internal definition of um
those things that are highlighted it would work and yes it would just like any internal definition yeah I wouldn't
do that though because um remember we're imagining a thousand more procedures
that are all about cards and suits and I want to use these consistently for all
of them so I wouldn't do it as an internal definition I would do it this
way okay all right so
um I haven't really changed anything um I just made up some synonyms and
because of that I have more readable code and I have more maintainable code
because uh I can change one of these two abstractions namely the one for cards
dividing a card into a rank and a suit or the one for hands dividing it into one card and the rest of the
cards um well the next
step oh sorry so these procedures card Rank and card suit and so on these are
called selectors a selector for a data type is
a procedure that takes an instance of this data type and
pulls out some piece of it so it selects one of the parts like selecting the rank or selecting the suit
of the card um an abstract data type means that it's one that isn't built into the
programming language it exists only in the programmer's
mind so scheme doesn't know anything about cards or hands scheme knows about
sentences um and I'm using those words and sentences and I'm using those to
represent uh card and hands so these are selectors and then the next step is that
if I'm going to use these selectors it's really kind of cheating for me to use a
quoted sentence like this as the argument to Total hand because if I now want to change
what a hand of cards looks like um my input to Total hand isn't going to
reflect the change that I made so instead of that what I should do is also
make Constructors so here we have the Constructor make
hand which is just sentence and here's make
card and I actually put a little frill into it that instead of just saying hscd
you can say hard or Spade or diamond or club and and it takes just the first
letter of that um as the representation of the
card so now um I can call Total hand
this way um so let me actually go ahead and load this all
up
and now I mean this looks like a step backwards because I had to do a lot more typing instead of just saying quote 3H
10 c4d I'm now saying make card three quote heart and so on um but again it
means that I can change the representation and my program will still work
I want to some programming languages actually provide a feature to let you specify
abstract data types in your program and then enforce them so you can declare
some variable to be of type card and then it won't let you say first
or but first or last or butt last of it you have to say uh card Rank and card
suit and so on scheme doesn't do that um knock on wood there's a new Revision
in the works um that may do something along those
lines but um scheme doesn't do that uh and for our purposes in this course
that's a good thing because it kind of makes you pay
attention to the abstraction so the language doesn't act
as your conscience you have to do it yourself um okay
okay now just to make the point here I'm changing the
implementation of cards I'm leaving hands alone but now instead of a
word like 3D for the three of diamonds I'm using a number between zero and
51 and 0 to 12 are the hearts and 13 to
25 are the Spades and so on okay so if I
um copy these
down the important point is I didn't change uh total hand at
all and yes
I can now run total hand and still get the same answer even though make
card for quote
diamond is now 30 instead of being 4 d
okay so this is just to prove to you that I can change the repres representation and as long as I
consistently use the constructors and selectors for my abstract data types uh
changing the representation doesn't require me to change every single procedure in the program okay that's
abstract data types
questions easy
right good okay um so before we go on and talk
about Pairs and list let me take a moment out to talk about the fact that a
week from Wednesday we're having a midterm um I know Pairs and L are more
fun um so here's some things about the
midterm that you need to know um it covers everything up through
this week so it's up to an including the homework that you're going to do this weekend and turn in on Monday but it
doesn't cover uh the lectures of Monday and Wednesday of next week that's Point
number one uh Point number two um you get one of the questions ahead of
time this is question zero worth one
point
okay so one point for your name that should be pretty easy right uh
your class login for this class um every so often we get a cs61 C- something I
won't do um your ta's name if you're one of those people who never goes to section um make an exception this week
and learn your ta's name and your lab section number not what day and time it
is but a number uh that's somewhere between 11 and I think
21 something like that um so those are the things you have to know for question
zero and you get a point because if you do know those things and you fill out the form correctly it really helps us a
lot in entering grades and in getting your exam back to you afterwards that's
why we need to know your ta's name and your section number so that we can put the exam in the right pile to be given
back to you um we are going to do our
best to get this first midterm graded uh
before Friday of next week because that's the drop deadline which is one of the reasons we
have an exam this early in the semester um don't take that as a
um precedent for the later midterms where there isn't any such pressure
um and one last thing I think um this exam
features a group component you should by now be in a group of four people from your section um and you are going to uh
take part of the exam in your group and the way that's going to work for this midterm is as
follows um first first you're going to take the entire midterm individually and then we're going to
collect those and then you're going to redo one or two of the questions in your
groups and um your grade is a weighted sum of the two
scores um unless your individual score is better um that that probably isn't
going to happen but if it does you'll get your individual score so don't panic
so um it would be a really good idea for you to get to know the people in your
group that'll help you in the exam okay I think that's it are bad
exams
um okay uh every programming language has some way to build up data structures out
of pieces um and you may have learned before
programing language that uses arrays with indices and so on you know for IAL 1 to 10 x of by blah blah um scheme we
do it we do have those actually you'll see later but the main data aggregation
mechanism that we have is something called a list um and lists are made up of pairs
so let me start by showing you a
pair this is a
pair and it has typically an arrow coming in and some arrows going out and
so the book uses the example of rational numbers um so if we wanted to represent
the number three fourths we might put a three here and a four here okay that's a pair
um even though this is not an abstract data
type it's a I guess concrete data type it does have Constructor and selectors
the Constructor for pairs is called cons which thens for construct so you can see
that this really is the kind of the key data aggregation mechanism um and the two
selectors are called left and right no they're not that would be too sensible
they are called car and
cter um why are they called that you want to know well the very first implementation
of list was on the IBM 704 I think
computer um which had a register that was divided into
pieces it had a little piece and then a big piece and then a little piece and then a big piece and the little ones
were called the prefix and the tag which you don't have to worry about and this one was called the
decrement and this one was called the address so those names stand for the
contents of the address part of the register and the contents of the decrement part of the
register um the one on the left is the car and the one on the right is the
cter don't ask me why um it's before my
time um the reason that these names are still in use despite how stupid they
are is that um we can build data
structures by hooking these
together and let's say this pair is called p and I want to
know what's down here well this is the cutter of the car of the cter of
P otherwise known as the kadat of
p and it's because you can do things like that that these otherwise stupid names have last have lasted but but
having told you that I should also tell you that you're never going to write
kadat because if you do you're probably breaking a data
abstraction so probably what this really is is something like the
y-coordinate of um the end point of some line segment or something like that
right and so you would say instead of kadat why coordinate of end point of line
segment um
okay
thiss
so in the library is this helpful procedure that teaches you how to
pronounce these names so this is could a DAT
um not to be confused
with CA dadar and so
on um
okay so what's in the top half of the screen here is an implementation of
pairs supposing we didn't have any kind of data aggregation in the language at
all um surprisingly enough that's okay you don't need it um this code is in the book except uh
they haven't invented quote yet and so they use zero and one to represent car and cter um but since we do know about
quote we can use car and cter um so if I were to uh read in this file
it would Define con and car and cter representing a pair as a
function um this
function that takes either the word car or the word cter as an argument and it
returns either it's you know X or Y the car or the cter of this pair and then um
we can Define car and cter the selectors uh simply as
um a little syntactic wrapper around invoking the pair with the word car as
its argument um I'm not going to spend a lot of time on this it's in the book uh it's
just really really neat that you can do this um and it's an illustration of the general point that if you have Lambda in
your language that's all you need um in principle you can derive everything else
from that um
okay the main way that we use pairs though is not for things like rational
numbers but as the implementation strategy for a list a list abstractly is
just a sequence um in the book and in my notes you will find a lot of pictures
that look like this
this is an abstraction diagram and what goes above the line here is what the
abstract type is that we're implementing like say
sequence boom boom boom boom okay bunch of things in parentheses
looking suspiciously like a sentence for reasons we'll talk about in a moment um and the way we're going to
implement that is this
way so a list a sequence of n
elements is a set of n Pairs and the car of each pair is an
element of the sequence and the cter of each pair is the next pair along except
for the very last one whose cter is this special thing called The Empty list now
the empty list is not a pair but it's the only list that isn't a pair okay so this is kind of a recursive definition
of list the list is a pair whose cter is a pair or the empty
list um now what goes in the middle of the
diagram is the constructors and selectors that Define this abstract
type um and the reason they go there in the middle is these are the only
procedures in your program that are allowed to know know both what abstract
type we're implementing and how we're representing that type
concretely so when I have um cards represented as a word with a rank and a
suit I have the Constructor make card and the selector card Rank and card
suit and those three procedures are the only ones that know what a card actually
looks like in my program um all other procedures either are part of a lower
down abstraction like words or are things that use cards
like total hand um but total hand doesn't know what
a card looks like it only knows that they have ranks and suits that are represented somehow or other okay so the
things in the middle are the implementation of the abstract data type
now how about this Implement uh this abstract data type of list
um well what there should be is a
Constructor called list and selectors called first element
of list and rest of list um Instead This is really the only thing in
the language that's quite like this we
use consar and cter which is um what in other contexts we would call
a data abstraction violation you lose points if you do that um because you're
not respecting the abstract data type the reason we treat lists specially is
that lists are only sort of half abstract so the language really does know about
lists and let me show you what I mean um suppose I say um I want to do 34
so I say cons 34 I get something that looks like this
parenthesis and then the car space period space and then the coder close
parenthesis this is not a list of three things that period in the middle is a
piece of punctuation just like the parentheses there's only two things here the left thing and the right thing um so
don't be confused about that but now if I
say this I don't get open parth 3 dot
open Brand 4 dot open brand 5 dot open close close close close I just get 3
four five because um we have this special shorthand
representation for pairs that are hooked together in this particular way to form a
list um and since the language knows about
lists um it's not as if we're going to change the way lists are represented so we don't have to treat list as an
abstract data type
okay
um we actually do have other Constructors for lists
yes how is a list different from a sentence okay um a sentence
is a list in which the elements are constrained to be only
words okay [Music] so um well
here if I do this I get this interesting
I don't get a list of four elements I get a list of three elements the first of which is a
list because if you look at the picture in the abstraction diagram of what a list looks like the car of the pair is
one Element even if it is itself a list so one difference between lists and sentences is that you can have lists of
lists okay that also means that you can get in trouble so if I say
cons three four
five I get this thing with a dot in in the middle of it which isn't what I wanted I wanted to put five at the end
of the list but I failed at doing that because the use of pairs to make lists
is asymmetrical the car of a list is a different kind of thing from the cter of a list the car is an element the cter is
a sublist okay
yeah okay why didn't I get he's asking in this example Why didn't it come out
oops this example Why didn't it come out open open three four close open five six close close
um that's what I'd get if I said this
list okay so list is another Constructor for lists it takes any number of
arguments it's a little bit like sentence in that way and it constructs a
list in which each element of the list is one of the arguments so if you give it six arguments you get a list of
length six okay con remember look at that picture again of
how we make lists out of pairs so if I say
cons to produce this pair right here okay what I'm doing is I'm saying
stick one new element in front of this whole
list okay so when I use cons to make a list the first argument is an element
the second argument is an already existing list so just add one element to the
front there's also a third list Constructor called
append this acts a little more like sentence it makes a list of the elements
of the arguments um sentence is different
because uh sentence will accept words as well as lists as
arguments and puts them together um in fact we
can do I not have it
here
here's an implementation of sentence um and at its core the implementation of
sentence uses a pend oops I lost my
person where it is okay so the essence of it is right here
but since aend only takes lists as arguments first we say is a a word if so
make a list of length one out of it and call sentence again is b a word if so
make a list of length one out of that call sentence again so by at most the third time through we have all lists and
then we can call a pen okay
um okay so three
Constructors cons list and a pend and
um you're probably going to have a wrong intuition about which is the most
useful the one that seems the most obvious is list um you know I want a list of four
elements I say list boom boom boom boom the problem with that is mostly when
you're writing a program you're not making a list of a fixed number of
elements you know you want your program to work on any number of elements list is only good if you know
ahead of time how many elements they're going to be so for example you have an abstract data type
which is a point in three space so you represent it as list of x coordinate
y-coordinate z-coordinate that's a situation where you might say list number number number
okay or you know expression as value as a number whatever um but mostly you don't do that so
mostly list is the least useful of them a pend is occasionally useful
because you did some calculation for each
element of an existing list and the result of those calculations in each case was a list and
now you have a list of lists and you really just wanted a list of the underlying data and then you flatten it
using a pen so that's sometimes useful but it's going to turn out that the most
useful of all is cons because uh you're writing a
recursive program to go through a list structure just like what we did with you
know squares um we said you know sentence of
the square of first of nums and squares of but first of nums you do the same
kind of thing where it'll be cons some function of car of list onto recursive
call of cter of list and that'll be a typical pattern for recursive list procedure so that's the one that's going
to actually be useful most of the time
um
okay now let me talk about why did we bother inventing sentences because lists come with the
language um why did we make this whole extra data type and
um if you look at the textbook forget about my lecture notes look at just look at the book chapter one is entirely
about numbers um and so they have some you
know pretty mathematically hairy examples about derivatives and and
iterative improvements of square roots and stuff like that they do that because
while you're just learning about the control mechanisms of the language they don't want you simultaneously to be
struggling with the representation of data in particular with the
asymmetry of lists so one of the things you're going to do in lab is write a
function to reverse a list and that's really easy for sentences because you can take the word
at the front of the list and stick it at the back of the list if you try to do that straightforwardly for lists you end
up
um with something
like this example where I tried to stick five at
the end of the list three four and I failed okay so um they wanted you not to
have to see dotted pair notation um by
mistake at the very beginning of the course so they get you all up to speed on control and then introduce dat
um I thought when I started teaching this class we should uh have some more interesting examples from the beginning
um and so I wanted a foolproof data structure so like lists but not lists
because they're not foolproof and the idea actually came from logo which is a
programming language for kids that deals in words and sentences and uh we just
implemented that data those abstract data types based on
the things that scheme already has um so now that we know about lists most of the
time you'll just you know you'll use constant car and cutter if what you're
dealing with is the sequence although
um we might ask you an exam question about lists of sentences to see if you can figure out you know say cons and
when to say sentence
um so that's the idea that that we wanted a really simplified data structure and I think
it's worth talking about that not just to satisfy your curiosity about it but to start you thinking about what's
involved in designing a programming language and how might you make
different design decisions depending on what you're trying to program so we're trying to you know
teach a freshman class um and that means what we need is a little bit different
from what we would do if we were you know programming in Industry using
basically the same language
questions wow somehow or other I'm way ahead of
time that's good
um okay uh let me start talking a little bit about box and pointer diagrams this
thing is called the box and pointer diagram um the pairs of the boxes and
the arrows of the pointers um and one of the things we want you to
be able to do is draw these diagrams um either explicitly in response to a
question like draw the box and pointer diagram for such and such or to help you answer a question by really
understanding what a data structure looks like um so here's how we draw a
box
let's draw the boxing pointer diagram for
this
okay list first thing I'm going to do is I'm
going to count elements one
two three four five six
elements okay not elements of elements just elements of the whole list
so since there are six elements I'm going to go ahead and draw
the spine of the
list here it is okay first step I get it right
yeah okay now I can start filling these
in um it doesn't really matter now what order I do it in so I'm going to start
with the easy ones a and seven are elements of this list
how about the empty list well when we have an empty list as a piece of a pair we just put a slash
through the corresponding half so usually you see a slash as in
this pair in the cter of the last pair of a list but this time it's in the car
because the empty list is an element to this list okay all right now let's do 34 that is
itself a list of length two so I'm going to go ahead and
draw its spine length two and then fill in the elements very
four how about this how many elements
two second element is just W the first element do a list of length
one so here it is a spine of length one in which I'm going to put a
b and last but not least this is a list of length
one and its one element is this
list of length
one one
more okay that's a do it basically start at
the top draw the spine first work your way
in um
Okay so crucial little details about boxing pointer diagrams first little crucial detail is
this thing this is called a start Arrow it's really important to have one
so that we can tell where the beginning of your diagram is especially when they get complicated and things kind of wrap
around all over the place so start Arrow don't forget secondly most important of all
there is no such thing as pointing to half of a
pair so this arrow for example is not a pointer to the car of
this pair even though it happens to come in at the left it's a pointer to this entire
pair okay um if you wanted a poter to the car of
the pair that would be this
this is the car of that pair it's the thing that this Arrow points to okay so no such thing as a poar to
half of a box
yeah what if he's asking you're pointing to a box that that has a slash on the
right there's no such thing as pointing a half of a box this Arrow points to this entire
pair okay um okay what
else that's it okay questions
yeah great uh what can go in a list answer anything yes procedures can be elements
of lists lists can be elements of lists true and
false can be elements of lists right and furthermore even one particular list can
have some of each of those things so lists don't have to be
homogeneous um yeah that's the nice thing about list they can have absolutely anything you want in
them okay
question yeah
okay the difference between a pen list and cons again cons is for the situation in which you
have a list and you want to add one new element at the
front so you can think of it as a join new element old
list list is you're making a fixed length list and you're explicitly saying
what each element is boom boom boom boom a pen you
have um a bunch of lists and you want to put them together
but you don't want a list of lists as the result you want a list of the elements of the
list what if those elements are actually list that's fine it it doesn't flatten all the way down it just takes the
elements of the list whatever they are okay
okay um remind me next time to talk about higher rotor functions and last
week I lost uh a power supply to the laptop that lives in here and if anybody
happens to have seen it let me know
