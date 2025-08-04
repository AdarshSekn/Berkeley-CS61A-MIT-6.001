Transcript


right hi everyone so as you can see I'm still not Brian um he's going to be back
on Monday so today we're going to continue with the stuff that we did on Wednesday of talking about how we can
use this new environment model that looks like this funny diagram here to
create what we've been going for all along which is that diagram way over on my left there you're right of having our
global environment and then classes and then inside those instances and this way
we can get object oriented programming to just come very naturally out of this environment diagram so the high level
idea for today is looking at that thing over there watching what I do to this
diagram and then seeing at the end of the day that they're going to end up being the same thing that's what you
guys should be watching for so what I have up on the screen here is something that you guys I think left
off with last time which is a definition of make count and this is a you know a pretty
good version of make count because we in say we can go ahead and Define C1 to be
make count and it will count up and it counts both numbers at once and then if
we make a second counter then you'll see that each of
these things in the list one of them is a local variable and the other is a
global variable and what we mean by those this lock thing is basically like an instance variable of the counter
because C1 and C2 have different instance variables and the one that's called glob for
Global is like a class variable of a counter because the two of them share that but if I just type glob here well
it gives me this primitive procedure that we don't bother using in this class it doesn't give you this number that is
very clearly counting up when I say C1 or C2 so what we want to do is see just how
that up there translates into an environment diagram down here so I'm just going to go very step by step with
each of these things we did so let's just start with what's over here on the left um which is this this definition
here so with this definition oh wonderful okay at this
definition the very first thing we're doing is a let so when we do a Define
we're not going to do anything special this is not a defined with parentheses there's no implicit land all we're doing
is just taking the value of this let and binding it with the name make
count and what we have to do for this is just like if we said define count plus 2
three we're going to add two and three and bind count to five so here we're
binding make count to let something something something so whatever the
result is from the let is what we're going to do at any point during this please wave
your hands wildly if something didn't make sense or maybe just one arm so you don't hit
someone so I'm going to go ahead and use white to represent what we're doing here and white will be our first step Define
make count let blank so while the Define does not have
an implicit Lambda a let does so this let here which board should I
use this let is really something like like open parenthesis and then inside
it there's this inside
Lambda that has glob in it and that has
somebody and then we're going to call that Lambda with
zero so this is just a normal scheme procedure call for every procedure call what do we do first evaluate the sub
expression well zero is easy that's just zero but
this Lambda is a procedure and our first rule about environment diagrams says whenever we see a Lambda we have to make
a new procedure in the environment diagram so let's go ahead and do that by
drawing in our procedure the parameters is
glob and the body is a Lambda of no arguments and it has
content where does the right oh yeah yeah I'll try this example uses up
multiple boards so okay but yeah um okay so we have this here where does
the right bubble point it points to the current environment where the procedure is being
defined where are we defining this procedure well we typed it in at the top
level scheme prompt in our file so it's in the global environment since there's
only one environment up here that should have been a good
guess now we've created our procedure for the let but we don't just create a
procedure we have to actually call it so a let is a Lambda plus a procedure call
and you guys should have seen that on midterm one so let's go ahead and call this let procedure by making a new
frame and I'm going to call this the glob
frame just because it's where we're going to store the value of glob so glob has the value
zero where's the parent frame where's the parent environment for this
Frame well we're calling this procedure
so we follow Its Right bubble and find out that the parent is the global
environment now that we've set up our environment we evaluate the body of the lead which is inside there just this
Lambda of empty do something well a Lambda is create a new
procedure so we're going to go ahead and draw another new procedure here
this time the parameters are empty but the body is another
Le where does the right bubble point we have two choices now it could be the G the global environment or the glob
environment so who thinks it's the global environment who thinks it's the glob
environment all right most of you guys are right and most of you guys are raising your hands which I really like um not too many extensions so it is the
glob environment indeed because where are we when we're defining this second
procedure we're inside the let because we're inside the let the glob environment is the current environment
and this here is going to point to
it yay I should turn off my sleep timer all right all right I'm just going
to come back and keep hitting shift every now and then so okay we did a let and let had a body
and we evaluated the body and got a procedure do we call that
procedure no if the procedure here was you know parameters was X and the body
was time x x we couldn't possibly evaluate it because we don't have a value for x yet so there's no way that
we could evaluate this procedure if it had a parameter and scheme doesn't make special cases so that's the sort of thing you have to
remember if you create a Lambda it doesn't call it right away and again
this is not anything new this is something that you've used all the way back to you know the second week of
class when you guys learned what Lambda was so here we're not going to call this procedure we're just going to return it
and so now we're done with the let and we can go ahead and add make count to our global environment
and make count is this procedure we're good so far
right okay so the next thing that I went ahead and did is this this line over here on
the right I don't actually know how to do Brian's highlight thing so I'm just going to take it again here um this line
is where we first called make count and we do it to you know make a new counter in our objectoriented world this would
be instantiate counter with no inst with no instantiation variables but for now
it's just a call to a procedure make count so I'm going to go ahead and do this one in blue chalk uh blue doesn't
show for at all I'll do it in red chalk so this is going to be Define C1 as call make
count sorry for running over the plus procedure okay we're doing a procedure
call so what do I have to do make a new frame
good so here's a new frame um we'll call it MC1 for the first
call to make count and is anything in MC1 no make
count doesn't take any parameters it's just this procedure here so nothing's going to be in the frame we have an
empty frame now you might say why do we even bother having an empty frame and one reason is again scheme doesn't
do special cases if you have a procedure then you put all of its arguments into a
new frame even if there are zero of all of its arguments the other reason which
you might find a little more practical is that if I then inside of this Frame I said define then it would add a new
binding to this Frame just like a Define added make count to the global
environment so we have a new frame and we're using it for this procedure
here so where's the parent environment is it the global environment or is it
the glob environment glob right good job
guys so again we're calling this procedure we follow the right bubble and we get this environment so the very
mechanical part of your brain says look at the procedure follow the right bubble okay that's the that's the frame I want
to extend the thinking part of your brain says well somewhere inside of this procedure here
we're going to actually need to set glob to something so when I make this new
frame I had better have access to the environment in which glob was defined so
that's also really important so in this way the thinking analytical side of your brain should be understanding what the
mechanical side of your brain is doing now we have this MC1 frame here
with nothing in it and we can go ahead and evaluate the body in this new environment so our current environment
is now MC1 what's the body well it's another let and just like that one we have a let
being a
Lambda whose parameters is local and I'm not going to write the body because you guys can see it up there and whose
current environment is MC1 then because it's a let we
immediately invoke that Lambda with our argument of zero so I can go ahead and
make another new frame and this is going to be the Lo one
frame this says L one and again it's going to
extend this Frame this environment because we were calling this
procedure what going to be in the frame a binding for Lo just like we had the binding for glob back here so I can
write Lo is
zero I want to make a quick note sometimes you'll see me or Brian or the other t write some values inside a frame
sometimes they'll write the values outside of frame for today just so you guys don't get confused on what's a
variable and what's a value I'm going to write all of the values outside of frames and all of the variables inside
frames the book keeps things a little more compact by putting the numbers inside the frame as well so don't get
confused about that things on the left side of an arrow a word on the left side of an arrow is a variable anything on
the right side of an arrow is a value the only thing where that doesn't hold is environments because you know
you can't ask for an environment in STK it just does not give you one
all right so we've done our let what was the body of the let well it's another
Lambda so I can go ahead and make another procedure in this current
environment which has no parameters and its body starts with a
set bang and then it has more stuff after that
do I call this procedure no just like last time we do the let we get the body the body is a
Lambda expression so we get the value of the Lambda expression which is a procedure so this is the value that's
returned by make count which means that this thing
here is C1 that's our counter this procedure
here so now now I can go ahead and call C1 and I'm going to do this one in
green and this is where it's going to start spilling onto the next board so first off this is a procedure
call which procedure am I calling C1 in the global
environment this one so that means that my new frame
is going to extend this
Frame because I'm calling this
procedure what's going to be in the frame
nothing because there are no arguments to this called a C1 I guess I should
call this like C1 a so we can call it multiple times
here we create a new environment now we can evaluate the body so let's go ahead
and evaluate the body here we have a set bang which works just like a Define so
the first thing you have to do is find the value of the set bang well the value
is plus uh plus L first or glob first Lo
plus Lo one so first thing we do is say okay
what's plus I don't know I don't know I don't
know I don't know oh it's this primitive addition procedure from way back here so
okay now we know what plus is what's L I don't know it's
zero What's one well that's just one we don't need to look in the environment for that so now we have addition 01 we
get one and now we say set bang Lo one well
what's Lo it's this Lo so let's go ahead and cross off at zero and write a
one now we do the same thing again but for a glob instead of L so again we go
through everything we find addition we start here again we go through everything we find glob it's zero we add
zero and one we find glob again and change Globs zero to
1 finally we do a list primitive list
procedure of L one and
glob one to get our answer of one one you
probably could have done all this without the environment diagram here's where it starts getting
interesting I'm going to call C1
again and when I call C1 a second time you know I should get two to what's
going to happen in the diagram well everything that I just did in green is going to get copied again so I get
another C1 here which I'm going to call c1b and c1b also extends this
Frame and you can see this is how the referring refering to the same location even though I called the procedure twice
they're referring to the same local so this becomes two and of course the global one also becomes two and our
result is 2 two all right so before I go on any questions up to this
point
yeah why does make count point to this procedure um so way back when we created
it um um the very beginning of make count was make count and then a let so
the let created this procedure which doesn't have a name and then we called that procedure
to get this new glob environment and the glob frame starts out with glob going to
zero and the body of the let was a Lambda expression that Lambda expression
had no arguments so we just made a new procedure here with no arguments and the
body being whatever and then that was the entire let and so that was what we returned
back to Define then Define added make count to the global environment and set it to
that value returned by the
Le
yeah yeah that's actually interesting um no the output of a procceed procedure never actually appears in the
environment diagram why mostly because real computers also don't put the output
of a procedure in memory they pass it sort of in like a scratch space which is called registers you'll learn more about
how all that stuff works in 61c but basically the idea is you don't need to actually put that in the diagram however
if you want to keep track of it on the side sometimes it's helpful to keep track of things in a list of saying okay
what is my current environment well it's G and then I call C1 a a and then c1a
gave me an answer which was 22 and now I'm back up to G so I can just print out
that answer so if you want to have this sort of thing for your own benefit
cool also not actually in the diagram these dotted lines they're helpful but
they're not actually stored in the computer anywhere of saying which procedure you called to make a
frame and similarly these names are also not in the computer because the computer doesn't care what the envir IR is named
they're just for us to be able to refer to them
yay all right any more questions
yeah okay so yeah so what would happen if we took away the empty Lambda call between the two lets well it's not it's
empty as in there are no parameters but it's not empty as in it does nothing so remember that empty Lambda was this that
empty Lambda made this procedure which is mate count so if we didn't have that
Lambda there instead of having a procedure that returned counters we would just immediately create a new
counter so we would get this this and this and then this would be our return
value and then we'd only have one counter and we we we would be back to where we were on Monday where we knew
how to hide information but we didn't know how to make like a factory of counters which is what we're working up
towards you don't need to take my word for this you can go ahead go back to the lab and try all these things because
again STK doesn't make special cases it'll just do what you tell it to do so a lot of these things that are questions
about environment diagrams I encourage you to just go and try them
okay good all right let's move on to the trippy part
so I'm going to define a new counter here which was
C2 so remember when I did the second call to C1 I said that I was going to redo everything in green a second time
and I did below the other one so similarly when I do this new call to make count it means I'm going to have to
redo everything I did in this sort of brick red color which means I'm calling
this procedure this is the make count procedure which means I need another new frame
here mc2 which also is going to
extend this glob environment we're calling this procedure so we're
extending this environment then the body of this proced of the make count procedure is a let and
and so that let requires another new
procedure whose body is this but or sorry whose parent environment is this
and whose body is actually shared with this
one so you can see these are two procedures that come from the same Lambda but because they have different
environments they're different procedures when you guys actually draw environment diagrams you don't need to
to show that these two actually share their parameters in body it's okay if you just copy it again but I'm doing it
here just to emphasize this point they have the same Lambda but they're not the same procedure because they're in
different environments and that's important so we go ahead and call this
procedure which is the one for the let get another new frame here which is L
2 and in this one we have a new Lo that's still at
zero and finally we said we're going to go ahead and make another Lambda of no
arguments which is again shared down
here with this sorry with this Lambda but it's in this
environment we don't evaluate the Lambda because it's not a let we just return it
and call that C2 and here I'm just going to make a total mess of the
diagram okay I'm G to give you guys a few moments to stare at
this yeah
you mean this do you mean this or the dotted line yes so yeah in in real life in an
actual practical sense you would just rewrite the body but for today I'm going to show this just to show that the
scheme compiler is allowed to let it be the same Lambda same parameters in body but different
environment so SDK is probably smart enough to figure out that it can save memory by doing that
yeah ah good point um so the question was if you didn't hear after we call C1
each time we don't really need these frames anymore because there's nothing in them and more importantly nothing
points to them so for the purposes of a test yes you need to draw them and they
need to stay there for the purposes of the computer scheme promises that it
will not erase anything from memory but there's a footnote if it can
prove that you can't tell whether it erased it or not then it will go ahead and erase
it so the way it does that is basically it starts in the global environment and it looks at all the arrows and it says
is there any arrow that points this envir en and if it ever figures out no then it's allowed to go ahead and reuse
this for other stuff in your computer um all of that actually doing
that is pretty complicated that's the basic
idea um by the way that is what uh Alan K was talking about when he said real
real programming languages have automatic memory management he's saying that in a real programming language you
can have not just frame but also procedures like these let procedures that don't have names and you can go
ahead and Define things and not have to worry about saying and then I want to delete it later in a real programming
language you should be able to just Define something and then the programming language environment will
take care of cleaning it up for you so definitely good
question all right let's do the last bit of this is
this actually yellow no this is dirty white
oh there's no actually yellow chalk huh darn it okay so I'm going to do this
huh I think it just looks yellow and it's actually just really messy white
yeah okay I'm just going to do this in messy yellow white then um so the last
thing we're going to do is go ahead and call C2 that's completely White
okay we're going to go ahead and call C2 and it's going to look like when we called c a lot like when we called C1 so
first off what procedure are we calling give me a color the blue one um and it's
going to be this blue one because it has a name which is C2 so we go ahead and make a new
frame this procedure's right bubble is this environment
so we'll go ahead and make this new frame point to that I'm taller than Brian so I can get
away with this and we'll call it the c2a
frame again there are no arguments we're just calling C2 but if there were arguments they'd go in here now we can
evaluate the body of C2 so the first thing we say is set bang Lo plus Lo one
and so we go ahead and we say what's plus no no
no no oh plus is primitive addition we go through the same search every time
why because someone could change the value of plus but please don't okay next one is up what's l no oh
lo is zero Lo isn't two Lo is zero that's
important what's one one that's not important so we say plus 01 we get one
and we go ahead and say okay change L which Lo no
yes now this Lo is one now we go ahead and set Globe no no
no here it is same thing as before cross off the two we get three
and our result this time is 13 which is exactly what I have over here on the right when we actually do that except
that I called C1 one extra time so it's
14 this is hard to read right I want you guys to squint your
eyes and let things blur into colors and then follow me over to the
right hand board
do you guys see what I did there everything that we did over here
in white the first time we used white was creating the class A a sort of counter class yeah then we went ahead
and made a first instance of that class which was in this orange red color then we went ahead and called Methods on that
class in green on the instance sorry in green then we went ahead again and made
another instance in blue and finally we went back to White and called one more method on
it so we've basically worked our way most of the way into the local state
part of object-oriented programming that's really cool we without you know doing anything
else we invented objectoriented programming
yeah yeah very good uh so you said would it would glob be a class variable and
local be an instance variable exactly
yeah yes I completely switched my methods thank you
good call this is important we just did this
to do local state what were our other parts of object-oriented program besides local state message passing and
inheritance so let's see if we can take this and add message passing to it
why would we want message passing well right now when we say when we call
account or whatever we always add one to Lo and
Globe but maybe we want to handle those separately so let's go ahead and load up a different version of this
file here's a message passing version so we still have this outmost let with the
globe and then we have a Lambda of no arguments so make count is still just a perceived of no arguments that returns a
counter nothing changed there then we have let Lo be zero and
that's sort of our instance bars and then we have this Lambda
message this is something that you guys saw before in the context of just plain straight message passing and it's the
sort of thing we wanted you guys to do for make array on the midterm we have these three con Clauses
where so that this class basically has two methods a local method and a global
method and the local method will increment Lo and the global method will increment glob and we're good both of
these methods do exactly what you think they do how does this change the diagram I'm
not going to actually do it don't worry that diagram I'm just going to leave as it is but basically you would have
something else in here in this green thing because because before we know
which procedure to call of the two options between local and Global we have
a dispatch procedure which is a procedure that takes a message and
Returns the implementation so let's go ahead and add that up here for our
objectoriented terms dispatch
again means
a message and it goes to a procedure which is the
implementation and that's exactly what you guys see up there equal message local return a
procedure equal message Global return a procedure else no such method
message so how do we actually use this one well let's go ahead and load this new
version of count and now we can redefine
C1 uh ignore that and now we can say something like
C1 local C1
local C1 Global they're separate they behave as
we expect them to similarly find c C2 make
count and then C2 local
C2 or C1 local again and we'll see you know of course they are proper local
variables they don't step on each other's toes but C2 Global is an actual proper class variable and they share
it so here now we've added local state and we've combined it with message passing
who's confused about the double parentheses just thumbs down so thumbs up I get the double parentheses they
makees sense thumbs down not so much
okay how about who understands them if you understand them but think that it's
kind of silly then put your thumb sideways okay not so many people so
either you don't get it or you understand why um so let's fix both of these so this is just something
saying call C1 with the message local and then call the result of that
so remember I just said A dispatch procedure takes a message and returns a
procedure it Returns the implementation of that method so that means that when we call
C1 with the word local what we get back is not you know in add one and then do
something it's it's a procedure that adds one to local and then returns local
so that's why we have two parentheses there and you might think that this is silly now but it turns out it's very
useful if your procedure has arguments so let's go ahead and add some a new feature to this class here where
we can say is the message set
bang actually let's use something a little nicer let's say set local Bang and if the message is set local
bang then it takes a single argument new and sets the local to
new so now if we load up our counter and
redefine all of this now if we say C1 local we still we get our procedure this
is our implementation method if we call the method we get our usual
results but now we can go ahead and say C1 set local bang
five and it doesn't work because I said local instead of
Lo there and now if I say C1 local I get
six again this should not be so something so amazing because all I did was just add a method and you guys have
been able to do that for a week and a half now um hopefully you guys have been able to do that on your project 3 but
here's a new method and it takes an argument and so we have this here now as a way to pass arguments
along with that if you still think this looks ugly here's how to make it nicer
does that look familiar now you know how ask
works so I'm this was in your lab but I'm going to go ahead and write it here
again just because it's cool here's ask
Define ask object me
message do args and remember this is the syntax from your homework on even parody
of saying zero or more extra arguments so if I get zero arguments then ARS will
be an empty list if I get five extra arguments then they'll all be put into a list called args and all its
implementation is is OB message and then
call that on args
yeah yes thank you Brian made the same mistake last
year apply so remember OBS message is going
to return a procedure like the procedure inside that's returned by set local
bang and that procedure takes a list of arguments or it takes a single argument
so apply we'll then apply this procedure to our list of arguments which hopefully
is just one argument and if the method takes no arguments then this ARS will be an empty
list good catch thank
you all right so are we good so
far okay so these last few minutes I'm not going to fully do this so this is
not quite how ob. scum works but it's basically the idea for your reading this
week you're supposed to look in the volume two reader um mine's pink yours isn't um but in the very like beginning
section of the book there's first there's a section describing how to use object-oriented programming and then
after that it says how everything works which is actually really useful and at the very end of it it says it has
something called show class which shows the implementation of an object-oriented
class you guys did with Define class and that's exactly what you have in your project where on one of the questions
you have the thing class written using only Define and let and Lambda and your
goal is to turn that back into a defined class that behaves the same way hopefully you guys have at least seen
that problem now you have all the tools to do it so are there any questions
yeah why don't I have an apply up there sorry when I have the why do I use
the double parentheses instead of
apply yeah um so in this case it's because args is a list of arguments and
so we want to apply this procedure to this list of arguments but up there I'm not giving it a list of arguments I'm
just giving it the arguments like in
line
yeah yeah yeah it's still doesn't work because it's a list
okay all right so in these last five minutes of class I'm going to give you a
very high level explanation of inheritance and that's our last remember that's our last piece of object-oriented
programming today we saw environments give you local state by turning this
complicated thing here into those into the nice thing over there mapped with
the colors we also saw that we can just put message passing into this just like we
did before we even learned about objectoriented programming and it'll just work the way we expect and if we do it this way we get some pretty nice
properties so let's go ahead and actually
um Define a subass of count so I'm going to
say Define not Define class
make buzzer and this is that same old buzz game where if it says if it gets to a seven then it'll say Buzz instead of
the number so buzzer has no Global variables
like this so we can sort of skip over this let or we could do an empty let but let's just skip over it and just say
make buzzer is a procedure of no arguments oh yeah a procedure of no arguments that's going to return a new
buzzer well what is a buzzer it doesn't have any instance
variables but it does have a parent so we can say let parent be make
count if the counter is a parent inside the let then it'll be accessible just
like an instance variable now we can go ahead and write our dispatch procedure which is Lambda
of message and the important thing here is that the object of the the counter or
in this case the buzzer is going to be represented by its dispatch
procedure I'm going to say that again an object is represented by its dispatch
procedure that's why in scheme if you type in an object something that points
to an object like in your projects if you type in BH you get a procedure back that's the dispatch procedure for that
object so here what I'm defining is the dispatch procedure but it's also the object so let's go ahead and say
cond is the message local well in that case first I want to
call the parents local
sorry Lambda of no arguments because local is a
method first call the parents local and I'm going to do it without
ask let result be parent
local then if
equal remainder result seven zero if it's a multiple of seven
say Buzz otherwise just go ahead and return the result like the parent would have okay that's
local now let's go go ahead and handle the other cases but I don't really want to rewrite Global and even worse I can't
rewrite Global because I don't have access to the counter's global variable I didn't even have access to counter's
local variable I had to say parent local to get that to work so instead I'm just going to say if I get any other
messages then let's just go ahead and ask the parent what to do about it and
this is where it's really valuable that A dispatch procedure doesn't do the operation but instead returns a
procedure that will do it for me so here I can say else parent message and that
means if the message is global then I will get back the parents implementation of global If the message is set is set
local bang I'll will get back to parents implementation of set local bang so let's go ahead and load
this and now I can define a buzzer
and all right let's ask this buzzer to count one two three four five six
Buzz eight it works and more I can ask the buzzer to do cool things like set
your local to be 13 or 12 and now if I ask the buzzer local
again it's 13 Buzz 15 it works I didn't have to
rewrite the parents' methods and that's exactly what inheritance is all about all right Brian I'll be back on Monday
see you guys then
UC Berkeley