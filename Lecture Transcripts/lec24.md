Transcript


okay good afternoon um thank you for braving the rain those of you who are
here um actually you should think of the Rain Is a Good Thing um as being in your
interest because today is grad student visit day when the current seniors from
around the world who've been admitted to Berkeley come visit and we try to convince them to come so because of the
rain we'll have fewer grad students next year and that means more research opportunities for undergrads
so you should be happy [Music]
um so thank you Tas for handling last week while I was gone how'd it
go okay good um I want to show you one little thing that uh you may have seen
in section but maybe not and you didn't see in lecture uh and it's called in of
draw stands for environment draw so here I am at a Shell prompt instead of saying
STK I say inv draw um and what I get is a modified
STK um and then I call the procedure inv
draw and what I get is this
window which I'm going to move over if I
can huh okay what's the matter
move cool all right close enough
um well we'll just have to switch back and forth okay so now I can say things like I want don't know Define make Adder
um to be um Lambda x + x
num and here it is in the environment I add and now I can say Define um + five
to be make add
five there's plus five so if you don't like the way it's laid out you can drag
the procedures or the frames and you can move them around um so now if I say +
five of n what I don't know what that's about um
anyway it made this Frame here um and I'm getting a little confused
about what's being made when so I'll just go to Colors whoops
colors and pick red
and now I'll say + five of
two H weird and now that's in red and you can see that the new frame is
extending this Frame that b and so on and so forth so that's n of draw
um and you can use it to make environment diagrams if you want um oh
one more thing um about the midterm that you had while I was gone um it seems almost everybody uh got
wrong the binary tree question um because as the leaf nodes you had
numbers right so um if you have a tree
like like this this was a binary tree
but this thing was just a number so if you said left Branch you got three now
it's not supposed to be like that these things are supposed to be trees also um and the way you know it's a leaf
is that its left branch and Its Right Branch are both empty lists so empty list
means there isn't a child at that Branch so you're supposed to do make tree for
the leaf nodes also and everybody lost points for that and because it was
everybody um our generous ta decided that we would give everybody back a
point so um you're not going to see that in G lookup because we're not going back
and re-entering all the grades but at the end of the semester we'll give you an extra point
um yeah even though you should know this um
okay so uh now down to business sort of business we're going to play a game uh
this is called the animal game I'm going to think of a secret animal and the
computer is going to guess what it is so animal game so it's going to ask
questions about my animal um my secret animal is a parrot by the way so does it
have wings I say yes is it a parrot this is a really smart
computer um okay so now I'm going to try again
um and my secret animal is um an eagle does it have wings yes is it a parrot um
it didn't do so well this time I give up when is
it so tell me a question his answer is yes for a eagle it's not so good at grammar and no for a parrot so is is it
the national bird
thanks so let's play again and my secret animal is an
eagle does it have wings yes is it the national bird why yes is it Eagle yes I
win so we can keep going like this um
okay my secret animal is a gorilla does it have wings no is it a
rabbit sorry I give
up so does it have long
arms does it have wings no does it have long arms
no is it rabbit no I give
up okay so
um is this a functional program no how do you
know same arguments namely none different Behavior okay every time I call it I get
different behavior um so it's not functional so it has some kind of local
state information except it actually doesn't it actually has Global State information in this case because um
there's a structure of all the animals that it knows about um and initially
that structure looks like
this yes
par no
rabbit okay so that's the structure that it starts with and um so now I call it
and my ant secret animal is an eagle says does it have wings yes and
what it finds is not a question but an answer so it says is it a parrot they say no I give up what is
it it's an eagle and it says Tell me a question
whose answer is yes for the eagle and no for the
parrot so is it the national
bird and
then we get rid of this and make this point here
instead okay so that's the structure of the of the game I'll show you the code
in just a moment um there first let me tell you about the data
structures uh basically this is a binary tree right because the questions are all
yes or no questions um and the leaf nodes are animals or guesses the branch nodes are
questions so for branch
nodes looks like
this the word
branch and then a question
like does it have wings and
then a yes branch which is going to
be parrot and
a no branch which is going to be
rabbit now the leaf nodes look
like the word
leaf and then the animal
okay so this is um using type tagging to distinguish branches from
leaves and uh we're going to go through the program and see how it
works okay so
um we have a data type called
um node here and the way we make one of
these is we have two Constructors make branch and make Leaf so these are the
constructors for nodes and um if you compare what you see on the screen with
what I drew on the board you'll see that they go together and here is the initial
definition of animal list which as you see um has one branch
node and two Leaf nodes so what you guys did wrong on the midterm was to instead
of make Leaf parrot you just said paret here
um okay we also have inside here selectors so carv a Noe is its type
which is either the word leaf or the word branch and we have skipping down here a moment uh procedures Leaf
question mark and Branch question mark that says is the type leaf or is the type Branch now um if it's a branch then
it has a question which is the cater a yes part which is the cator and a no
part which is the cator if it's a leaf then it has an
answer which is the CER okay so those are the selectors for these uh binary
trees and now here comes something new up to now we said um an abstract data
type is implemented using selectors and Constructors but here's a third kind of thing called a
mutator um set yes bang it has an exclamation point in its name because
it's a mutator it changes the value of an existing structure um and set no bang and these
both call a scheme primitive procedure set car bang whose first argument is a pair and
whose second argument is anything and there's also a set cter pair
anything um that changes what's
in um a particular node so let's
um let me now kind of spell this
out so this guy points down here Leaf
parrot and this guy points to
Leaf rabbit so here's the initial configuration and now we're going to run
the program um The Code by the way is um
terrible uh which is what happens when you do things sequentially instead of functionally so and we have to do that
because it's asking questions and reading answers from the user and so on so we have to do this first this then
this then this then this so the code goes on forever which is kind of annoying but sorry so here's a helper
procedure um Yorn which is actually supposed to be pronounced y or n um
because you have to answer yes or no if you say yes it returns true if you say no it returns false
if you say anything else it says please type yes or no and it keeps asking until
you finally say yes or no it's very insistent
okay so display the question part of the node so um when we call this procedure
we're always calling it with a branch node I'm not even testing for that that's the Assumption and that's because
our initial Tree starts with a question so we're going to keep getting
at least one branch node until finally we get down to a leaf which we'll handle inside here differently so we have a
branch node display the question display a space
um call Y orn and so YN is going to be either true or false it's a Boolean uh
depending on whether the question was yes or no now the question was does it
have wings so that's the value of question of
node so um I said yes it has wings so the value of
YN is true so now
here um why is this a lead inside a lead well because I'm using the value of
YN so I could have said let Star but since the book doesn't talk
about let star uh we just expanded the let star into what it expands into namely nested lets so we have to have
value for YN from the outer let before we can examine that value in the inner
let so next is going to be either yes part of node or no part of node I said
yes so this is
next please don't draw an arrow into here thinking that you're
pointing to the car of this pair right there's no such thing as is pointing to half a pair the car of this pair is the
thing that is in the car okay
um okay so now we uh so we let next be that now we say is this a branch or a
leaf if it's a branch then what we do is very simple we just recursively call animal this
procedure on the new note so that's we had a question we got an answer now we have another
question we just do the same thing recursively because we're going to keep going we're not going to do anything interesting until we finally guess an
animal because we hit a leaf node I mean it is interesting that we're traversing a binary tree
um but the code isn't interesting it's just this little recursive called to
animal so it's a leaf node we say is it
a answer of next that's CER so we say is it a parrot question
mark let correct flag be y RN so correct flag is going to be true or false true
if this guess was correct according to the user false if not uh I said no it's
not correct um if correct flag is true it just says
I win and that's the return value I win
um but I said no it's not a parrot so new line display I give up
what is it so correct is the new correct answer
so correct is
Eagle okay please tell me a question whose
answer is yes for a eagle and no for a
parrot period new line and close the question at quotation
marks let new Quest be read
so new Quest is going to be is it the national
bird okay um what's the value of YN who
remembers it's either true or false depending on
what did my animal have wings or not this is the answer to the last branching
question that the computer asked before saying I give up the last question it asked was does it have
wings and I answered yes it does have wings so we're going to do this part set
yes bang whereas if we were talking about a non-winged
animal then we would be doing the set no Bang underne it the arguments to set yes
bang and set no bang are the same either way um what we're doing is
modifying um either the cator or the cator of the
question um so set yes bang node oops
that was wrong what did I mean to
do
sorry
oops
there so sit yes bang of node what's node node is this
guy so set yes bang of node means we're
going to change this pointer right here what are we going to change it to well there's a call to make
Branch so let's go ahead and well before we do the make Branch we have to
evaluate its arguments uh which are all easy except for this one we're do calling make Leaf
correct so let me make a pair
whose car is
leaf and whose catter is Eagle okay so that's a leaf node with
the correct answer so that's what this does so once I have
that I can do this make branch and Branch node looks like
this oops and then comes the question new
Quest and then what comes after
that there's a pointer to this leaf and then what comes after that
that is next which is sorry this is a little
going to be a little messy but I'm going to go all the way around here
to this pair okay so I've made a branch note
where the question we're asking is is it the national bird if the answer is yes
it's an eagle the new thing if the answer is no then we go back to the old gas of
parrot okay and now I can do the set yes
bang like
this okay
so set yes bang works by doing a set car bang uh when you're manipulating
lists you can you can use pairs for arbitrary data structures remember but if what we're looking at as a list set
carbang means change one of the elements of the list because the cars of a list
are its elements right set cter bang in a list means uh that you're doing
something like inserting a new element in the middle or deleting an element so
you're you're rearranging the spine in some way where it say car leaves the
spine intact it just changes one of the elements because of that and I don't
want you to just learn this as a piece of mumbo jumbo I want you to understand the because of that it's almost always a
mistake to say set carbang of some pair
to cter of something else
or set cutter bang of a pair to car of something
else okay if you do this you and what you're looking at as a list you are
trying to use a piece of spine as an element or you're trying to use an element as a piece of spine and there
are situations where that's what you want to do but they're really pretty rare um and that's a common mistake that
students make dealing with mutation is getting confused about
that okay let me stop for
questions wow your brains are all wet in the
rain okay who's getting
it who's not getting it okay the person next to you is asleep
nudum um all
right okay so that's the program um it's a lot of detail because you know it
actually does something you might want to do um namely play a game but
um the essential point is that when we created data abstraction we used to have
just selectors and Constructors and now maybe we have mutators um
so one point I want to emphasize is that you never have to use
mutation if I wanted to write a purely functional animal game what I could have done is make a
copy of the entire tree except when I get down to the place where the wrong answer was put in this new stuff in
place of the wrong answer U but that would have taken a lot
longer and it's much quicker to just um mutate the existing
structure and better too because you can write it out into a file if you want and then next time you play the game load in
the the mutated structure so that it knows about all the stuff you've already taught it all that stuff
um so there are reasons to do mutation but it's never because you really have to in order to solve the
problem um
okay mutation is messy that's the next thing to learn um
so if I say A to B list xot yote
Z I say Define [Music] B to be cter of
a so B has the value of YZ now if I say set car
b f ah can't
type the value of b as expected is Fu Z but the value of a has changed
also so I intended to change B but I changed a as a side effect because a and
b share storage um now that isn't always the case if I
said um Define um I don't
know H to be sentence quot a quote B quote
C and now I say
Define J to be but last of
H so J is AB and now I say set
car J quote
B you're going to say isn't this a data abstraction violation yes it is I
know um and now I say What's the value of J it's baz B and what's the value of
H going to be Bas BC no it's
ABC because H and J it turns out don't share storage if I had said but first up
here instead of but last then they would share storage because but first is just
cter for sentences um and so it would have worked like the previous example but but last
has to make a copy of its argument and why is that
because if I have a b
c and I make a sentence out of
them and now uh that's H and now I want
J to be just AB I can't use these pairs I can't reuse
these because we can't have this both point to
c and also be an empty list right which it would have to do if H and J both pointed
to the same place I can't do that so instead what I have to do
is make new
pairs for J um so sometimes you're sharing storage
sometimes you're not sharing storage if you're sharing storage then mutating
something may affect other data if you're not sharing storage then it
won't so this sort of thing um as you can probably imagine makes it easy to
have bugs in your program so one last pitch for functional programming if you can possibly do
something functionally you avoid having to think about this ugly
stuff about whether two lists that look the same are actually sharing the same
pairs or are as in the first example or a different pair pairs even though they
have the same elements as in the second example
um right in
particular why didn't I just say quote parenthesis XYZ here I would have gotten
the same result a list of X Y and Z and it would have been less
typing because there's a rule in scheme that says you're not allowed to
mutate a quoted list and the reason for that is um the
scheme standard allows an implementation that wants to use storage
very efficiently to whenever you quote something look and
see if it's already made that particular value that
particular quoted list and if so give you a pointer to the very same one
instead of making a new one um so that would happen for example if you have quote parenthesis blah blah
blah inside a procedure and you run that procedure once and you create that quoted list and then you run the
procedure again it might as well give you the same quoted list instead of another one on the other hand
implementations that want to be straightforward are also allowed to create a new list every time it sees
that quoted value therefore you don't know with a quoted list whether it does
or doesn't share memory with something else if you write a program that depends
on that that uses setar or set cutter on a quoted list um because you want to be
sharing values or or because your particular scheme isn't sharing values
sharing pairs between those different things um and then you take your program and move it to a different scheme
interpreter or compiler it stops working and you'll be upset so the rule is you're not allowed to
um modify a list that was made by quoting it you have to call list or call
cons or something to make lists that you're going to modify okay
um okay so two weeks ago you learned about set bang set bang is a special
form right because its first argument which is not quoted has to be the name
of a variable right so that first argument is not evaluated even though there isn't a
quotation sign in front of it um setar and set cutter are ordinary procedures
their arguments are evaluated and they are because um we have to be able to say
things like this set car could it or node to
something so that expression whose value is a pair that's
evaluated um and the second argument of course is evaluated also so it's a plain ordinary
procedure uh the exclamation point doesn't mean special form it means
mutator right so it's a warning that you're not doing functional
programming uh and again it's not a re the scheme system doesn't enforce using
exclamation points for mutators it's just a convention that you will do well to
follow okay
um so there's a relationship though between set bang and setar set cutter
namely both of them uh make your program
nonfunctional because in both cases uh the result of calling a procedure may
depend on previous the previous history of the computation so it's it it looks
at state so it's not functional um and also we're going to learn that if we had
either one of them in our language we could use it to implement the other one
um so given set
bang the way we could Implement setar and set cutter is remember way back in
chapter one they said um we could Define pairs using
Lambda you and they did what you later learned is message passing right so it was defined cons AB
to be Lambda of message um con EQ message quote
a EQ message quote car a EQ message cter B well we can add to that EQ message
quote set car bang then set bang a to the new
value right um so we can use a message
passing implementation of pairs and give it setar and set cutter as messages um in the other direction when
we look at the metac circular evaluator the scheme interpreter written in scheme that comes up in chapter 4 pretty soon
um we will see that environments the things you learned about last week are
represented in the evaluator as list structure and so if the user of metac
circular scheme uses the set bang special form we end up um set caring or set cutter ring
set caring I guess um a piece of a frame in the
environment okay
um okay so let me get back to this question
of how do you know whether you're sharing um values or not and in the
example with uh A and B down here we said that um A and B are sharing
memory so if we modify B it changes a also and we said that H and J are not
sharing memory um so how do we find what so we have to
make a distinction between two different meanings of equality that didn't used to
matter there's the kind of equality that means has the same value if you print
them both out they both look the same that's the one we've been using up to now and it's what the procedure equal
EQ question mark implements um there's also are these the
very same thing in memory the very same pair or the very same whatever and the
name for that is EQ so if I say um here's a a here's
B uh equal a I'm sorry equal B cter of A is that
true yes it's true because cter a is fuzy and B is
fuzy I can also say EQ B cter A that's also true it's true
because a and b share pairs so cter a is the exact same pair as
B whereas H and J so here's H here's J um oh well they're not the same at all
um yeah let's make a new one Define
X let
BC I should have said sentence all right never mind um Define why to be but last
of X so here's y so
equal y but last of X is true
eqy but last of X is false because every time I call but last of X it makes a new
copy so this but last of X is a different set of pairs from y even
though they print the same they both print AB okay questions about EQ versus
equality yes didn't they tell us back in Chapter 2 that EQ is for symbols and
equals for lists well yes they did tell you that um but they said it with their
fingers crossed it was a simplification um it's a rule in scheme
as in basically every list System since the beginning of time
that there's only ever one copy of a particular
symbol um different from strings different from numbers I'm talking about
symbols there's only ever one copy so when you type a symbol Into The Interpreter what The Interpreter is
doing behind the scenes is saying oh a symbol have I seen this symbol before
and it looks in a collection of all the symbols it's ever seen before yes I have let me return a pointer to that same
data structure so when you type Fu and then you type Fu again those two are
always EQ now they're also equal um but they're EQ and they wanted
you to use EQ for symbols back then because you were one of your homework assignments was to implement equal
question mark using EQ question mark right as the base case for symbols so
they needed a way to compare symbols that wasn't equal question mark um but now you know the truth about EQ which is
it's true when two things are the same place in memory the very same identical things so
we call that identity versus equality EQ says are the two things
identical um questions about
that there are all kinds of questions you could ask what about numbers what about
procedures
yeah um eqv you want to know about um you're asking the wrong person I have
never in my life found a use for eqv
um eqv
is the the attt in eqv is ignoring
implementation uh are these as the same as things can
be um and so it's kind of a halfway point
between equal and EQ the problem with eqv is that really implementing it
correctly um is awfully hard and slow um whereas
EQ is constant time right equal for lists is Theta of
the length of the list right because you have to go down cter ring down seeing what all the elements are the same um EQ
for two lists take constant time because you just have to look at the first pair of each one and say are they in the same
place so you're looking at pointers to things those of you who've studied pointers if not you'll get it next
semester um and that's just a constant time operation so EQ is really really
equal is reasonably straightforward but Theta N and eqv is supposed to be somewhere in between the trouble is
knowing whether two things are mathematically the same it's very tricky
so um what should the answer be to
this what should the answer be are they the same or
not well actually what I meant to say was eqv so let me go back and do that
oops hey
oh let's see what SDK does SDK says false they're not the same
mathematically it's the same function right um they have the same
input output Behavior with which is all we care about now if these things had local
variables right so if I had said um you know let
count be zero Lambda of nothing um setb count plus count one blah blah blah
twice then eqv should return false so in order to know whether two
functions are the same function or not you have to do some very very careful um
complicated I'm not sure if it's even theoretically possible analysis JY you took 170 is it
theoretically possible to see if two functions are the same from the I don't know
um yeah um
so so eqv is always kind of a compromise between what it should be and what's
possible and so it's kind of messy and ugly and I've never found a good use for it the other uh equality tester is the
equal sign um and that one is supposed to be true if the numbers are
numerically equal even if they're represented differently so we want um
equal the integer three and the floating Point representation 3.0 those should be
equal and and they are numerically equal um
whereas they're not EQ and they're probably not even
equal let's see no they are okay um but
there are all these different complexities by the way it's not even guaranteed uh that this will be true I
think it will be in SDK um but if I say
um
that's false small integers R EQ in STK bigger integers
bigger meaning more than 4 billion aren't and that's just an implementation
detail so you're not supposed to rely on EQ for numbers you're supposed to use equal sign equal sign will be true for
those numbers uh because it actually takes the trouble to look through the complicated
data structure that a large integer requires okay uh any one more question
yes
Define X like this
eqx I that will be true because this is the value of x is a symbol the symbol
I anytime two symbols print the same they are
EQ a list system will never make more than one Comm of the same symbol okay um
for efficiency reasons basically storage
efficiency okay next time we're going to look at how mutation that we just learned about can be used to implement
tables
UC Berkeley