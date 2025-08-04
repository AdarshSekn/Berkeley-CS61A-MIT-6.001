Transcript


okay good afternoon um this is one of my favorite weeks uh
you'll see why today um what we're talking about is trees which are kind of
two-dimensional hierarchical data structure um unlike lists which we
talked about last week there's nothing about trees built into scheme um it's
entirely an abstract data type that you can build however you want we're going to look at actually various alternatives
ways of doing it um but first let me start with what are trees for why do we
want a hierarchical data structure first reason is to represent a hierarchy so
this is um a small slice of the world tree so there's actually a lot more
countries than this that you don't see um but the first level is just the
world and then there are some countries and some countries we just hang cities
off of and in the US we have these things called States and states have cities in them um and then there's this
weird thing which is the United Kingdom of Great Britain and Northern Ireland um
and Great Britain is in turn divided into England Scotland and Wales plus a couple of uninhabited islands I think
the last Ms person died a while back um
and those have cities um so here's Liverpool you know the center of the universe
um and uh notice by the way we'll talk about this in a bit that there's a
Cambridge Massachusetts and there's also a Cambridge England um so that will get
interesting in a bit um so one use of a hierarchical data
structure is to represent a hierarchy do um here's another
one this thing is called a
binary search tree what makes it a binary
tree is that each node has at most two
children and the children are explicitly divided into a left child and a right
child so 33 here has a left child but no right child whereas 105 has a right
child but no left child um now these I'm sorry so that was what
makes it a binary tree what makes it a binary search tree is every node has the
property that the nodes to its left underneath it are smaller than this
datam and the nodes to the right underneath it are bigger than this
datam okay um that's what makes it a search tree now there's nothing
inherently hierarchical about these numbers it's not that you know 25 plus
92 adds up to 47 or anything like that um the position of numbers in the tree
is kind of arbitrary as long as it comes out pretty well balanced um you know you throw things in
at random it probably will come out pretty well balanced um the value of the hierarchy is uh if
we want to do a search for something that's in this
tree uh remember searching through a list takes time Theta of n proportional
to the number of elements um so let's say I'm looking for
the number 70 so I look at
47 I say 47 is smaller than 70 therefore I don't have to look at any
of these because they're all smaller than the number I'm looking for so now let me
look at 92 that's bigger than 70 so I don't have to look at any of
these so now I look at 81 that's bigger than 70 so I don't have
to look at this I look here that's less than 70 and
so I look at its right child but there isn't any and therefore I know that 70 is not
in this tree and to find out I only had to look at four nodes okay so searching in this tree
turns out to be Theta of log n we use um
LG as an abbreviation for log to the base 2 um so that's where we're
using um a hierarchical data structure not to represent a hierarchy but to
represent an order ing in an efficient way okay and then finally um over
here we have what's called a parse
tree um this one represents the expression
that you usually see written as 3 + 4 *
5 um
that's what's called an inorder traversal of the tree we'll get back to this later I started on the left then
the node in the middle and then the stuff on the right and for that recursively this left middle right um it
can also be done in prefix form where I start with the operator and then put the
oper ends and then we get + three times 45 a notation you've seen
before in this course um and there's also postfix in which I say
three enter so we're going to do the operands
first so here I'm done with three now I do all this thing operands first four
enter five times plus um and that notation is called
reverse polish notation it's used by HP calculators uh so all of these ways of
traversing the tree are useful any compiler or interpreter for programming
language builds a structure very like this from the Expressions that you type
no matter what the surface form of the language is it ends up with a tree like this in order to do the compilation or
the interpretation okay so that's three different uses for trees
um we represent these trees in different ways for example the world's tree each
node can have a huge number of children right so USA
has uh 50 states District of Colombia Puerto Rico and a few other little um
subjugated Islands still um so 55 or so
nodes and each of those has a bazillion nodes um
in the binary tree uh we say again there's only two nodes and so instead of
having a selector called children we have a selector called Left child and a selector called right
child okay um
sorry okay so um that's what a tree is that's the
general idea of tree I haven't shown you any actual code yet I'll get to that in a minute uh what I
want to do first is talk about the idea of a
node and a node is basically a piece of a tree so um this node represents the
United States the node is not just D the datam
USA sorry it's the chalk dust um the USA node is this whole
thing it's the datum the value USA plus all the children and grandchildren and
Grand grandchildren and so on of this node
okay so what's the difference between a node and it
tree come on no hands at
all a tree is a bunch of nodes connected well but this node is a bunch of notes connected
too somebody
yeah okay he's saying a node is part of a tree and um a tree doesn't have a
parent that's not part of anything else um well that could be except what I
didn't tell you if only I could find my talk is that
there's this tree called called solar system and it also has nodes Venus and
Mars and so on um so has this just stopped being a
tree okay so it's a trick question the answer is there is no difference a tree is just a
node that we happen to be thinking of as the thing that we're looking at right now the the important collection
um I'm emphasizing this because um data
structures textbooks almost always get this wrong they think that there's a
difference between trees and nodes and as a result of that they build way too
complicated abstract data types and as a result of that their programs are
humongous and people get the idea that trees are a very difficult thing to work with but if you understand as you guys
do that a tree and a node are synonyms then you will be inoculated
against the fear of trees that they're probably going to try to instill in you next semester um so
okay all right um so why are these things called trees
um well it's because they look just like a tree in real life in real life a tree has
roots in the ground and then it has branches that grow out of the
roots and finally it has leaves right so a tree looks just like
this um that's why it's called a tree I once got to give this talk in
Australia it was so much fun CU um cu the trees do look like that down
there um so
um as I said there's no built-in data type called tree and scheme and that's
because you want different kinds of trees for different purposes um we're
going to be looking for most of today and Wednesday at at a particular kind of
tree uh that has the property that a node can have any number of children um and there has to be at least
one node so in in this world that we're dealing with there's never any such
thing as an empty tree um but other trees are different
from that when we talk about binary trees for example it's going to turn out easier uh to say that there are empty
trees um in both cases we choose uh what's
going to make the programs easier to write so you'll see after you've written some tree code
why no empty tree for a multi-child thing and yes empty tree for binary uh
are the right choices
um okay oh up there is uh an abstraction
diagram where the thing above the line that we're trying to create is this notion of a twodimensional
hierarchy um and we're going to implement it is with a Constructor make
tree sometimes you'll hear me say make node they mean the same thing because trees and nodes um and selectors datam
and children and it turns out datam is just car and children is just cter in the implement a that we're using um but
as with any abstract data type once we've created this abstraction you're
not supposed to think about it that way so up here we have the Constructor and the two
selectors for trees and here's our first above the abstraction barrier tree
program it takes a tree node and says is this a leaf and a leaf note is one that doesn't
have any children children is a list it's a plain old linear sequential list whose
elements are nodes so a node doesn't have any
children if its list of children is empty that's what this procedure says
any questions about that so Leaf question mark doesn't know
anything about the implementation of trees the sort of below the abstraction
barrier representation of trees it uses children which is the abstract selector
for the list of children of a tree um to
find out now that list of children by the way is not a
tree it's a list a plain old sequential list linked together by cters you know
and cars for the elements like last week in which the elements are nodes or trees
in other words so it's a list of trees there's a name for a list of
trees it's called a forest for obvious reasons
um and there isn't any abstract data type for Forest because a forest is just a
plain old sequential list so like all plain old sequential lists we can use use car and
cter to find elements and sublists respectively um is there a
question thought I heard somebody but I don't see a hand okay okay
um
okay so here's
T1 one two three
four five six seven
eight so this is the list uh the tree
T1 if I actually print it out in scheme it looks like
that um but you're not supposed to worry about what it looks like what you're
supposed to worry about is probably the most beautiful
piece of code you're ever going to see in your life which is tree map and to show you what it does
do I'm going to say tree map Square
T1 and it gives me uh another
tree like this where each datam
is um the square of the corresponding datam in T1 so it's a tree with the same
shape as T1 and I've have applied a function to every datum in the tree not
to every node because a node is the datam plus the children but to every datam the things at the nodes um in the
picture and um I get back something that's the same shape as the input no
matter what how complicated the input tree may be um applying a certain
function to each datam in order to get the result and we do that with four
lines of scheme and I hope you realize how
impressive this is because of the fact that this is a complicated data structure you have to kind of wind your
way through it and look at all the children and don't forget the datm of the node you're at and so on um and this
little program does all all that how does it do it
well what data type first of all should the result of calling tree map on a
function in a tree be what do you get back a tree how do we make trees we use
the Constructor make tree now make tree takes two
arguments the first one is a datam so what datam should we put at
this node we're constructing and for that we just apply
fin the argument function to datam of
tree okay everybody clear how that makes sense we're given a datam in children we
call Square in this example on each datam so now we have to say what should
the children be well
the result
of the result of calling tree map on let's say this node right
here is this node right here
okay and in general in the result we're going to have one child in the result
for each child we have in the original right and what is it that we do to those
children well we tree map them because each node is a tree
right so what we want to say basically is map tree map children of
tree we can't quite say that because tree map is a two argument
function so I have to say instead map oops hello
oh Lambda of child tree map F child over children of tra and that's
it wow was that
easy where's the base case say it
louder in the map yes buried inside of map is if this is an empty list then
just return the empty list do you have a question that was your question okay
um so what's going on here if you think
about it hard is actually pretty complicated
um when is Children of tree I'm sorry when is the argument to map going to be
empty well two cases one is Children of tree is
empty what kind of a node are we at if children of tree is
empty your choices are root branch and leaf leaf we're at a leaf node so that's
a kind of vertical base case we've gone as far down as we can go when else is map going to be called
with an empty list besides being at a leaf
node uhuh all right let's say we're doing tree map of this note here the one
that starts with five and direct your attention to the children of five even
for a leaf node this is not just a six it's a node whose datam is six and whose
children is the empty list okay but what we have is
is a list of three nodes so map is given this list of three
nodes and it cers its way down the list until finally it runs
out okay so one base case is the sort of vertical end of things when we're at a
leaf node and the other is a kind of horizontal end of things when we've run out of
siblings right um neither of which is explicit in
this code because map just takes care of it and we we're
leveraging the abstraction of a linear sequential list to help us build the
abstraction of a two-dimensional hierarchical tree okay
you are not going to totally get this piece of code sitting here in the room today you're going to go home and take
it home and stare at it for hours and play with it and poke around inside it
and Trace the calls to map uh until you finally get it but you will see that
this these four lines here are like the most beautiful thing in the universe um just an amazing thing that
we can do that and it's not by the way that I got to write this beautiful thing
because I'm brilliant it's it falls out of the nature of abstract data types
yeah so what would oh the running time
um basically you have to look at each node at at each datam right um so it's
linear in the size of the tree um unlike the cas with the binary
search tree where we could avoid looking at some of the data and so uh it's only proportional to
the depth of the tree rather than to the total number of items but here we have to look at every
item um okay so a two-dimensional data
structure gives rise to a kind of two-dimensional control structure as you're tracing out what's going on here
um you're G to start with a node and you're going to look it through its children and go left
to right in the children but within each child you're going to go top to bottom um so what's the order in which
the computer actually figures out squares of numbers well it depends on the order in
which STK chooses to evaluate arguments um the scheme standard does
not say the leftmost argument has to be evaluated first that's left up to the
implementation some go right to left I don't know of any that do something other than left to right or
right to left but it's imaginable that they might do the easy ones first or something
um so we don't really know but let's say it goes left to right in that case first
we square one then we Square two then we Square three then we Square Four then we
Square five then we Square six then we Square seven then we Square eight so that's the order in which things
actually happen so it's one one two three hit a base case back up to two
down to four hit a base case back up to two hit a base case for running out of
children back up to one down to five right that's how it
goes um and all of that incredibly complicated up and down left and right
structure is in this call to map that
calls tree map map but it's not tree map calling tree
map it's map calling tree map right so I mentioned last time the
idea of mutual recursion what we have here is a mutual recursion where tree map calls map and
map calls tree map more than once map calls tree map as many times as this
node has children okay whichever node we're looking at um so that's what gives rise to the
two-dimensional control structor is the the mutual recursion and
yeah can we do it without Mutual recursion
um yes but you're not going to like it the answer
um anything it turns out can be done iteratively just you know with one tail
call but the cost of doing that is that you have to build explicitly yourself a
data structure full of Unfinished tasks so in essence you have to write a
little scheme interpreter of on your own that remembers what parts of this
problem it hasn't solved yet and goes through them systematically um so you
really are doing the equivalent of a mutual recursion but you're doing it in
a more complicated way uh but it is is tell you know it's iterative so that
that used to be as I said it used to be really really important in the days when computer memory was expensive and
small um people were happy to find iterative equivalents to recursive
programs today if you're dealing with a two-dimensional data structure please
don't try to do it itera okay Mutual recursion is your friend enjoy it it lets you write tiny
little programs like treat other questions
yeah say it
again yeah if you're doing something in two Dimensions you should naturally think about Mutual cursion yes
um and in particular you should think about this trick of using map to handle
one of the dimensions for you okay
um the the vertical moves are sort of handled by this call to Children right
here which is outside of the map but Matt inside of map is where we deal with horizontal motion across
siblings um okay
great speaking of mutual recursion
here's tree map done without using map
to make the pattern of behavior even clearer so instead what I did is I
invented a helper function called Forest map that looks a lot like map uh but
it's specific to tree map so Forest map
function and the second argument is a forest which is to say a list of trees a
different thing from a tree so when we're dealing with a tree we say datam and children to get
the pieces of it when we're dealing with a forest we don't say datam and children
it doesn't have a datam and children it has elements that are trees and so we
call car and cter car gets one tree cter gets a slightly smaller
Forest okay um so it says if the forest is empty return
the empty list so here's the base case both vertically and horizontally um otherwise
cons what should the car be well it should be a tree and we get one by calling tree map
on on car Forest which is the first element of the forest which is a tree
because each element of a forest is a tree and then what should the cter in
the Scala cons be well it should be a forest which we get by doing Forest map
of cter of forest okay so the pattern of the
recursion
tree map calls Forest
map which calls itself recursively and also calls tree
map okay so that's the sort of dependency picture for these two
procedures and that circularity tree map calls Forest map Forest map calls tree map that's what makes a mutual
recursion
yeah what does a forest look like forests don't have branches because they're not
trees a forest is just a plain old linear list like we learned about last
week so it looks like
this right and each of these cars points
to a tree what does a tree look like like
none of your business it's an abstract data type okay you're not supposed to think about it you're supposed to think
about this is a tree this thing is a list of trees and that's that
okay um all
right okay oh I forgot to make an administrative announcement so let me
back up up and do that the administrative announcement is um the instructions for project two are in
volume one of the reader under the week five homework page um so the actual project the
problems that you're doing are in the textbook but in in the week five homework page it tells you how to load
the file that you need and how to actually run it and see pictures on the screen also when you turn in the project
you don't have to turn in pictures um in fact you shouldn't print pictures
on the lab printers um if possible you should just turn in your code and a
transcript of the kind of debugging that you can do just looking at values on your screen okay uh so that's the
administrative announcement
um somebody asked me before class do we need blue books no no no Blue Book no
Scantron the only thing you should bring with you is your one page of
notes um and a good book to read
um somebody asked an office hours about abstract data types and I
said there are two sort of opposite mistakes you can make so let's talk about trees and forests one
mistake the most common one is to just ignore data
abstraction so up here where it says datam I would see
car and down here where it says children I would see cter so that would be violating the tree
abstraction but the other kind of data abstraction mistake would be to say
datam here because because this thing Forest is not a
tree so it doesn't make any sense to ask for its data mered children
yeah the abstraction of data in children no it's um it's not I defined those
procedures right at the beginning of class there were the first three lines of code were Define make tree Define
datam define children to be Kar and cter respectively
here
yeah would it be yes if we call car on the tree like for example here that's a
data abstraction violation you should imagine once we've built make tree datam
and children you should imagine that you have no idea how trees are represented
they're a data type that came with scheme and the only kind of insides they have or a dam and children and they're
completely unrelated to car cter yeah why not I'm sorry why do we call
car for a forest because a forest isn't a tree a forest is a list of
trees so I wouldn't say car of car of forest because car of forest is a
tree okay but Forest itself is not a tree so it's okay to take its car and
it's cutter that make sense okay
yeah yes that's right you will not be asked to draw box and pointer diagrams for a tree I want you not to think about
it in those terms actually okay um all right moving right
along um another kind of two-dimensional data
structure lost my chalk again behind me thank
you and another kind of two-dimensional data structure is a deep
list my favorite
example
this is not a tree like those ones I drew on the board because it's not a
sort of infinite depth kind of thing it's a list of lists of words or in other words a list of
sentences okay and ordinarily I would write a program to
manipulate a list like this by using car and cutter for the elements of the outer
list and first and but first probably for the elements of the inner list because I'd say those are
sentences all right um but right now I want you to kind of squint a little look at it
sideways and say this is kind of like the following
tree
okay see the connection between this picture and this picture now this is a funny sort of tree
it isn't like the trees we've been dealing with because the branch nodes in this tree don't have
data so there's a very sharp distinction between a leaf node which has a datam
but no children and the other nodes which have children but no
datam okay um so it's not an example of the
abstract tree structure that I built a few minutes ago but it is a tree like
thing and we can use treel like code to manipulate it so if I wanted to do
something to every word of this thing and I wanted to figure out how to
do that I might one approach I might take would be to write something that looks a lot
like tree map except that it wouldn't talk about make tree or datam or children because
we're not using that abstract data type um instead it would
say this
and what this code says it's not as pretty as treemap but it's not too
bad as is an if for treemap we for every node we have to do
something to the datam and also do something to the children in this kind of deep
list a node has only a datam or has only
children depending on whether or not it's a list if it's a list it has only children so I
do this thing which calls deep map by way of map
just like tree map called tree map by way of map um but instead right here whoops
where it used to say children of tree here it oh LOL by the way does not
stand for laugh out loud it stands for list of lists
so you kind of want to be seeing children of LOL here but a branch node
is its children a branch node is just a list of its children so there's no
selector needed for finding the children of a branch note a branch note is a list
of children and at the other end of things if it's not a list then um it's a leaf
node and the leaf node is just its datam so instead of calling fun of datam of
LOL we just call fun of LOL all right so in tree map every call
involves both of these pieces in deep Map There's an if and we do only the
thing for the datam or the thing for the children not both and that applies to
the whole node all right so that's what you get by kind of squinting your eyes at a deep list of lists and it could be
a list of lists of lists and this mechanism would still work it could be an arbitrary depth list of lists of
lists okay so it's it's better than something that you would write just for lists of sentences list of sentences one
might be easier to read for this particular situation but this one this deep Map works on lists of sub list of
Sub sub list of Sub Sub sub lists to varying depths and varying places however you want just like trees can
have varying depths okay so just to make your life unbearably
complicated
okay the book confusingly uses the word tree to mean what I'm calling a deep
list I is the word tree as a broad generic term for any of these
two-dimensional data structures including the list of lists the capital T tree the binary tree any other 2D
structure that we come up with where each node has one node or except for the
root node okay so me this is a generic
term them they mean deep list so they have a thing called tree map that's like
my deep map okay just to confuse you when you see tree with a capital T
it means this thing with datam and children is selectors and make tree is the Constructor okay so that should be
true for example on an exam not this exam which doesn't cover this stuff but
midterm two if you see capital T tree I want you to know what that
means okay
um we doing on time one last question
yes does scheme deal with nodes that point to their own parents is that what you're asking
um yes we are going to talk about circular structures um but not for
another month or so uh because they're pretty hard to deal with satisfactorily but yes we are
going to okay see you Wednesday twice
