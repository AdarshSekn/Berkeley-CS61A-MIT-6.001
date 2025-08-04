Transcript


uh Hey guys uh as you can see uh your midterms coming up for this class um
pretty soon believe it or not so we're holding another review session uh HK uh
it's going to be uh Sunday 36 from 2: to 5 uh in the HP Auditorium 306 soda so
show up if you want some practice
okay so the the other administrative thing what Jordy put up on the board over there um today is the first of
several grading complaint deadlines um we talked about this at the
beginning of the semester uh the today's the deadline for midterm one project one
and homework one through five all of those scores should have been up for at least a week um if they're not up or if
you think a score is wrong go to the class web page there's a link about
grading complaints and you go there and there's a form to fill out um the reason we have deadlines is that before we did
it used to be uh the day after we published the final exam
scores um I would have 40 students lined up outside my door wanting to tell me
about how homework three never got a grade um because you know the the
grading steps are about 10 points apart that means one tenth of you which is 40
people are going to be one point away from a grade step and another tenth of
you another 40 people are going to be two points away from a grade step and so on um and that's true no matter what
policies we use a bed grading leniently or harshly Whatever It Is 40 people are
going to be one point away from a deadline so today is the deadline for complaints about project one homework 1
through five midterm one and says over there what to do okay
um our master plan for the semester is to talk about four programming paradigms
two of them at some length and the other two very briefly um we've been doing
functional programming we're done talking about about that it doesn't mean you're done using it we're done talking
about it um for the most part we're going to be talking about object-oriented programming which you've
certainly heard of and have probably actually used in whatever School you
were at before this one um I'd like you to try to um forget that you've used
object oriented programming and and really look at it with you know beginner's mind um so that you
[Music] can see maybe a different point of view about it from what you've seen before
not that that other stuff is wrong um except where it is but uh having more
than one way of looking at it will help you understand the big picture so the big picture is up here this is an
abstraction diagram uh a little bit different from the ones you've seen before because of that dotted line
partway down um the dotted line is an abstract action that takes place entirely in your mind so there aren't
any selectors or Constructors associated with it um above that dotted line
is the central metaphor of object-oriented programming which is that of multiple
independent intelligent agents so multiple you know of course
means there's more than one which is different from what's really going on inside the computer really is the one
computer running your program um but we're trying not to think
about that and instead we build an abstraction in which you know every
window in your window system is a separate entity every spaceship or
gorilla or you know Pac-Man in your game program is a separate entity and so on
um independent means that each one has its own program um
some of them may be similar to other ones and some of them may be completely different from other ones but each one
runs independently of the other except that uh they have ways of interacting
with one another so it's just like you know in this room there are a lot of
people and um you can you know go over and tap your neighbor on the
shoulder um and by doing that you are um causing that other person
to get a message that you want to have some kind of interaction um but most of the time the person you're tapping on
the shoulder does whatever he or she does completely separately from what you do
and just every once in a while you interact uh so that's multiple
independent um intelligent means you know they know how to do
stuff um so it's different from the data structures we've seen up to now uh for
the most part the data is just data it's like numbers or something and the
intelligence about how to do things is in something separate from the data which is procedures and here we're
putting those together so that um these agents have data likee aspects they
remember stuff but also they know how to do things um so that's the
metaphor um now in order to implement that metaphor looking at it from a
technical standpoint there are three things we need and that's what's right underneath the dotted line the three
things are message passing which we talked about last week local state which
we'll be seeing uh this week and we're going to really understand better next week and inheritance which is the idea
that um some of those independent agents are a lot like other ones and you don't
want want to have to program each one from scratch okay you want to be able to use
the behavior of one you want to be able to say this kind of thing is just like that kind of thing except for the
following differences um so we if we have um let's
say a kind of object called a person um and there are many many
behaviors that all people share like we talk and we walk and we eat and you know
things like that um and uh then we can say well uh
there's a class of professors who are people and they do everything people can do uh but they
also lecture and then there's a class of students who are just like uh every
other people except they have haircuts you know
um so uh that's inheritance and we'll be talking about that
um what we're doing this week this is stuff that's not in the book The reading
for this week is in the course reader um and we are implementing on top of
scheme a kind of scheme Plus+ an objectoriented system in scheme um based
on scheme we're doing that in order to make
what a connection between what we're going to do next week and what you've
probably done before in classes and what you'll certainly do next semester in 61b uh which isn't going to look much
like next week's exploration of how to make object-oriented programming
actually run in scheme so we're starting with something that sort of uses the vocabulary that object-oriented
programming uses and then next week we're going to see how that's actually implemented U but I'll give you a
hint um [Music] it's going to turn
out that um once you have Lambda object-oriented programming is
just a trivial application of Lambda um and I'm saying that because there's
kind of a Mystique about object-oriented programming that you have to have a special object-oriented language to do
it in um and you'll see that that's not true if you have a good programming
language to begin with with uh adding object duringer programming on top of it is no big deal
um and that's good because you should understand how things
work right uh one of the goals of this course is when we show you about a
programming Paradigm we don't just want you to see how it's used we want you to also understand a little bit about how
it might be implemented um because you know that makes you a better and wiser
practitioner later on okay um there are
four components um to our object-oriented language uh they're
Define class instantiate ask and usual um ask and usual or like selectors uh
Define classes like a Constructor sort of and instantiate is actually both
because in this language as in most but not all objectoriented languages we have
the idea of classes and instances so person is a
class U Brian is an instance of that class
okay so an instance is a particular one the class is sort of the general description of the behavior of things
like that um so Define class creates a class where what instantiate does is it
takes a class as argument and creates an instance of that class so from the point
of view of the class instantiate looks like a selector but from the point of view of the instance it looks like a
Constructor got that so who's who's with me on that sort of I'm seeing some sideways
thumbs so okay um if I wanted to model Us in in my computer program I would
start by saying Define class person blah blah blah and then I would say Define Brian
to be instantiate person blah blah blah
okay so instantiate looks at the person class
and sort of pulls out from that the information to make an instance um which is Brian okay um so
instantiate doesn't make a class it it's a selector for classes kind of but uh
it's a Constructor for instances all right so let's look at some examples maybe that'll make things
clearer um the way Define class works it's um
it's a special form uh which is to say it doesn't have
the standard syntax of scheme quite and it doesn't
have uh applicative order evaluation and
the pieces of a defined class are called Clauses um and they're kind of like con
Clauses that's where we got the name in that there's a bunch of them but they're different from con Clauses because con
Clauses you really only do one of them and here we're going to actually use all of them
um so actually Define class oh sorry first things first if you look at the
highlighted text right here in the second half of the screen um you will see that in order to
use Define class we have to first load this file from the library obum u in which these things these four
things are defined okay
um so that's the first thing I should have said so now Define class it's meant
to remind you of how Define looks uh when you're defining a procedure so If this just said define instead of Define
class we would be defining a procedure named complex and it would have formal
parameters real part and imaginary part right and then all this other stuff
would be its body okay so that's how defined for procedures works and defined class has
much the same structure even though it's doing a different job so we are defining a class named complex it represents
complex numbers um and these
things are called instantiation variables which are like arguments to
the class um I'm going to start writing things
down here so we have the names
class instance and now I've talked about
about instantiation
variables um oh and I used the word
clause so to show you how an instantiation variable works let me uh
Jump Right In and Make an instance of this class so I'm going to say
Define D1
instantiate complex
34 so C1 now represents the value 3 + 4
I um if we actually look at what C1 is uh it's a procedure that's what we're
going to be talking about next week how we do this um but it's much like the
message passing approach that we saw last week where um a datum takes the form of a dispatch
procedure that you call with a message and it does something or another okay
um so what can I do with an object once I have it well that depends on its
methods a method is the name of a kind of clause so Define class has um a
pretty small number like half a dozen or so kinds of Clauses and each one starts
with its name so method is a kind of clause that's in a
defined class um
and the syntax again is meant to look like the syntax of Lambda so if you
imagine for a moment that this says Lambda then inside these parentheses
here would be the formal parameters I'm sorry uh not the Lambda I take it
back back up like defined for procedures so if this were if this said
define we'd be defining a procedure named magnitude with no arguments
right and this would be its body and method is exactly like that it
is making a procedure uh but it's not doing it in quite it doesn't give it a name in the same way that Define does
but we can use these this way I can say ask which is one of the four pieces that
make up this implementation and now I put an object um ask is an ordinary procedure
so this thing C1 here that gets evaluated it happens to be a variable
whose value is an object but I could have said ask parenthesis instantiate blah blah blah and that would work too
um and I'm going to send it the message magnitude and magnitude doesn't require
any arguments uh so that's all I have to say and it tells me five which is the
magnet Square Ro of 3^2 + 4^ S right which is what this says to
do right because real part is three 3 squ is 9 imaginary part is four 4 S is
16 9 + 16 is 25 the of 2 is 5 um and we can say uh ask C1 quote
angle and it's 9927 blah blah blah
radians um in our object
system we provide automatic messages and
methods to look at the values of these variables so I can also say ask C1
[Music] quote real part you get the answer three and
similar imaginary part will tell me for okay um that's just a design
decision that we made many other object systems do things differently because there's a whole other story that you
might hear about object Orient programming that revolves around the idea of information
hiding uh and that story goes like this um the way you get bugs in
programs is this piece of the program does something that affects the behavior
of that piece of the program in ways that you didn't intend and this and that are widely separated in the code and so
you don't catch the dependency and to prevent that what we do is we build a wall around each object
class um so that nobody else can look inside
it at the values of its variables for example um unless there's an explicit
method so when you're designing a class you get to say exactly how somebody outside the class can interact with you
um that's the right way to think about object-oriented programming if you're on a team of 5,000 programmers you know
writing a huge project where it's easy for you to write code that steps on someone else's toes or vice versa so
everybody builds a wall around their thing and says how you're allowed to interact uh you guys are not going to be in teams of 5,000 you're going to be in
teams of one or two um so that problem doesn't apply so much and uh as I think
I said once before your programs are never going to get into production you're interested in your program only
as long as it doesn't work um so the goal of our language is
to make debugging easier rather than to hide information um so you just automatically
get ways to examine the values of the every variable of every object
yeah is each class acting like an interpreter well um
only in the sense that its methods are scheme
code right um what the way you actually run the
program it could be interpreted it could be compiled so each class could turn
into you know machine language um that has to do with the underlying scheme
implementation I don't know if that answered what you mean or not let's go on we'll
see other questions okay
[Music] um okay so far this example uh doesn't
do anything that we couldn't do before you've seen in fact precisely this example near the beginning of chapter
2 where um a complex number was created with a real part and imaginary part and
you had procedures called magnitude and angle that would take a complex number and do precisely these
computations um so all we've done is taken something that we knew had to do
already and recast it in the language of message passing
um let me just say a word about this quotation mark right
here um it means what it always means namely
the thing that comes after it is the actual datam that we want to use
um generally speaking that's how messages are going to be presented in
your code is when you're writing the program you know what message you want to send an object and you want to put
that message right in your code and the way to do that is to make it data which is to say you quote it uh but I don't
want any of you developing mystical ideas about how quotation mark is part
of the idea of being being a message a message is just a word and you know I could have said ask
C1 um word quote whoops quote real quote minus
quote part oops I spelled it wrong
okay ask C1 word quote
real quote minus quote part and you would say three all right
so don't get hung up on the quotation mark it means what it always means in scheme
yeah okay the question is why don't I have a method real part and the answer
is again in this particular objectoriented language we automatically generate those methods for every
variable of an instance okay so it's just as if we had said method open print real part Clos
print real part but we provide those automatically for every variable okay and we do that again
because it makes debugging a lot simpler if they're just automatically there we don't provide automatically
methods to change the values of variables um most oop languages don't do
either one you have to provide methods both for looking at and for changing variables our choice was uh we could
have provided both of them automatically we could automatically make a method called set real
part you know um but we decided uh it should be easy to look and not quite so
easy to Tinker that was our design Choice
um Okay so let's move on to something more
interesting um which is this counter class and let
me before we even look at the definition let me show you how it works so Define
C2 instantiate counter and there are no instantiation
variables that's all I have to say and while I'm at it I'm going to make another one
or be quiet not interested thank you okay so
now I can ask
C2 next I'm
gonna and now I'm going to do that again and again and again
okay so every time I say next it gives me a different answer so this shows that we're not doing functional programming
right I call the same procedure with the same arguments and I get a different answer each time so we're out of the
realm of functional programming which you clearly is and into the realm of local state local means that each object
has its own memory um so I can ask C3
quote next and it starts from one and now I can go back to C2 and it
still remembers that it was at four so it gives me five so each counter has its own separate count that's what local
state means okay questions about the idea
yeah um okay the question was I can predict what C2 is going to do next it's
going to say six so why is it not functional again the definition of functional
programming is that every time you call the same procedure with the same
arguments you get the same answer right there can't be any memory of past
history and what that buys you again
is the absolute certainty that that other piece of the program isn't going
to do anything that affects this piece of the program so for example if you
want to have um multicore computers doing things in parallel you can uh let's say you you're
looking at a function call with three arguments Each of which is itself a
function call okay so we can take those three function calls and give them to
three different processors and we don't have to worry at all about who finishes first or any of that stuff because they
aren't interacting with each other whereas if we have a function call and
two of the argument expressions are both ask C2 quote next then we have to worry
about okay is this one going to be six and that one seven or is this one going to be seven and that one six okay so
that's why it's not functional other questions yeah
yeah okay so now let's look at the way it's actually defined um which is up
here and the thing that's new is instance
bars um and the way to think about instance bars is it looks kind of like a lead with name value
pairs okay well the first part of a lead it doesn't have a body so let me write instance bars up here on the board
and I'm going to write instance variable over
here in our vocabulary list and notice that the name instance variable is a lot
like the name instantiation variable and the ideas are very much the
same also the difference is where does this very iable get its initial
value okay when we create an instance how do we know what the value
of real part is or how do we know what the value of count is for instantiation
variables the values come from the call to instantiate so back
here when I made the complex number C1 that's when I said what the value of
real part and imaginary part should be okay whereas for the instance
variable when I instantiate
counter down here I don't say what the initial value
of count is because every instance is going to start with the same value of
count and so I put it here in the definition of the class okay does that
answer your question okay so initial value from the class definition that's an instance
variable initial value from the call to instantiate that's an instantiation
variable and the purpose of the difference is does every instance have
the same starting value in which case we use an instance bar or does every instance have a different starting value
in which case we use an instantiation variable okay um
so that's one big difference here the next big difference is
this um that's an exclamation point right there it's pronounced bang so this
is set bang um that should go on another list
set bang is an official built into scheme special form
um that its notation is just like a Define the kind of Define that doesn't
imply an an invisible Lambda so you say Define name value we say set bang name
value um the difference is Define creates a new variable set back bang the
variable has to already exist so if there weren't an instance of ours count
in here then it would be an error for me to say set bang count so
whatever right um this is what makes our objects
nonfunctional is the ability to change something that already exists it's different from let right let
kind of serves the purpose of give this variable this value and you may have been thinking about let in the past when
it's part of a recursive procedure as if it were kind of an assignment statement to an existing variable but it's not
every time you run a let it makes a new variable for each of its name key name
value pairs so if there was already a variable of that name then they both
exist they're two variables with the same name and different values and they're both around and which one you
get depends on where you are in your program um set bang is not like that it
doesn't make a new variable it changes one that was already there um the convention in scheme again it's not
enforced by the language it's just a convention is that anything that changes the value of something has an
exclamation point in its name like said bang um to let you know that it's doing
mutation because that's very important it means you're not doing functional programming
so if there aren't any exclamation points in your program then you are doing functional programming basically
and if there are then you aren't um
so the method next I mean it's not very subtle it says take the the value of
count add one to it and replace the value of count with this new value in other words add one to count and make it
the new value of count and then when you do setb set bang Returns the word
okay um in the scheme standard it says the return value is unspecified we make sure to return
something useless uh to kind of rub in that it's unspecified and that's why
after the set bang we have this count here um so you've actually seen things
like this before with print instructions but uh officially this is another new
thing that we're giving you um which is up to now the body of a procedure has
pretty much always been one single expression because a procedure can only
return one value that's still true a procedure can only return one value but
it's possible to have more than one expression in the body of a procedure if so those expressions are
evaluated in order so first we do the set bang and then we evaluate
count um the value that the procedure returns is the value of the last
expression the values of all the earlier expressions are
ignored okay they're computed and ignored so presumably all but the last
expression uh are in there to have an effect on the World to do something
rather than to return a value even though they all do return values the values might be things like okay or the
value might be something would conceivably be useful um but we're just not interested in preserving it and then
the last expression the value that it returns is the value that in this case
your method next returns questions about that
yeah can you do set bang of instantiation variables yes once the variables there you can treat it like
any other variable question yeah
right yeah if you wanted to say what the initial value of the counter was uh then
you would make count an instantiation variable rather than an instance variable that's exactly the difference
between instantiation variables and instance variables so our variable the initial value is zero but the first value return
is one because we do this plus count one thing before we return the value
yeah can set Bank take a procedure is a value argument ah thank you good
remember first day of class I said over and over again in this class people are going to say Can I use in the context of
and the answer is always yes right this is one of those yes absolutely the value of a variable can be any legal scheme
value okay um It's A Hard idea to get through
your head that that's always true but it's a great principle
yeah yeah again this particular object language gives you automatic getter
methods examination methods for every variable so yeah you can say ask C2 quote count and it'll tell you it's
count it's current count without incrementing it yeah
yeah if you if you if count were an instantiation variable you would say
instantiate that's the verb instantiation is a noun instantiate counter five and then you would say s
counter next or you know it's Define you know C4 be instan a counter five and
you'd say ask C4 quote next um and it would say six yeah if you wanted to you
could build a set method into your class you could say method set count new value
new value would be the formal parameter of the method um set bang count new
count and then people would be able to change the value of the counter on the Fly it's up to you what methods are in
your object
yeah can you have one class that either does or doesn't take an instantiation
variable I'm actually not sure what the answer to that is I think
not um I mean you certainly can't have two separate defined classes or the same
name it's like any like defining a procedure the one you do second is going to win um the question is can you put
rest arguments with the dot notation in a defined class and I have no idea um
we'll try it later but don't okay a lot of times let me tell you you know you're
going to come up with a lot of questions this week of the form can I do the following screwy thing
um and the real deep answer to that question is maybe you can and maybe you
can't in this particular object language but the object of the exercise here if
you pardon the pun um is not for you to get intimately familiar with the nooks
and crannies of this system it's for you to understand sort of how one does
object dured programming so I'd rather focus our attention as much as possible
on kind of mainstream things to do rather than peculiar things to do okay
all right let me move ahead we're actually going very slowly here so I'm gonna um where' my cursor go there it
is a b um so here's the
doubler class um let me make one
one and I'm going to say ask D quote say quote
hello it says hello hello the only purpose of this example
is to show you that ask can take extra arguments and what those extra arguments
do is they car correspond to formal parameters in the method so this is the
first time we've seen a method with a formal parameter um it works just like formal
parameters of any procedure so stuff has the value of this
expression which is the word hello um this isn't a very interesting object
in particular there's no reason to ever make more than one of it because it has no local state so one doubler is exactly
like another doubler this is a kind of functional object um and the the doubling happens
because of what's in the body where he say sentence stuff stuff okay everybody
with me all right
okay so here I'm redefining the counter class um so let me go ahead
and Define G4
instantiate counter Define
C5 stangate counter
ask C4 quote
next so it seems to be it seems to be giving the same number twice every time
we call next and now I'm going to ask C5
next and you'll see what the two numbers are all about the first one is specific
to each counter each individual counter starts at one the second one is a count
of all the times any counter has counted so if I go back to
C4 I get six which is the number after this
five and I get seven there's been seven nexts on all counters Al together okay
and uh what's new to make that work is this class vars
so class variable is an
idea and class vars is the Clause that
implements it class vars looks just like instance vars which looks like the first half of a let
um except that the meaning is different
namely there's one variable total which is created as soon as I do
the Define class instance vars are created when I
call instantiate so every time I say instantiate counter I get a new
count but total there's only one total it belongs to the entire class it's not
a global variable if I say total says Unbound at the scheme prompt um but it
belongs to the class and each member of the class can use it okay so this is good for situations
where you want to keep track of something in common to every instance of a class um it's a useful
idea uh I can ask a particular counter for
the value of total I can also ask the
class for the value of total so you see now that classes accept messages just
the same as instances do not the same messages I can't say ask counter next it
will give me bad message to class next um an error message but
um I can ask it to because that's something that is shared by all the
instances okay um
oops okay so moving on
Define BH instantiate person quote
Brian okay so there's a person class um and there's three methods for
the person class so I can ask VH say
um I love
scheme and it does that's not very interesting the method is
just stuff right say stuff stuff um I can say ask BH quote ask notice it's a
complete coincidence uh that the name of this procedure to get objects to do things is
the same as a message in this particular object class nothing to do with each other askb would ask
um study for the midterm and it will say would you please
study for the midterm because it uses
self which goes in some list someplace over
here um self is a kind of hidden instance variable that every instance
has whose value is that instance itself so the ask method doesn't just
return uh would you please stuff it asks itself to say that that's going to
become important in just a moment um and then the final one is
greet I can say ask B quote
greet uh no argument it says hello my name is Brian um just a note in
passing what's the name of this
instance tricky question right it has two names one of its name names is
BH which is the name of a variable whose value is that object that's the name we
use to get at this object from the outside and then it has uh an
instantiation variable name that's kind of its internal name and that's the one that it knows about it has no idea as
usual in scheme it has no idea that there's a variable whose value is itself
other than self it doesn't know anything about the variable BH which is a global variable not an instance variable or
class variable um but it does know that its name is Brian so these particular
objects have internal names and external names and I'm emphasizing this even though it's not very interesting
intellectually because when you work on programming project 3 the adventured game which is coming up uh your objects
will all have both kinds of names and I want you not to get confused about that
um okay now for the fun part in three
minutes toine PP instantiate St for Porky
Pig pigger quote
Porky um now what does a pigger do well it has the same method
and it same method basically says um call the piggle method on every word of
my input if the input is a word just call piggle on it otherwise map calling
piggle over it if it's a list of words a sentence it really should say every that's a boo boo
um so I can say uh ask PP quote
say quote um I love
the Bealls and it will say I
of who doesn't speak pig Latin anybody few people how Pig Latin you know how
Pig ltin works we did it in the first week go back to lab one to review Pig Latin never mind forget I asked okay so
that's how its same method works now notice does not have in this class
definition an Ask method or a greet method nevertheless I can say ask PP
quote ask
um f more be
music it says play a play or May
May right right how does it do that it does that because
of this Clause so we have a new kind of clause which is
parent and that's a technical term also this has to do with the question of
inheritance which is the third leg on which object-oriented programming rests
this says a pigger is exactly like a person except for the methods defined
here so persons don't have a piggle method so only piggers know how to do that persons
do have a same method but we don't use it we use this different same method
that speaks in pig latin right so what about ask
well if we back up just a bit
here's the ask method for people it says ask myself to say this
remember when you saw this originally for people you thought huh you know this is why go through this effort of asking
myself to say when say just returns its argument without doing anything now you see
why when a pigger gets an Ask message it uses its parents ask method
but inside that method self is a pigger
so if I ask myself to say something it says it in pig
latin okay pretty cool huh uh we're out of
time so I'm not going to take questions now I just want to show you the problem which is ask P quote
greet so we want it to say hello my name is
and nothing happens it's in an infinite Loop why because we have a very
primitive idea of what a vowel is and so the word my doesn't have any and so this
thing is buzzing around trying to convert my to Pig Laden and we'll solve that problem on Wednesday
UC Berkeley