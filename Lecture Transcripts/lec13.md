Transcript


welcome um there's a midterm
today sorry hurts me more than it hurts
you um okay on the board up there is a
little chart about different things that are in the tree
family um and there divided
in two categories two ways each um so
there's a kind of tree in which every node has a a
specific left child and a specific right child and that's it and there's a kind of tree in which a
node can have any number of children so that's the category that's labeled across the top two children or
nild and then the vertical axis of this chart um you can build abstract data
types for this kind of tree or sometimes you're just using regular old pairs to
make regular old lists but you're using the ideas of this week about trees to
think about those lists so we've looked at uh the abstract data type capital T
tree the kind with data m children as selectors um the book spends a fair
amount of time on the binary tree abstraction um and we also talked about
deep lists about seeing a deep list remember as being a kind of um
degenerate Tree in which the branch nodes have only
children no data and the leaf nodes have only data no children and so we write
program instead of writing programs like tree map that say make tree something
about the data something about the children it's either or we say if this
is a leaf node and do something about the thing viewed as a as a
datam uh if this is a branch node which is to say it's a pair then uh do
something about this node viewed as a list of children
um so the last piece of that chart that we haven't talked about is car coder recursion
which I am going to get to I guess right now um so let's
take my favorite list of lists
okay in the interest of time I'm going to abbreviate
okay so this is a list of four elements each of the four elements is a
list of two elements and those things are words okay everybody with
me so you got it that this is a list of length four right and that each element
of that list is a list now what I'm going to do is I'm going to grab this by its
start Arrow I'm going to pick it up off the board word and shake it okay and the result will look like
this wait no that's not going to work I'm going to run out of room
okay so you see what I mean about picking it up and shaking it and just sort of let gravity pull down um this
stuff because this if I pick it up over here it's really right heavy so Its Right End is going to swing down right
um okay speaking abstractly what does this remind you of
a binary tree right every node has a left every Branch node which is to say
every pair has a left child and a right child this thing is more like a capital
T tree so deep lists and this is how we viewed it on Monday as a list of lists
if you think list of lists it's like the capital T Tree in that a node can have
any number of children this node right here has four children right and this one has two
children and so on um
here it's more like a binary tree there's a specific left child and a
specific right child for every node even though these are exactly the same
structure right I drew the diagram differently but if you follow the arrows
you will find that that there's the same number of pairs and they're hooked up in the same way between these two diagrams
so what used to be the spine of the list
is these four pairs right
okay um so I put up on the screen um the most
beautiful piece of code you're ever going to see is that you could worship it on your way in um but now I'm going
to uh find do I
have any of this relevant no
sorry just a
sec yeah that's the one I want but
um okay never mind let's just put it up
here okay so up on the top of the screen we have um
deep map Rewritten so we wrote a deep map last time that said um I can just type it in
actually it says define deep map list of
lists it said something like if pair
list of lists
then um
map oh
whoops what I
meant child deep map function
LOL uh child child
LOL otherwise
LOL okay so this is um deep map for trees viewed as deep
lists so we say if what we're looking at as a pair then we're going to take it as
part of a list and we're going to map deep map
essentially over that list the very list we have because it's its own
children if it's not a pair then it's its own datam and we call fun on
it okay so that on the bottom that's the Deep list way of looking at structures
made of pairs up at the top though we have a
different ver version of Deep map um
wait oh no that's what I just wrote uh I'm an idiot
sorry thanks right here's the other
version um the formal parameter is uh xus because that picture all the way on
the right looks like a Christmas tree to me um so I'm reminding myself what shape it is and there are three cases now to
worry about if it's an empty list then I just return the empty
list if it's a pair and here's the tricky part then I say okay what is a pair it's
got a car and a cutter it's basically that's what a pair is it's a car hooked up to a cutter and
um so I can make the ma version of this pair by calling deep map on the car and
deep map on the cutter and consing those two things together and I really don't
care what kind of thing the car is and what kind of thing the cter is that's the job of the recursive call to worry
about that I'm just going to take on faith that no matter what my car is and no
matter what my cter is deep map will work on them because that's the way recursion works you assume that it'll
work for anything smaller than the given problem so I have these two sub problems
one for the car one for the cter I call Deep map for each of those and I cons those two results together to get my
result okay um so that's called car cutter
recursion it has the disadvantage compared to the top version that it
doesn't really respect the list structure okay the top version really
understands that a list is a string of pairs with elements in the
cars um whereas the bottom version doesn't know anything about
lists particularly um because the bottom version unlike the
top version doesn't call map see in the top version if we're looking at a
list then we use map which is the plain old function for plain old sequences
from last week to go through the spine of the list and apply the function to
each car along the way in the car cter
version there's no call to map there's just these two recursive calls to deep
map um one for the car one for the cutter and that's like what we would do
for a binary tree for a binary tree we would say something like um make binary
tree fun of datam of this node deep map of left child of the node
and deep map of right child of the node right we would call Deep map recursively exactly twice once for the left child
once for the right child and that's what this does except instead of making those things
arguments to an abstract Constructor make binary tree we just cons those two
results together to make a new pair okay
yeah okay his question is if K car and cter are used as uh Constructor and
selector for lists why doesn't the second one have the idea of listing it so one answer to your question is
imagine a structure hooked together out of pairs that isn't a list or has pieces of
it that aren't list which is to say there are pairs whose cutter is
something other than uh the empty list or a pair right so you have like two do3
that kind of there in your structure this second version the car cutter
version will happily work on that we can say deep map Square cons 2 three and
we'll get the result 4.9 okay so this thing doesn't care
anything about how you hook the pairs up so I just said a moment ago that that's its weakness but it's also its strength
so it's a little bit more General whereas the first version because of calls map and Map works on the
assumption that all the actual information is in the cars of the spine
so that's making an assumption that only works for lists of lists you know however deep you want but they all have
to be lists for it to work um so they're both
valid you know uh they're both really good techniques neither one of them
respects abstract data types so I think I said last time that
in that particular example about Donn Paul George and Ringo um what I have
that really is a list of sentences and I would probably if I'm just manipulating things that are that shape I would write
my code that way to know that they're exactly too deep and the first thing is a list and the second level is sentences
um these techniques are good for sort of heterogeneous data structures that
they're different depths at different places so you want to use something like tree recursion um but they're the
abstract data types that they represent are something other than a tree you wouldn't use either deep list recursion
or car cutter recursion on a capital T tree or on a binary tree you would use
the correct selectors and Constructors for that abstract data type this is for
the correct selectors and Constructors are something about a database right we have a database over it sprow
about students and it has a record that consists of your name and your student
ID and your less known address and uh your transcript which is itself a list
of courses and grades and and your courses you're taking this semester which is another list and how much you
owe the the cashier and stuff like that right and so it goes different depths at different places in that structure and
now I want to go through and and um make everything capital letters because some
software the comparisons fail of some upper case and some lower case letters so I'm going to totally ignore the
abstract structure of this list and I'm just going to treat it as a kind of degenerate tree and I would make a
choice whether I want to treat it as a degenerate in children tree or a
degenerate binary tree and they both work okay really the key things about these
techniques is that they involve tree recursion and in the case of the one we
did last time the tree recursion is hidden in this call to map because map's
job is to call this function which involves a call it to
deep map once for each child of a branch node so this call to
map turns into several veral calls to deep maap okay in this
case oops what you mean thank you in this
case at each time through this function we make exactly two recursive calls one
for the left one for the right but that's enough for it to be Tre recursive for it to have the full generality of
infinite depth of data structures okay so when you see two recursive calls
like this you know that you're dealing with a tree recursion is that a hand up
yeah right I'm sorry say
again the order of growth of all of these things is uh proportional to the
number of nodes okay because you have to visit every node now what counts as a
node is slightly different you know whether you think of a pair as a node or you think of a whole list as a node but
it's going to turn out not to matter basically all these things have the same order of growth um trees get you a
better order of growth when you don't have to look at every element so last time I showed you a binary search tree
and the whole point of the binary search tree was that in each comparison you get rid of half the remaining data right and
so that gave me a running time of proportional to the depth of the tree rather than proportional to the total
count of the tree so typically log n rather than in but if we're traversing every node
then you know it doesn't matter how it's array you still have to get to every now okay
um okay so I've just finished telling you that if you see two recursive calls
you're looking at a tree recursion and there's either explicitly or implicitly
a data structure that looks like those involved somehow now I'm going to show
you um not to get too hung up on form rather than
meaning because this is a procedure you've seen before this is filter this
is like the list version of keep right and it
has two recursive calls one here one
here is this a tree recursion take a vote I want to see
every hand who says yes who says
no good all right yeah no is correct somebody has said no why not
yeah because only one of these two recursive calls is going to happen any
particular time through this so either the predicate returns true in which case
we only do this recursive call or the predicate returns false in which case we
only do this recursive call there's no situation where we do both of them as opposed to down
here where we always do both of them okay okay so don't think oh if I see two
recursive calls that makes it a tree recursion no matter what what makes it a tree recursion is the two recursive
calls are actually performed right so almost the very first
program you saw in this course was a tree recursion namely count
change right can you remember back that far makes two recursive calls one for
supposing we do use a quarter and one for supposing we don't use a quarter or a dime or a nickel or
Penny right and we add up the results of those two recursive calls so that's tree
recursive now is there a tree involved is there a data structure in the
computer that's tree like no not in count change in count change the tree is
implicit
it's like I have
$137 and my biggest coin is quarters okay and then this it's a
binary tree either we have
a137 in the biggest coin is dimes or we have a dollar can I do this subtraction
in my head 12 using quarters okay and so on down all right
that data structure doesn't exist as a data structure in memory but it's in the
programmer's head it's implicit in the program that
there's a control structure that has that shape for this problem okay so it's
tree recursion whether there's a concrete tree involved or not
um so tree recursion is a very important thing to understand it's it's pretty
hard um some people had trouble with it back in the first week some of those
people have since dropped the course um but probably some of the people who
had trouble with that are still here and if so now is your chance to
really learn it and understand it so don't let yourself get past this week
not understanding tree recursion if it's a problem for you get help from me from your TA from hkn from
somebody all right um tree
traversal okay so the topic is
um I have a tree and I'd like to visit every [Music]
node and let's see where is
this say my notes search is there a search yes there
is
yay okay so let's say we have a tree
it's a capital T tree it's an abstract
tree and we have um I don't know
losing my mind
um oh Roger that's
right day and he and Nick okay whatever
it's a tree my job is to go through this
tree printing out the datom of every node one per
line okay well there are two basic ways I can
do that they're called depth first and breadth first depth first
says okay I've printed out the word music now what I'm going to do is look
at the first child so far we could be in either bread
or depth first and when looking at the first child it's a tree and I'm going to
look at the whole thing so the datam at this child I'm going to print beetles then I'm going to print John and Paul and George and Ringo and then when I'm
complet and if some of these had grandchildren I would print them too
then when I'm totally finished with this tree then I move on to the next sibling
so it goes down before it goes sideways that's why it's called depth first treat
reversal okay the program to do it is very simple it's the first three lines
at the top of the screen so to depth first search a tree
and here all I'm going to do is print out the datom of each node so I start by saying print the datm of this node
music and now I'm going to say for each of the children depth first search them
so I'm going to depth first Search Beatles which is are going to print Beatles i'mna John Paul George Ringo
then I'm going to dep first search who and I'm going to friend who Pete
John Keith forgot again Roger thank
you I am so getting old and then after I finish that tree
complet completely I'm going to go on to Kinks and I'm going to do ray Dave Pete Mick okay that's it that's very simple
and the reason it's so simple is that my processing of the
tree is following the actual links because there aren't any links
from sibling to sibling in a tree the linkage is all
child to parent parent to child so in order to get from Beatles to
who I have to sort of think sideways right whereas in depth first
search remember each child here's the real Point each child of a tree is a
tree so if I do a recursive call for the child it's going to do that whole
tree so for each calls depth first search for each of the
children and that's the pattern that I get red first search is a little more
complicated to do bread first search I have to invent a data structure
that's going to remind me where I'm up to so the goal of of bread first search
is I want to print music Beatles who Kinks John Paul George Ringo Pete John
Etc okay okay so go all along one level and then go down to the next level so to
do that I am going to
have a
Q you there was an XK cedd last week about
words with a lot of vowels that's one of them um
so for the purpose of this exercise something with a triangle drawn around it means the tree that has this as its
root denam so to start with my starting conditions are going to be
um that my Q is
empty okay and I'm going to call bread first search iter it's an iterative algorithm
oops here it is and oh I'm sorry my tree my Q is not
empty because I call bread for search itter with list tree A Q is just a
list I'm going to stick things in at the back and pull them out at the front so my initial
CU is the music tree
okay that's my Q to start with now what do I do I say is the Q
null no it isn't so now let task be car of Q so task over here is going to be
the Tre music now what does it mean to deal with
this task well so I'm I'm down here
oops it's got to be oh I see pushing the wrong button there we go so I'm going to print the word
music and now I'm going to make a recursive call with a new
Q in which I append cter of Q which is
what what's the cter of this the list it's not a tree at all
it's a list this the queue is a forest it's a list of trees so if I take cter of this queue it's empty I'm going to
append to the empty list children of task task is a tree so it has a children
what are the children there's the Beatles
tree there's the who tree and there's The Kinks
tree okay so that's my CU now I'm going to
say I'm making the recursive call to BFS it um is this Q empty
no so let task be car of Q so task is
now the Beatles
tree and what do I do for this task well I print datam of the task which is
Beatles so I printed music I print Beatles and now I
append cter of Q which is now more interesting it's not empty right it
has who and HS in it and to that I append
children of task which is the John tree
the Paul tree the George tree and the Ringo tree
okay so that's my new Q now I take car of
Q that's who that's the task the new Q
is Kinks John Wall
George Ringo um
Pete John
Heath Roger I got it this time
okay so do you see how this generates a depth first search I'm going to handle
all the siblings of be before I handle any children because all
I do with the children is stick them at the end of the queue end means I'm going to get to them
last right because I'm taking things off the front of the queue Q by the way if you don't know the word is British for
line as in standing on line at the bank that's what a q is so things come in at
the back and they come out at the front um otherwise known as last in no
yeah last in last out first in first out yeah first in first out that's a
cute okay so this procedure it's only a
little bit longer it's six lines instead of uh well eight lines instead of three
lines but it's a lot more complicated because I need this auxiliary structure called a q I have to understand how that
works um notice that by the way as an exercise
in data abstraction we use car and cter for the Q but we use datam and children
for the task because each task is a tree whereas the Q is not a tree it's a
forest okay so don't make either mistake of data abstraction too many atams or
too many cars um okay why would I want to do things in
either of these ways well depth first search mostly to be
honest you do depth first search when you really don't care what order it's in and depth res search is just easier
because you're going with the flow of how the language represents things and
using higher order functions like map to help solve your problem so it's just easier but also you want to do it depth
first because you want to group things that are related so if we're printing out this tree it's
actually much more sensible to say Beatles John Paul George
Ringo who Pete John Keith Roger Kinks Ray Dave Etc
okay to put the group name and then the people in the group rather than the three group names and then all the
people in a row it's more informative to print it out depth
first okay why would we ever want to use bread first
um the answer broadly speaking is about searching of some space of possibilities
and the canonical example is I'm writing a program to play chess so I hope you all
know that 30 years ago chess was the canonical example of
something that a computer will never be any good at and today the world's champion chess
player is a computer um not so much because we got smarter
but because computers got faster and more powerful um so how do those computer chess programs
work well the way they would work ideally is
they would construct a complete tree of possible board positions
right so the beginning board position would be all the white pieces in these two rows and all the black pieces in those two rows um and then you'd take
every possible move for white and that would make a child node
and then each possible move for Black based on that move for white would be the children of that and so on and you'd
go all the way down until you reach leaves and a leaf node would be somebody wins the
game or you get in a cycle and it ties and then you would work your way back up
the tree trying to figure out how we can force a series of moves that leads to me
winning sadly the number of possible board positions in chess is I think this is
true greater than the number of atoms in the universe so uh we aren't ever going to
construct that tree in its entire day um and instead what happens is you
build that tree bread first to get as deep as you can before
you run out of time because you only get certain number of minutes per move in chest that's why they have those clocks
like in the movies b b um so you take almost all your time and you spend it
building this tree red first because you want to you don't want to chase down a a
dead end and not get to some other possibility so you have to look at all the possibilities at once and then when
you're almost out of time you stop building the tree down and you start evaluating board positions right now the
board positions that you're looking at nobody's won or lost the game yet you're
like eight moves ahead of yourself or something um and so what you have to do
is evaluate those board positions basically the way human chess players do right you say um what's my Pawn strength
and how many points of captured pieces do I have and all those questions that chess players ask it's in the books um
and so you come up with some figure of Merit for each board position and then you work your way up trying to force the
best possible board position that you can force your opponent to give you um
so making that tree is an example of why you would want to do something breed first because if you do a depth first
you're going to run out of time before you have an answer okay um
another reason is it's not that you would run out of time but you're looking for the minimal
possible path to a leaf okay so my favorite example of that
is everybody take the kind of IQ test where they say uh you have a three qu
pitcher and a five qut pitcher and you're down by the river and you're trying to measure four quarts you know
and the pictures aren't marked how do you do it and you can four for one to another all that those are piter pouring
problems and their trees are you know quite simple basically um so you could
Traverse the entire tree in in no time if you're a computer but the answer you
want to come up with is the one with the fewest possible pourings from one thing to another and the way to get the fewest
possible steps to a a leaf node is to do it bread first so can I find a leaf node
one level down from my starting point if so finished if not construct the grand
my grandchildren can I find a leaf Noe in there no construct my great-grandchildren and so on so that's
another reason for doing bread first search okay you are going to get all of
this in glory detail writing the code to do it and everything in 61b but I'd like
you to kind of have the ideas um at this point uh
okay for binary trees um within the general category of
depth first there are subcategories so I'm going to
construct the best example that I know for why these ideas are important about
reversal which was the parse tree that was like this that I showed you
before okay so now to parse this step
first for each node there are basically three steps there's print the node
this's do the left child and this's do the right child right those are the three
steps well we can do those three steps in basically any
order people always do it left to right people being people who speak English
which is a left to right language always do it left to right I have no idea maybe if you're a Chinese computer scientist who do it right a left anybody
know anybody follow Chinese computer science anyway it doesn't matter for our
purposes we're going to go always left before right and that reduces the number of interesting possibilities three and
the three possibilities are in
order is left
bom right and that gives you 3
+ 4 * 5 right first I print the three
then I print the plus then I do an in order traversal here which means first the four then the times then the five so
that's in order next we have pre-order also very
interesting where we say datam then
left then right that gives us
plus three times 4
five which two months ago you might not have thought very interesting but now you can see is sort of the center of the
universe and then finally we have post
order where we say left
right datam I think I show do this actually um
which gives us the peculiar result um
three four five times
plus um for human purposes that looks pretty
bizarre unless you have an HP calculator in which case you're accustomed to it and you understand the merits but if
you're a computer and you're running um a postcript you're running a
postcript file to be printed or JavaScript do I have that right no
JavaScript is three some language or other it's
postfix this is what you do you get the data ready first and then we say what
operator do I want to do so this work order although it looks funny is the
order in which a computer actually carries out the computation so we say three put that on a stack a stack is the
opposite of the Q it's last in first out so I take my
three put it on the stack take four put it on the stack take five put it on the stack oh look an operator let me pop two
things off the stack and use them as the arguments to times and that gives me of course 20
which I push on the stack and then oh look an operator let me take three and 20 and give them to
plus um so that's a really useful way to have things represented from the point
of view of a computer so those are the three sub possibilities within depth
first for binary trees
um as usual I'm not going to get to show you pathf finding in my lecture notes there's a nice example
taking the world tree asking the question um where's Berkeley the answer to which is World
USA California Berkeley that list so that's a slightly tricky piece of code
it's just as well that I can't lecture about it because you wouldn't understand it from me doing it quickly but you
should read it in my notes um next time on Friday um you're going to see your first
scheme interpreter written in scheme and then Monday's a holiday which
means everything you're doing for project and homework is due Tuesday okay I think some piece of the
reader has that wrong okay see you tonight not here 2050 vlsb
