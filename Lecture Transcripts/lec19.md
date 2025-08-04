Transcript


okay good afternoon um this is where we're up to I think and talking about
our little objectoriented language um right at the end of last time I
introduced the idea of um inheritance which is controlled by the
parent class um the parent Clause sorry and
what goes on the parent Clause is is um the arguments you would give to
instantiate to make an instance of the parent so in this case I want the parent
to be a person and if we back up and see what a
person looks like uh person has name as an instantiation variable so I made pigger
also have name as an instantiation variable this is sort of the formal
parameter part for pigger um and this is actually a reference to that variable so
this isn't uh it's only by coincidence that the word name is a
variable in piger and a variable in person I it's not a complete coincidence obviously because I'm using them for the
same purpose but what I'm trying to say is that what you put in here is not
necessarily even though it is this time exactly what you you see up here it'll
be person and then some expression whose value is a word that'll be the name of
the person okay so this is how parent Works um you can have more than one of these
in a parent Clause now I'm not going to show you that in lecture um because it
doing it setting it up is easy but figuring out what it means is hideously
complicated um Small Talk which started object-oriented programming does have
multiple inheritance but pretty much every uh objectoriented language since
then has given it up as a bad idea um and the reason well I'll show you the
reason after we see how inheritance actually works but basically in certain situations it's hard to know which
parent you meant to use for a particular purpose um Okay so
the question really is how does it happen that even though pigger doesn't
have an Ask method I can ask PP to I can
send it the message ask um and it finds the method in the
person class which says oh let's go look at that again sorry um here's the ask
method it says ask self say would you please and the
argument that's what it says to do and that's what happened down here we said
play um which is just what persons do when they're asked when they're asked to
ask something we put would you please in front of it but the interesting thing is even though we found the method in the
person class this say message is still
handled by this same method the one in the pigger class and that's why it comes
out in pig latin so how does that happen well it happens like
this here's PP uh it's an instance of the pigger class
um it has a name which is
forky it has methods
piggle and say but it also has something
else it has um sort of a hidden instance
variable my
person and the value of that variable
is a person now persons have
um name which is also
Porky uh and they have methods say
ask and greed no arguments okay so this is what
a person looks like this is what a pigger looks like and because I said parent
person uh our language created an actual person object an instance of the person
class which is sort of buried inside this
piger so I'm send the message um ask not play games in
class to this object so this object says do I have a method called ask no I don't
ah but I have a parent and it just sends the message to
the parent okay
but remember I said um there's this special variable self that methods can
use uh like ask self such and such well self is not actually an instance
variable here well no I'm sorry yes it
is let's put it in
self for this pigger self points to myself
okay if I just said instantiate person it would have a self that points
to itself too but I didn't I used person as the parent of another object so
itself points to the original pigger so when this ask method says ask
self to do something it looks up self and it doesn't find this object it finds
this object so when it asks itself to say would you please not play games in class
we're using this same method which overrides this one because this is the object we're talking to okay let me stop
for questions yeah
right if so you mean the self the self of person yeah um if you said instantiate
person then itself would point to itself but inside the object language we have a
special only for the object language not for users version
of instantiate that takes another object as
argument and makes that the self of the new thing so what it's doing when you say parent person it's not doing an
ordinary instantiate it's doing a special kind of instantiate that has a different gives it a different
self okay the way you're supposed to think about it as a user remember we're we're looking both above and below the
abstraction barrier for objectoriented programming so I'd like you to understand how object programming can be
implemented and also like you understand how to use it from the user's perspective that person object doesn't
exist from the user's perspective piggers just have both kinds of
behavior and pigger just you know if there's something in the defined class
for pigger we use that if not we use the thing in person okay
um but from an implementation standpoint we we have chosen to to implement
inheritance using a method called delegation you know what delegation means in real life it's like um I say
you know write me a 20page paper about delegation and you turn to him and say hey write me a 20page paper about
delegation that's what delegation is you get somebody else to do it um and that's
what we're doing here we are delegating the ask message to this invisible person
object that's not the only way to do it a lot of object languages don't do it this way what they do instead is a kind
of um it's as if they stick when you say
parent it sticks the defined class for the person object in front of the
defined class for uh that you actually wrote for pigger so you don't actually
have a person object you have one instance you only have an instance of pigger but it has built into it both
kinds of behavior that's the other way of doing inheritance um it works fine um
it takes more effort than doing it the way we're doing it here and this way actually is you know good enough so um
in fact technically delegation uh is more powerful if you read the papers
than um the other kind of you know sort of inserting the thing in thing okay
yes ah good question so the question is how would you get PP to say would you
please um not play games in class without turning it into Pig ltin you
wouldn't um when you defin the class you defined it so that Its Behavior the
whole point of a piger is that it talks in Pig ltin it talks in pig latin no matter how it's asked to say
something um if you wanted it only to speak pig Latin
sometimes then you would give it two same methods or something and or a same method that takes an extra argument you
know for how to do it but that would be complicated because the person thing
just calls say so you'd have to have for example you could have an instance variable that
you set to true true if you wanted to speak Pig Latin and false if you don't and the same method in here could test
the value of that variable so you know if you really wanted to do it you could but the big
point that I'd like you to get is that the whole reason you used a pigger is for it to speak pig Latin
okay yeah I'm sorry say it
again yeah um it comes from the fact fact that
you used a parent Clause what the parent Clause does is
instantiate the parent class makes an instance and it gives you a a variable I
don't know if it's actually called this or not but you have a hidden instance variable um and the what it's used
for um if you think about the way message passing works from last week
it's Lambda of message cond is it this message do this is this message do this this measure do this else
error okay so what we're going to say is if it's piggle do this if it's say do
this if it's name because you get free methods for all your variables then return name else send the message to my
person okay that's how it works other questions
yes isn't the self an endless loop um
no well yes it's a circular data
structure but where that arrow is pointing is not to the instance variable
self but to the instance that big box okay this is why remember when we
introduced box and pointer diagrams one of the things I said was be careful about where the arrowe head is this is
why it's not pointing itself yeah
okay question is if pigger didn't have an instantiation variable what would we
do about in the parent Clause the fact that person does take an instance variable well if you didn't have an
instantiation variable for name it would mean that you want all your piges to
have the same name you might want that in which case
up here instead of person name you would say person quote
Porky you have to put something you're the class designer you
decide okay all right moving
on so this is a very cool thing I want you to really understand how slick it is
that piggers don't have an Ask method persons don't know anything about
piggers or Pig Latin or anything when we wrote the person class we wrote it to stand on its own not as part of the
implementation of piggers because in our world we're going to have real people as well as pigs right
um like babe we should have called it babe um but because babe talks you know
uh And yet when we get to this ask method
from a pigger it speaks Pig Latin it's really really a cool thing it's what
inheritance is what makes object-oriented programming practical we could do it without inheritance but what
we would have to do is when we Define piggers we would have to manually put in
a ask method and a greet method and similarly for any other class you define you'd have to keep copying
you'd be doing a lot of copying pasting of methods from one class to another this avoids that it makes it
much much more practical side note when you're writing a computer
program try to pretend your editor does not have a copy and paste
feature anytime you are find yourself pasting code in a bunch of places what
should you do instead yeah make a procedure right um
anytime you're copying and pasting code there's something wrong in this case if you're doing object during your
programming and you're copy and pasting it's because you don't have inheritance in your language or you're not using it
or something okay so whenever you find yourself copy and pasting in an object-oriented language you say wait
should this class that I'm defining be the child of some other class okay good
um let's move on
so uh first we're going to look at Square let's define oops let's type it
right s to be instantiate
squar um and the way this works is if I give it a number like five oops I say
ask f S 5 it says 25 ask
S 43 oops what ask
s43 thank you I don't know what I did wrong I typed it wrong ask S
100 ask s seven buzz it
says well it's clear why it says Buzz it's because of this um notice in
passing this is a stupid class you wouldn't write a class like this ever uh unless you happen to be giving
61a lectures um but notice in passing that
you can use numbers as messages even though I could not Define a procedure
named seven numbers are not allowed to be the names of procedures so this gives you a hint about the implementation that
we're not actually using Define whatever the message is blah blah blah to make
methods instead we're just saying Lambda of whatever arguments it takes and we're somehow associating that with the
message seven so we'll see more about next week about how that works but the important Point
here is this um a new Clause we haven't seen
before
you can think of this as um an alternative
to uh inheritance to to having a parent clause for messages that you don't know
how to deal with so what what the parent says is if I don't know how to deal with a message
ask my parent this says if I don't know how to deal with a message here's
how and in this case the default method says times message message so we need
another list of special variables in our object system one is
self um and here's two more
message and
args these two exist only in default method so when you're writing a method
that has a name you can't use these um because when you're writing a method that has a name you know what the
message is and youve specified formal parameters
for the arguments but in default method there's no Lambda or anything here uh but
implicitly it's Lambda of message. ARS
um well no I'm sorry it's Lambda args and message is from the the the
conclus anyway the way it works um never mind the implementation details message
is whatever message was sent so if I send the message 43 message has the value 43 times
message message means times 4343 and we get
1,849 okay I didn't use ARs here because uh there weren't any extra arguments so
args in this case is always going to be an empty list but you can write a default method that does take arguments
by looking for them in
args yes what if I have both a parent and a
default method I'm saving you the trouble somebody always asks well first of all it's a screwy
thing to do because as I said these two are different approaches to solving the same
problem which is how to deal with messages I don't know about second of all supposing for some
reason that you do want to do it only one of the two possible interpretations actually makes sense and two possible
interpretations are about which do I look at first do I try the parent first or do I try the default method first
well what happens if I try the default method first it always
works right default method accepts every message so if it if we did default
method first we would never get to use whatever you put in the parent Clause so
the language if you do that it tries the parent first if the parent handles that
message accepts that message then that's what happens we use the parent and if not we come back and try the default
method which will always work okay but again if you want to do that you're
probably designing your class structure wrong in some way um okay so default method there it
is um
okay oh yeah so a new kind of counter
oops oh
yeah so this is just like the counters we saw on Monday now I'll ask
C2
next8 29 and then we were up to seven so I should
get 81 yeah okay so here we have these two counters what's new is there's a new
class variable called counters let's see what its value is
it's not a global variable I can't say
counters Unbound variable but I can say ask either instance or the class quote
counters and here's what I get I get a list of two procedures well those procedures are the
two counters why because of this
Clause initializes it's like method but it's a special method that you only use once
when an instance is created So when you say instantiate some
class one of the things that happens is after we make the new instance we send it the message
initialize um and initialize does some stuff
um besides what you tell it to do so you always do have an initialized method
whether you ask for when or not because of the way the object system happens to work it takes a little bookkeeping to
set up the objects but if you do say initialize we do this thing also and
what this says to do is take counters which starts out being an empty list and
we say set Bank counters cons self counters so counters is this list of
counters and we take self which is this new counter that we just made and we're
going to stick that in front of the list so this is actually the list C2
C1 why would you want to have such a list
well you're writing an adventure game
and uh the user says something like
inventory um so in that case it wouldn't be a list of all the things in the world it would be a list of the things that
the person has but it would be a list of objects um you might want to have a thing where you can say show me all the
objects in the world and then you get a list of all the objects in the world
um so let's take a a simple example of how you would use such a list it does
it's not very interesting to print out but I can say uh
map Lambda C for counter ask C quote
count ask counter quote
counters and I get that c2's count as two and c1s count as
eight okay [Music] um so that's an example of how you would
use a list of these objects when you're doing objectoriented programming this is going to be an issue for you in the
programming project that starts next week um you're going to be
tempted especially if you haven't done object dur programming before you're going to be tempted to do things like
make lists of names of objects so when you hear uh give me a
list of all the objects in the world you're going to think what you want is a list of words a list of the names you
know wand and Canary and ogre and you know whatever they all
are um but you don't you want a list of objects if the user wants to print stuff
then the very last thing you do is ask all those objects for their names but if all you have is the name you can't
really do anything interesting with it what you really want to do with objects is send them messages and that's why we
want lists of objects and not lists of names of objects okay so try to remember
to think in those terms when you're doing the project okay uh that's initialized
questions about that
yes
uhhuh what if the parent says ask self
um greet then the Greet message since self for
that particular person self is the pigger will send a greet message to the
pigger the pigger will say I don't have a greet message so I'm going to do what I always do with messages that I don't
know how to handle I'll send it on to my parent and so it'll come back to the parent
okay okay moving right along
um so last time we had the problem that if I asked a pigger to
greet um it didn't work it got into an
infinite Loop because it tried to convert the N the word my and hello my name is to Pig Latin and it doesn't
think that Y is a vowel so it Loops forever so I'm going to solve this problem in a really bad way so again
this is code you would never write in practice um but it's a good
demonstration to be [Music] instantiate
piger Porky I'm saying this again because I now have a new class pigger
that's important too when you redefine a class any instances you may have made
are still instances of the old class so if you want in distances with the new class you have to make them over
again um you will find often that if you redefine a class the easiest thing to do
is quit uh scheme and just start it again and load your new definition in um
okay so what happens first of all if I ask PP quote
greet it says loh my a orip so it didn't
try to convert this to Pig Latin that's the wrong Solution that's why you wouldn't write it like this in practice
you would try to make it so this comes out I may you know y ma a y um but what I
did here it is so we're looking at the say
method and what to do if it's a word because if it's a sentence which is what I gave it it just Maps ask self say over
the words but let's say it's a
word we have this if if the word is something other than
my let's look at the false case first then we ask self quote piggle stuff which is what it said before but if it
is the word my then I call a procedure
usual um so now we're going to have a list of the procedures that are part of
um this implementation and I'm putting Define
class in Brackets because it's a special form rather than a procedure we have
instantiate we have ask and we have usual and that's it
we're not going to Spring any more implementation procedures on you this is it um usual
says send this message to this object like ask
but start right at the else Clause with the parent send it right away to the parent without looking at the child's
methods so usual say says I don't want to do this say method I want to do my
parents say method the reason it's called usual is
that when you make a child class uh you're saying the parent is sort of
the general thing there's lots of things like the parent and we're specializing that in some way like of all the people
in the world only a few go around speaking Pig Latin all the time so usual means say it the usual way
instead of in pig latin that actually hits an answer to the question somebody here asked before what if you have a
piger and you want it not to speak pig Latin um you can say usual say it won't
work however to say usual ask because we're using the parents ask method anyway the parent would have to say
usual um to not speak pig Latin on an ask but you can make it not speak pig
Latin on a Say by saying usual say but only inside uh a method of this object
you can't type that at a scheme prompt the usual procedure is defined globally
but it won't know what to do uh unless it finds a variable
self um because it it does a sort of special kind of ask self that says don't
look for your own methods just ask your parent um okay questions about
that yeah ah yes what if you have multiple
parents it's not just a problem for usual it's the same problem as if you don't have a method at all um so here's
the deal about multiple inheritance
okay so I have two parents and
um here's grandma okay now the the priority rule
is whichever one you put first in the parent Clause that's the one you want to
have priority right so uh the answer to the
question which parent do we ask is in this case first we'll ask Mom and then we'll ask
Dad okay but what if neither mom nor Dad
no I'm sorry what if Mom does not have a method so I send it the message
Foo there's no Foo here here there's no Foo here grandma has a
foo and dad has a foo okay well if mom had a foo it would
be clear that I want to use mom's because I put her first in the parent Clause but now the question
is which is better a more
specialized method Fu cuz the one that my dad had has is
closer to me right um it's less generic or a more generic method that's
inherited rather than actually in my first choice parent my
mom okay get the problem the reason it's a problem is
that uh I can construct and those of you who do the extra for experts homework will
construct examples in which which Grandma's Foo is the right answer the
thing you want and you can also construct methods in which dad's Foo is the thing you really
want okay um so it's up to the Lang the designers of object-oriented languages
to try to resolve that question and do what you mean and doing what you mean
everybody seems to think these days is not possible um and so they just throw up their hands and say look we're not
going to do multiple inheritance uh and it's because of this Grandma versus dad
problem that's what makes it hard the I mean make setting it up to work right is not hard but knowing what to do is hard
is that a hand up
yeah ah um the instance of Grandma that we make okay when we when I Make an
instance of me and remember these are classes when I make instance of me I
implicitly Make an instance of mom and an instance of Dad making an instance of mom implicitly makes an instance of
Grandma okay so that instance of Grandma herself is going to point to me not to
Mom for the same reason that moms point to me namely if you say ask self
something you want to do the most specific possible thing right and if I have a method for
it then that's clearly the most specific
um our object system this one if you use multiple inheritance does not use the
most specific possible thing because I did a different form of throwing up my
hands namely do whatever is easiest to implement and what's easiest to implement is when I send that message to
M I've decided that I don't have a method for that message so I send it to
Mom Mom doesn't tell me how she got a method she just says yes I can handle
that so I don't even know whether it was Mom or Grandma who actually defined a
method for that message okay so therefore Grandma beats dad in our system because in my object
the only one that knows that there's any multiple inheritance going on my object has no way of knowing whether it was Mom
or Grandma Who provided the method now we could make it possible we could send
mom a special kind of do you have this uh can you handle this message that says
can you handle this message by yourself you know and we could have we would have to build in every object
knowing how to receive that kind of thing um and so we could do it anything is doable but we just did the easy thing
which is let the system do what it naturally does in the same way that you
know if you just naturally Traverse a tree it's going to be a depth ver a search not a bread first search it's the
same thing here yeah usuals within usuals um when you
say within do you mean as an actual argument
expression you usual of usual of say
stuff you can say that but usual isn't something special kind
of syntax it's a call to an ordinary scheme procedure when you say usual will say stuff what you get back is not an
object or a method or anything you get back a sentence right so it's a usual a
sentence just doesn't make any sense um but
also this is why multiple inheritance is so weird when you delegate a message to
some other object using parent you're not supposed to care how
it's implemented your parents implementation is a black box to you as
far as you're concerned the parent itself handles all the
messages so if you put in something that makes the assumption that your parent
has a parent and then they change the way that parent class is implemented because some
one of the other 4,900 199 programmers wrote that class then your your code is
going to stop working okay um multiple inheritance really is a can of
worms um so the point of the extra for experts homework is to convince those of you who really have to convince yourself
of everything that multiple inheritance is a can of worms okay um so that's
usual you should know about usual already because you saw it in lab right
saw it in lab didn't go to lab all right
um okay so that's all the features the object system so there's one two three
four five six kinds of claws in a defined
class uh you can put them in any order um
the only one that there should be more than one of is Method because the other ones each take
multiple arguments right you don't say instance vars a instance vars B you say
instance fars a this value B this value right so only one instance bars um only
one class bars only one parent again it have multiple parents but they're all in the same parent Clause only one default
method only one initialized but a method per
message okay so um oh and the other thing that should go
in some list someplace some list
someplace is the special form set bang um which is the only new piece of actual
scheme that we've learned this week everything else we've been talking about is part of the language implemented by
the file ob. scum ab. scum is written in scheme that's the thing I want to really
emphasize strongly there's nothing that we've done this week that you can't do in plain ordinary
scheme uh next week we're going to see how that happens
um H oh yeah vocabulary and um a piece of vocabulary
that we're going to see again next week but we saw last week and I want to remind you of it is dispatch procedure
so in our system objects are represented by Dispatch procedures A dispatch procedure takes a
message as argument and returns a method and that's different from last week when we did
message passing last week it took a message's argument and just did whatever that message
wants okay here we're saying you call the dispatch procedure with a certain
message and you get back a method we can you know I can show you that actually
um
oops okay um let's call
PP say there's the
method okay so
um when we invoke it what's really going on is something like
this right so that's basically what ask does it does a procedure call to the
object which is to say to the object's dispatch procedure those are the same thing and gets back in method and then
it calls the method with any additional arguments you might have given you don't have to write it like
this because we wrote ask but ask is a really simple procedure
um there's a little bit of hair about you know parent inheritance stuff and
and how that works but most of that complexity is actually inside the dispatch procedure in the else Clause of
that con okay uh any other
questions
yes yeah okay he he's complaining that my example about Mom and Dad and me
makes these things sound like instances um and you're right um it does make them
sound like instances but try not to think that way think about uh pretend it says
person mother father grandparent or something okay and those
are it's kind of weird because um really for all of those are people in in real
life so really it wouldn't be like uh mom and dad I that was sort of a um
little cute thing that I did making a pun about the word parent but you have to think um you know
Square rhombus qu rectangle all that right
yeah okay his question is could we design different kinds of ask for different kinds of objects or different
situations um um and the answer is you could but you'd be sort of violating an
abstraction ask is the way you talk to objects when I did this right here I was
intentionally violating an abstraction just to show you how it works um but what you can do what you would do in
fact is you would build user interfaces on top of the object-oriented system so
your user and this is not how you're going to debug the ADV Venture game but if you actually were preparing it for
use by a user you wouldn't let them put in scheme instructions because then they
could put in scheme instructions to affect the other players or the you know the world in general um you would build
a whole Adventure game language where they would say go east and you would translate that into
ask human quote go east or something right
go go cod e you would say um so yeah you would build your different kinds of
object interfaces on top of ask rather than instead of ask other
questions okay let me say a little word before we go about the J
language um it's more complicated than this
the way they do object-oriented programming is full of details um for
example um we treat once they've once they're made we treat all our
instantiation variables and instance variables and class variables the same way in terms of how visible they are to
other objects namely we automatically provide a method that lets you to get
the value of the of the variable and we do that again mainly for debugging
purposes um but we don't provide a method that lets you set the value of the variable in Java for each variable
you have to say how accessible to other classes you want it to
be um in Java it's a uh strongly typed
language which means you specify the types of variable rather than the types of actual data we
talked last week about um type tag data
versus variables that say what type is in them um and Java is that kind of language so you have to say when you're
declaring these variables not just this is an instance variable but this is an instance variable of type integer um and
in many other ways uh it's more complicated than what we're
doing here um that's neither good nor bad really it depends on what you're
trying to accomplish again if you're doing uh a team of 5,000
programmers maybe you do want to really pin down every detail about how your
object class works and how it interacts with other classes um if you're just learning about object ored programming
on the other hand uh the simpler the better I would say for your first time around so I think I hope that what we've
done this week even though it's not the same as Java will prepare you to think
about 61b and all the stupid syntactic details of 61b semicolon blah blah blah
brace and all that stuff be able to think about that without losing sight of what the basic ideas are on Friday uh
you're going to get to hear from Dan Les it's a a recorded lecture you've heard
the name Dan Eng Les before in the Alan K lecture he was the actual implementor of small talk and he has a point of view
on object arer programming that's just a little bit different from what I've been saying and that's why I want you to hear it okay see you Friday
UC Berkeley