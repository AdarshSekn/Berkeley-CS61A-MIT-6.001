Transcript


okay good afternoon today we're going to
hear a slightly different take on object-oriented programming maybe a
little more like what the rest of the world thinks but not entirely like what the rest of the world thinks this chart
that Jordi is writing on the board actually is about where the rest of the world stands relative to what Angels was
talking about to help you understand the lecture I put up on the board here a
translating dictionary between his names for things and our names for the same
ideas these three are actual things in the language that's why they're in capitals when he talks about a small
integer he doesn't mean six or seven he means anything less than absolute value
less than two to the 31st he is going to define a class point in small talk and
these three boards are the equivalent definition of class point in objects
game OOP language so if you can leave these board lights on at the table with
the boards while watching the video thanks that'd be great go
and then use those increments several Uruk applications such as a music system and an animation system and then we have
the opportunity to do something which most other projects get too big which is what is evolve built instead I going
commercial and delivering it we got to throw it all away and do it over him the way we would have wanted to do it and in
the process we get signed address complexity because the applications were quite complex and we had a chance to try
out several solution dealing with that complexity and when you try to try to
break that complex problem down you want to try to break it down into it it's two
parts you can and you want them to be as independent as they can be I just leave
you with a simpler analysis and then if you have general parts that you put
together I'm ready to have available when you use them to put together a system it would
be easier to learn because there are fewer components it can be more
productive because the compilers are hopefully more gentle and assistance to
build will be more maintainable because those with fewer components you'll
encounter less things you don't know about when you're going to making it now
if you look at the evolution of computer software systems over the last 40 years
or so he kindly started out with incredibly basic components that were
not at all flexible to speed instruction to the machine in the memory cells available in it then on top of that we
put a more general layer with formulas for the instruction symbolic sort of
description and very folks can fit a simple memory and then we added in the
notion of procedures which sorted made it much more flexible kit of things to work with because now you could augment
the basic set of instructions where available and then soon after that time we also develop data structures which
again I wanted you to define your own memory primitives that differ and in
each level it became possible to break problem we found or completely generally
then toward the end of the 15th the beginning of the 70s we discovered as we
try to do more and more complicated things we discovered further problems for instance the use of go-to in
procedural effects that made things nothing jewelers and we rule that as the
structured programming principles and also in the area of data structures people were using data structures in
unclean ways as we cleaned that up I am the use of extra data types where you
basically bundle the data with the procedures that work on it and hide the
information behind so this is where we were at the at the beginning of the
seventies and the problem is that one still encounter difficulties when
building really complex systems for instance if you do a large simulation
like that you'll have several different kinds of data in that simulation for instance in
hospital he would have doctors nurses and patients and in building data
structures for that simulation you and we implement structures fourth and Clark
cubes drinking for two of paper waiting her door and some programming languages
at that time required you to have a different kind of two for every kind of pen you're gonna put into it they're
going to get too large in relation as becomes impossibly difficult or in this
example you would have doctors nurses and patients all waiting at the elevator sometimes record or so it requires the
to be able to have all these different kinds of medications
and there would be code like this scattered all over the city now what you
have to do then is inside of the killer this is even if the programming language allows you to do this he'll have to have
text on what kind of thing is in the queue since if you want to display
everything if you you have when you have the type of the thing yell and you
conventional style if you build it for
large in this way you'll have at first pin and a hundred version code scattered
around the system and it becomes a nightmare to maintain it's also harder
to build because he just had the sheer bulk for that code to write in order to modify because you have to maintain
consistency we build and change one thing you have to change all those places where it occurred it's also
harder to understand because if you come into a system that's perfect way you
can't see the forest for the trees you just confronted with a mountain of
irrelevant details and example here is this spot if you wanted to add janitors
now to this simulation you have to go back and fix up all those places which
would be a tour and that's assuming that you found all the places that you needed to fix up and you get fokin it
inconsistently sees regard so there's a crystal at work here which is if any
part of a system depends on the internals of another part then complexity increases as the square or
the sides of the system in other words in each of the places we set a piece of code that's getting bigger and bigger
not just because of what it does but because the rest of the system is getting larger
and you can turn it a bit graphically as you think okay you get these little circles the number of parts of the
system and the blue line has the interactions between them they get to be more and more blue lines because you get
a forest but you simply can't deal with this is truly to limitation to what you
can generally accomplish there are a couple of approaches you can go from there and you can stick with simple
problems that's part of the academic approach but then there's the industrial military approach which is demanding or
whatever see if it's actually a better way in other words the complexity you
have is not so much intrinsic to the task of trying to do it results from the
point of melee attack and what you're doing and it was the people who worked on
stimulus first we ran into this problem and saw a way to deal with the
situations more simply what they did was to sort of change from the procedural
fuse which is that in these procedures who have been there was dispatch on the types of the object and they flipped it
around to the other point of view we can see aspect oriented one which is that within every type of object you have all
the procedures that work on it and so in addressing an object you need to
dispatch on the procedure you want to call it so as we go back and look at the
situation we had before it can be represented pretty much this way testing
on the type of the object but they said one thing they operate on say print in
the queue you test if it's pipe and a band called a version print if the place
is B then cold bean version of print if the type of squeeze and close game version of print you can collapse that
in into one more general statement which is just to call extra type version of
and then you can still simplify that commodities it as Residex and
encapsulate them extending the message print to be out there and letting us take do it up however at once free and
if you go even farther to decide that you're going to do everything in your language this way and you don't need to
have a certain feeling to quick look look you see you can this right at the
print for it hungry whatever so let me take a minute
in to prescribe the smoke accessory so I got into the syntax for both simple
operations such as asking for something side or cleaning an object where you
just say hey Scott have you been domestic ties to the IPA and return some value we go to learn
arithmetic form of this and here's the confidence statement a size plus five this would be accomplished by sending
the message size to the object taking the resulting value that comes back and sending message plus five to that and
then for larger procedure code if you will that have several parameters you
can comprise a message in the following way this reads is eight plus five between zero and two top that would be
evaluated by sending message plus five to a getting come result and that result
would be sent the message between and with two parameters to zero and the top
limit to top and it's intact with the
key words and with putting the receivers at the beginning reads a little bit like English and in the team's look at
something like a music system that's been built into place you find statements that mean very naturally is
kind of a micro language heaven to get with music for instance and favorite instrument play this note
so for a little bit of Criminology we have objects and they are described by
classes that have certain factors the description but what the object consists of and what they're capable of doing
then we have messages which would be intense and we call the part of their
name of the message that selector and the message is the electric pulse
whatever value has been synonymous and finally we have methods these are divided into classes and they are the
specific code for how to carry out the request implied by the message and if
you have it to work in just a simple kind of object will consider how you
model XY coordinate pairs which in twelve up we could call the last point
the first thing in the class describes what fields are in the same way there's an x-coordinate and a y-coordinate these
are local variables in each instance of a point and here is a protector from all
the messages that are understood by point and the code that is invoked the
methods that are encoded message so the first one is s : y : which allows you to store into three
variables inside a point with the new Mex and Y for you it could end the point
the messages say that would return a text message if you send us a message while return it's Y value if you send us
a message plug in another point then it will create a good point and they knew
to the class which will make up any one applies and initialize it with an x-coordinate which in this point set
plus the other point set and the y-coordinate which is this point line plus the other point
and it is just a short way of doing sort of vector addition of these two
coordinate pairs and this last message down here would divide a point by a
certain scalar value creates a new point and this x-coordinate is divided by him
from the caleb is well having made this
description we can now build a rectangle from these points here's the model for a
rectangle which has two fields in each okay it's a point describing its top leg
corners and opponents at renovators bottom right corner and there would be a
couple of messages in this class top legs return the top left corner onward to return the bottom-right corner and
now you can see how the capabilities that we gave gave to me allow you to do interesting things very simply for
instance he can ask for the center this rectangle for which there's no stored
value and it will invoke this lesson here which says return for tock length plus the bottom right / - and make those
messages will invoke the similar code back in class points will return in the
pointing to the coordinate is the arithmetic mean of these two points which will in fact the defenders that
rectangles so we're building up a little sort of a graphical micro language here
it's really just a set of procedures but they can be described very truthfully in this manner and let me show you how that
works inside the rectangle is a little
picture storage and it has a pointer to it's quite and AB in the class but the
information is stored about what fields is that because credit talk like that about right and these names correspond
to the clock in every little rectangle
adults I pointed here from the class to an actress called a myth and dictionary and it's Carla seeing names as the
messages pink pencil collectors with the code we submitted for we're turning the
appropriate values so here's the top left and there's the message because your turn out--we here's an entry in the
dictionary under the name Center and your clinic up to the messenger center
and these structures that are put together effectively so at the point the
point for the path west point to another walk out there this one is an instance
of class point so it would point out to some description of flex point at first and I'm excited because and these other
clinics just the same way that it has different values to protect now having
put all those things together it's now possible to produce completely complex
simulations without running into the problems we had by mixing different
similar interacting datatypes but there's still some problems when you
want to go describe a new class or data you have to write the whole thing from scratch and also you'll find many places
where there's the same kind of code for instance if you're talking about collections he might have array anyway had character
streams anyway have dictionaries and you'll have similar code for doing kind of say collecting all the elements for
which special measures true don't actually have copies of that code in all those classes so once again you're into
a problem mode it can go you can build one complex system once again you start running into a big limit except that
complicated things are in the way for dealing with these problems is begin to
try to simplify and get mixing more general in the the concepts we have to
take advantage of here is inheritance ingeras it's very simply put into the
implementation I showed you by having a chain it goes from a class up to another
class from which it will inherit behavior that way to send the message to this object and it's not filmed in the
method table for this class then it will go looking at super clinics and see if
there's a definition for that message here and this continues on up all the way to a sort of a default superclass
which describes the general property property with all object and what the
inheritance allows you to do is to save a lot of code here's an example of
factorial and here's a simple description forgot fact if you send the
message factorial to an injured then it says am i less than or equal to 1 and it's true effective and return the
result woman if it's false in return myself minus 1 multiplied by myself so
this is a recursive definition of factorial and notice the comments are integers and here integers inherits the
properties of all not to neglect these simple things but that are instances but
the properties to find an integer are inherited both by small integers which may be compact and that particular tax
operation and also by large integers which may have a greatly extended range
of behaviors so if you asked to compute the factorial of 20 or something it will
go through this calculation let me just
show you how the video to the samaritans work both named classes here will
inherit from class integers now what's interesting is when you actually invoke
this code running something like factorial of 20 there will come a comment
people start out being small integers because when T is a small integer but there will come a time when the
factorial of the number that smaller will actually be a large integer and we
have here an asterisk implying multiplication in most programming
languages most conventional programming languages it has to be known what the clips of the integers are on both sides
but because that is simply message if it's the name of an operation this code
will work regardless of whether the receiver is a small integer or a large integer or some completely different
kind of integers into five so there's a spectrum is area symbiosis between the
the inheritance that's available in the system and the polymorphism in other
words the ability to work with any different types with Canaris in the sending of messages and what this does
is it makes code much more reusable means you can have generic code
throughout the system in some super class it can be used by all of the classes and it greatly factored the code
system you can then add messages
subclasses or override from Princeton tier you can object called a pin might
have some little over a minute to draw a line for certain different commentor at certain angles for doing some geometric
to the ninth you could define some class exact call the commander which we do all
the same things but which might actually own a whole set of pins because when it
was told to draw a line of a certain length it would tell all of it to go a
lot differently you could make really fun design in that way and then you could define another class below that
called the collider which we do a kaleidoscopic present pattern and the
only thing you have to do would be to override the turn operation so that when I sub in it would turn
opposite directions for every other pin and you get a kaleidoscope effect and
all of this has done without having to write any code and your subclasses except for what's different and you can
also make use of the code that you've overridden for instance an initializing commander it can invoke the initialize
code that's inherited by his parents by thanks super initializes and presidio
variable it's like sending the message to excel but using the definitions inherited from above and then it can put
in and go in particular code as well but it wants to go for initialization so in
this case it would initialize both normally and then span out operations would be one which would take all the
sub pins instead of all starting the same directions with spread them all
another point that I'd like to bring up that I think as a part of object-oriented programming although
it's probably not a strict requirement but it's certainly through the complexity issue it's automatic storage
management if the system doesn't have automatic storage management and then it
inevitably has all sorts of code sprinkled throughout it healing with the lifetime storage and with the codes that
are true if do you need to get the code wrong so charges to look properly it
doesn't tell you anything about the problem of things that also in that sense irrelevant detail and if it's
wrong it will cause the system to fractional scarily good think that if
we're going to talk about what it means to be object-oriented I think we'd have to assuming that the language is high
level to begin with and I think about pneumatic storage management it's being a requirement for any high level
language I'd like to talk just a little bit about the operating system interface
which is another area that's important in object-oriented programming languages because if you try to hold
object-oriented committed to a conventional operating system even have problems with the interface to really
detract from the overall value of having an object-oriented programming language and I think which need to do is to have
the point as new the operating system itself is just to collect about a collection of objects and they're also
such objects like files and directories that this kind of programming is perfect
for model remodeling this explai and then the one
thing that the output is is at the operating frequency with a certain number of primitive operations which presumably are easily necessary to get
at the hardware or that one particularly has what you have to do is to be very
careful in how those are interface to the rest of the programming language so
that so that all the requirements for the
operating system permit then you finally call it and if it's a failure for instance could be closed from operating
routine an operating system routine for turning a rectangle black that requires
integer coordinates on the rectangle you better be sure that he had a just integers by the time you do that but you
don't want to reflect that requirement out into the whole programming system we want to tango spilled a floating point
coordinates fraction support so we can have to do is to check that on the way
in and use the object oriented protocol
to find out the integer coordinates pass that on to the operating system and it's that way you can get the result II woman
without having made things fun games about for the programmers I learned the
simple text which I considered and now you find out if a system is truly object oriented and if can you define your own
new kind of number for instance a fraction then you'll have to define in hell plug that great support less than
solaris but once you've done it can you use one
of your numbers in the right hand of the part of some programs record and then
tell the operating system to blacken that rectangle and have it all work and what it requires is that all of the
operations that want to get done are done by sending messages and moreover
that you can add your own new kinds of messages
and the key to this is that you need a uniform reference in other words
everything is an object and the only way you can do anything but finding method
to mount it and what the guarantees is a property which I call simulation which
is if you only have a hold of this object for that reference and you can only send admit to do then you're sort
of guaranteed somebody else will come along and put a completely different kind of object out there and everything
you've written will work because you don't know anything about it all you know is what kind of questions that can
answer constantly and people ask in
really well Victoria is programming just good for graphics the answer is no turns
out the practice is a great application product oriented programming and the reason is that's not a graphics consists
of a whole family kind of an algebra similarly behaving object for instance
there are common object or primitive ones like points and lines test commitments and then there are higher
level objects black rectangles that are more oval polygons that are made of
smaller objects and then they're really complicated or at least really high level ones such as overlays you might
have an overlay and it overlays 50 different other polygons or a window
which represents the clipped representations of some graphics these
all will obey the same message protocol and and you can put them all in a
hierarchy in there all inherit the same property so it's a demain which just
factors itself back very nicely this way it's interesting that the implications
of graphic is one where that is fully convinced sort of in press has been
called object oriented when you talk about a friend level user interfaces and I think that's just because the kind of
operations in with the screen are very much like the equations we build incredible comfort oriented parameters
there are lots of other texts for which object-oriented programming is perfected for instance building compiler if you
look at compiler construction as tasks where you're generating a tree that
corresponds to the parts of coming Linkwood six statements you can model
that tree perfectly that way you could have different no that represents an expression represents a method known
that represents dimension and the compiler simply builds those trees and then each node will have local
properties local methods for generating its own kind of code we would generate
code or something you're compiling or it can detect codes for printing back
source code if it corresponds to it you can use that to do a pretty print of some it can also have methods in it for
locating the PC and with every node in your tree as a way to locate where the
program converts isn't it then you can find their program ken burgin a large
winter and we use distant buggers you can also have other methods for printing
the structure that you compile them into another language and that way for the translator so that's another area that
to spray stands perfectly okay and there are many others get online reservation
system bank banking systems all can be factored nicely display
there's a couple of neat things to be done in the small talk system just fiber to making tainted object for instance
small hearts as an object from the context which is it's like an active
object the colors forms that frames as the language of learning and if you can
actually send messages to be best friends then you can take the prose and state of a complication filled onto by
the debugger and in perfectly high-level language we go through and single step
your program or we have temporary variables and it makes the writing of
the debugger a much simpler prophecy and in a language you can't do that one last
thing I think is worth mentioning is in a true object-oriented system if you
spend a message to an object which isn't understood then it will go through the
inheritance hierarchy prone to finding the meaning for that and ultimately it
will terminate at the end of bed tree without unique definition and that is
typically an error and was initially them into discord lease which defendants welcomes wisdom is there a way of
catching that situation and turning it around so that if you sent a message food to an object and it isn't
understood anywhere in the inheritance hierarchy then the system itself the
interpreter or whatever you prefer I turned it around and bundles of messages the name food as an object call the
message and present this to the original receivers implemented as the argument of
the message that is message not understood in other words when
everything else is failed the original effect will receive the message it said I didn't understand this
message and explain and it's actually been up in class
objects there can be code for when message is not understood it invokes a debugger so that's how you handle simple
errors of a message being sensitive but there are other more powerful things you can do for instance if you have a file
that's not open for which it wouldn't make an offense to respond to most
messages you can change it into a kind of object that doesn't understand those
messages and then when those went to differences it has a chance to discover that reopen itself changes changes come
up into a proper fun and then can be through the operation of caring for an
even more powerful use of it would be you can object in the system which are
even in your computer they might be on somebody else's computer over a communication network and if you send a
message to them they get a chance to look at the risk and see what it is and
they may actually dial opposed the telephone the dials and message to be sent over the phone response so this is
really all a manifestation of what I said the simulation property as long as you have this very tight control over
here think the answer objects and simulate all sorts of behavior
that concludes most of the major issues about object oriented programming in a cycle of a details of this moment I'm
Kristin I'm actually talking with babe younger about a ton of the questions that people
hold a nap after that nice clear explanation of object-oriented property
and I'm like just the thing to use for building complicated systems but I think
a lot of people are going to be afraid of the efficiency what do you think of
it I don't think it is a big issue but
it's a reasonable question my first thought about it is machines always can
run faster and faster and somewhere in there it makes sense to go with the language that works better in order to
take care it still needs to question ask why is it
slower how much slower the speed and basically a lot of great images that you can apply
to making message finding doable if you can use to be having to the return
floaters and other things most of the implementations a decent
implementations now run between ten and five funds and so don't see that as a
big problem people say that automatic storage management takes a long journey but it's
something like 10% and I think in your scope what's Kevin generations give you like a 90% under foot center and plug
there's another factor in there which is if you don't have it you have to have explicit code in there at least if it's
written into the language that it all happens in one possible way so I think
it's just you know the future is more efficient in the question of lending one a week a few I certainly agree yeah
some researchers in an attempt to look make things go faster origin simplified
their longings have left certain things out or even it attempt to
come up with new initiatives so for instance there are a lot of ingredients in what we talked about they're abstract
data type that requires message perhaps saying Brock's inheritance one thing he did
mention which we type declaration some of the ones that were there in small tub
which ones do you think really essential and also what would you feel about type
declarations which is one feature that's um but ok contingent I think is most
essential is miss attendant because react will give you this this interface
to ensure you can simulate and that's what all the way power so that that's
the thing that hides
I think imperative is also really important because it's inheritances
together with the polymorphism comes gives you the reusability and that's
what to make an object-oriented programming now you can I don't think the classes
are efficient we must feel the same way to do one would set the pace on
prototypes sure something in both
shelves and small talk is that everything is cooking whereas one of the
easy ropes to efficiency is where you have simple things non theater
what do you think about ok forget it you
in problem it's a basil that I gave of being able to define your own classes
numbers is an existing class for rectangles as they out for you to select the rectangle I don't think will work if
you have that convinced which numbers and rectangles that are built into the
system is primitive uptick in one group so it's not only that message passing is
essential to have it's essential to have for every
well there are other features here
except there's some connection between blocks well I'll think of bucket I
didn't say anything about blocks like frogs God where are you they're like little enzymes expression
sir where you can have two piece of code along a message what it was having an
effect or in a framework like that one exactly we have inbox to behave that way let me let you write your own programs
theorem controller structure which is very nice so you can take a piece of code it gives you a little block that
gives you the population with city and then you can take a collection city is enough to collect out the populations of
all very simple so that extends up the power of objects I like to me by letting
them even find the way control of insect
to hide it and also begin you know control structures that have appropriate to the various University okay well
what's the relationship between abstract data types
well
well I guess type declarations were
small sort of different have any particular engine no ideal there isn't
any reason that they can be type declarations I think love it but it's a different situation
conventional strongly type languages Thanks according to what I would call
concrete type and in not the three divine persons fiddle for certain type
operations but what you want to assert is without the abstract type in other words he won't look that this is an
object which understands the public protocol and then if you do that because
you obtain kind of security that people like to feel about code they've written which is you've asserted that all these
things are so therefore coaching Reisman agrees I think there's still the philosophical dispute over whether
that's all nailed in every possible leak if you have to clear the type on
obviously that's because you can have better use arresting people who like
wearing decorations
that's right but I don't keep looking any problem I actually did a type system once without onboarding it didn't turn
out but we did get a chance to use it and it felt completely natural and it
added the kind of green ability people say it it makes code more readable because you know well let's see in a
minute - we have less how about a warning people up they must be some
situations where expense these object-oriented programming but had any
interest of responsibility we should just mention what those are well I don't
think you want to take your driveways now there are certain thanks for which
it's not good honking sorry ins provisioning is a style of imperative program so analyzing
this is the best way to do paradis programming you can consider combining
rule based programming you would not use you could build a little base small
peseta group rule-based programming system in Smalltalk learning tips but the program you would do using it I
could get me close so in other words what they will do is where they need imperative statement on your logic
programs they'll use an object-oriented programming and I think that's appropriate I also think that whenever
possible to get by with just formal language
so this chart upper on the right here a lot of though the last part of that talk
was what about this feature and what about this feature and what about this feature and a kind of subtext of that
was C++ had just come out and was sort
of paraded as the big new object-oriented language of the future and they're pointing out that C++ isn't
actually object-oriented at all it doesn't have first-class procedures it
doesn't have the uniform reference that he was talking about where everything is an object and it didn't have automatic
storage allocation so our object or a system well small
talk of course is yes yes yes the object-oriented system we're using this
week obviously it has lambda it has automatic storage management it does not
have everything as an object so in our system numbers for example are just
numbers and it's only the abstract types that are objects and that whole business
about can you use a rational number in the coordinates of a point in a rectangle addresses that that if you
think of numbers as not being objects then you can't invent exact rational
numbers and have them fit in with everything so how is industry stacking up so the next improvement on C++ was
Java everything is not an object numbers
aren't the same as in our system what they do have is a parallel set of object
classes that are named after numeric types but those classes can't do arithmetic so it's like you can have
numbers that aren't objects or you can have numbers I can't do arithmetic it's a big mess a
big big big improvement in Java is that it does have automatic memory management and that eliminates a big class of bugs
and does it have lambda well it has
something called anonymous classes which got shoehorned in about the third or
fourth revision of the standard that you can kind of use those lambdas if you
really stand on your head but it's not designed in so this is sort
of where things stood as of you know
when I started giving this talk 25 years ago since then there's JavaScript a
language with a terrible name because it has nothing to do with Java and is in fact better than Java does have lambda
does have automatic storage management which is kind of mean okay you can treat
things as objects but sometimes they act funny okay and some making progress Ruby which is
another not so widely used because it's better but real world industrial
language is the yes-yes-yes and they're even talking about now
putting lambda into C++ and its latest revision so this is all good news
actually it means that good ideas do eventually
kind of filter down into industry so
we're not totally wasting our time here at the universities on the other hand
these languages are fairly hideous and
it's not just because they have bad designers that they're hideous it's
because they kind of try they're based on every good idea at once
so when your program and scheme the big organizing idea of scheme is first-class
procedures and every problem that comes up is done in a way that fits into that
framework so it has a very uniform syntax and it has a pretty simple
semantics simple not in the sense that it's intuitive necessarily but in the
sense that there aren't very many rules small talk which you saw some examples
of in this talk is very very different from scheme and it's notation and it's ideas in everything but it has the same
simplicity and small touch everything is done by sending messages to objects and
that means again a very simple set of rules and great generality in industrial
languages so far they haven't been brave enough instead what they've done is said well this is a good idea this is a good
idea this is a good idea and they try to cram them all into one eventually maybe
they'll even learn that lesson okay see you next week
UC Berkele