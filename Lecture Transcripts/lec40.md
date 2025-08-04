Transcript


Friday in lecture um all of you out in webbland should come physically and
bring a pencil because you're going to fill out a course evaluation questionnaire um that the department
uses to actually make decisions about courses and promotion and all that so it
matters and uh besides that you get a point toward your grade in this course
for doing it um an out andout bribe to get you to actually come because
um there's a there's been a historical problem about students not bothering to do evaluations and that's bad um and so
since we started giving out points people actually turn out somebody came up and said oh but I can't do it because
um the survey is being run by adap and new and if you have a problem take it up with them but try to be here um and the
other thing is I got an email about um did we notice how badly everybody did on
midterm 3 um yes we did notice um we're a few points below the
historical um average Don't Panic about it um uh my policy is not to make Point
adjustments on specific assignments but to wait until the end of the semester because usually you know something is
easy and something is hard and they all balance out um but if that isn't the case we'll do the right thing
um okay and not for administrative things what we're doing uh this week the
rest of this week is talking about two different variants of the metac circular
evaluator um and you're making a third one which is the logo interpreter um so let me actually start
by saying with respect to the final exam um you are expected to understand
but not memorize the code of the plain metac circular evaluator that we looked at earlier uh I guess last week um and
you're expected to understand uh the stuff you did for the logo interpreter
project 4 again not memorize but understand how that works um for these
variant evaluators um you are not
expected um to know about for the exam um the details of implementation I'd
like you to get the general idea and I'd like you to understand how they behave differently to a user so you know today
we're looking at the lazy evaluator a fair exam question might be um uh this
procedure here uh does it give you a different answer under the lazy evaluator than under the pl scheme
evaluator that kind of thing um but not modify the lazy evaluator so that it no
no we won't do that if we do that at all it will will be on the plain met a circular evaluator um
okay this is actually detailed in oh yeah in the course reader volume two
there's a onepage thing called exit handout um which is end of semester
information and it's time you know for you to read that not right this minute but um you know this week it's time to
read that okay so back to thinking about
streams and um one of the problems that
the book does let me skip past the integers understand
that um one of the problems the book does is to make pairs of integers so
here we have a bunch of lists of length two uh with integers and uh the
particular application the book had in mind um they don't care about the order
so they only generate uh the ones where the first number is less than or equal to the second number so there's a pair
35 but there isn't a pair 53 so it looks like this sort of diagonal picture and
the book does it this way it says const
Stream So pairs take I'm sorry pairs is a procedure that takes two arguments which are streams s& T and the idea is
we're going to say pairs integers integers okay so const
stream list Stream Car of s so that's one because we're starting with the
integers Stream Car of T so that's this little pair one one that's in a yellow box all by
itself and then inter
leave stream map Lambda X list stream carve at Xtreme
carve s is one so we're making a list one blump for all values of
blump um starting with two because of this stream cutter this stream cutter right here is why you only get half the
possible pairs um so we take one and pair it up
with everything no I take it back that's not why we get all possible pairs um it's
it's why one one isn't included in this yellow uh stripe across the top because
we have one one done separately so we don't want to do one one again we want to do one lump starting from
two so that's the second piece and then the third piece that we're interleaving
with is pairs stream C or S stream c or t that's why we only get half the
possible pairs because we could ear both of them at once so we're going to get
for the recursive call here all the pairs from 22 on
down okay now Lewis Reasoner in exercise 3.68
which I think you did comes along and says I don't get it why do we have to
have one one as a separate thing all by itself why
can't I just take the entire first row and interleave that with the
recursive call so Lewis agrees about the recursive call uh to pairs
with stream cutter stream cutter but he wants to map uh Lambda X list
Stream Car SX not on stream cutter of T but on T so he's going to get one one
one two one three all in one step okay
um and so the exercise of course asks why doesn't this work and how can we fix
it so why doesn't it
work come on somebody why doesn't it work why doesn't ls's version work
yeah inly evaluates both arguments so he should he didn't it's because he didn't have a const stream right because
constam is the thing that delays its second argument in leave doesn't um so he has to do a delay of
the recursive call in order for not to work I should have seen every hand up you guys you all did this exercise
supposedly you all should have read the solutions for this exercise um you should have all said oh yeah I remember
that but he didn't so nagnag okay so
that's um Lewis's version not working and we can fix Lewis's
version this way um instead of calling interl so
we're doing what Lewis wants to do we're only having two um chunks instead of three chunks of
this picture so the whole front row is one thing but we're calling inter leave
delayed instead of calling inter leave um and this is the same this stream map
is exactly like Lewis's version and this is almost like Lewis's version except
that there's an explicit call to delay in it okay so we're explicitly delaying the
recursive call and so we don't get into the infinite Loop problem that Lewis had
inter leave delayed down here looks just like
interleave except that it calls force on
um the delayed argument it's only S2 that's delayed
that's why the arguments are the formal parameters are S1 and delayed S2 so we
know to force delayed S2 oops not what I meant and then um const stream stream
car of S1 onto interleaf delayed of force delayed S2 And Delay stream cter
S1 so when you do inter leave you reverse the arguments S1 and S2 in the recursive call that's how you get the
enter leaving of one and then the other um so here we're using explicit called
to force and delay in order to solve Lewis's problem so now um here in chapter
four what uh they would like you to understand is that for once Lewis
actually had a good idea the thing that Lewis wrote is correct as a description
of the result that we want okay it's absolutely true that this chart consists of its first row plus the
rest of it and Lewis has an expression that does compute the first row and an
expression that does compute the rest of it and he's putting them together correctly with inter leave because he
understands that if they're both infinite you can't say append this that
so Lewis understands all that um the only thing is he's
missing something that's a restriction in the implementation of streams really it would be better if
Lewis's version did work that would be a better implementation of streams okay so that you just wouldn't
have to worry about it um there's a name for making it work
ls's way where things get delayed without you worrying about it what's it
called yeah
no there's an official name and you learned it yeah thank you normal order evaluation
right that's what it means what is normal order evaluation you don't evaluate actual argument Expressions
until you really really need them um so you pass in argument
Expressions um instead of passing in argument values except as we now know
from looking at the implementation of streams you don't just pass in the expression as a piece of text you wrap a
Lambda around it so that you remember the values of variables as they're being
used in this expression because when we get around to evaluating it those variables might not exist in the
environment that does the forcing of the delayed expression um so we actually say
Lambda open close and maybe we even memo it okay so normal order evaluation would
solve the problem um now back when we first learned about normal order
evaluation we said well you might not want to do that because if you have a
normal order evaluator and you define Square X to betimes XX and then you call
square with some big complicated expression that big complicated expression is going to end up being
evaluated twice instead of once and that's inefficient but since then we've learned about
memorization so we now know that you can do a normal order evaluator with
memorization and you do square X to be times xx and you send in an expression
and that gets um evaluated the first X that we see and
then when we come to X again we already know what the value is because um that
expression was memorized um so that eliminates the efficiency
objection to normal order evaluation um in fact sometimes normal order is more
efficient um because maybe we never get around to using some particular argument
in which case we shouldn't bother evaluating it um so if normal order is
going to turn out to be more efficient once we do memorization why doesn't everybody use normal
order when you were studying streams what was the problem that came up that
that made things a little
weird oh man
okay remember they um did some stream problems and what they put in the cter
and the thing that was delayed was um print this or or set bang this to this
plus one or that sort of thing and if those got a valuated in an order that wasn't what you were expecting things
printed out the wrong order or maybe things printed did twice or something like that remember
that okay so how did we deal with that problem at
the
time we said streams should be used
if yeah yeah if you're doing functional
programming where you're not doing anything with side effects you're not changing the value of anything you're
not printing things out all you're doing is Computing functions if you're Computing functions then it doesn't
matter what order things happen in this was also the big strength of map
reduce right that if you're Computing functions you can parallelize things very
easily that's not true once you start set banging variables as we saw
um back in chapter 3 with serialization you know parallel execute and and make
serializer and all that um so uh the actual State of Affairs in
programming languages right now is that there are some purely functional
programming languages languages that do not have anything comparable to set bang
in the language um so ml is a very wellknown examp example and hasal is another one
um that professors tend to like in purely functional languages they do use
normal order evaluation and they do it precisely so that uh you can get infinite streams and
stuff without having to think about it and your programs always work okay
scheme is an attempt at um supporting multiple programming
paradigms that's because well it's partly just because of the history of who made the language and
stuff but uh it's also because it's turning out in practice that very often the best
solution to a big programming problem is not to be purely in this Paradigm or
purely in that Paradigm um so very often there'll be whole chunks of the program that really are functional in nature and
those are best computed functionally and then there'll be other parts of the program that are for example interacting
with the user uh and those things are best done objectoriented and so on okay so scheme
tries to let you do everything because of that it does have mutation in the language and because of that it can't
just use normal order all the time because if you use normal order all
the time you get funny um effects of reordering the sequence of
events in the computation things don't mean what they look like they mean um and instead what we have is the
ability for users to Define special forms the way we defined constam using
delay so uh if you're solving a problem where normal order evaluation would be
really helpful you can arrange it um for yourself okay so what we're going to do
here is um modify the metac circular evaluator to be a normal order
evaluator and um again you wouldn't really do that
unless you took out zbank in practice but um it's interesting to do as a you know exercise
in understanding the evaluator okay
okay here's the lazy evaluator um it's actually what's in this file in library
is just um the parts that are different from the regular meta circular valuat so
it starts down at the bottom of the screen here by loading in MC Val and
then it's going to redefine certain procedures in particular it's going to
redefine eval and apply so let's look at why that is
here's eval so self evaluating expressions are
still the same it Returns the Val expression if you get a variable as an expression you just look up its value
that doesn't change if it's a quote expression you just take its cater which
is what text of quotation is um that is to say the thing that comes after the word quote um so if it's an assignment
we do a valid assignment although again that's what that's the line we would leave out if we were really defining a
functional language if it's a definition we eval definition if it's an if we eval if if it's a Lambda we make a procedure
with the parameters in the body and the current environment on the right bubble that's all the same begin that the same
con that's the same here's what's different what if it's a procedure
call well what we do in the regular metac
circular evaluator let me actually
okay so down here is the ordinary version and up on
top is the lazy version in the ordinary version what we're looking at is a
procedure call right so in real scheme what's the first step in doing a procedure
call yes yes evaluate all the sub Expressions the operator and the arguments uh and that's
what we do we MC EV Val the operator we list of values which is just essentially
map eval um for the operand and then we call MC apply with
the actual procedure that we're calling and the actual argument values now in the lazy evaluator the
thing that's highlighted on top um we call actual value
instead of MCE Val so we're still evaluating it but you'll see that what actual value does this is just a little
detail the kind of thing we're not going to ask you questions about on the final um but you should understand it anyway
if we are uniformly um turning argument
Expressions into funks into lamba open PR closed BR the expression if we're
delaying arguments all the time um suppose um suppose we have something
like
this [Music] Define a of
x to be B of X and b is another procedure that we Define so I now invoke a with some
actual argument expression we turn that into a thunk and we pass the thunk we bind X to
that thunk and then evaluate in the new environment B of X well that's a
procedure call also so we're going to turn its argument into a
thunk so now we have is a thunk of a thunk in fact we have delay of delay of
something all right and that could happen you know 20 times before we
eventually call A Primitive procedure and then we need the value so actual
value says evaluate this did the value turn out to be a thunk force it and then
evaluate that and just keep doing that forcing and evaluating forcing and evaluating until finally we get a
value okay so that's what actual value does now what about operands um in the
ordinary met a circular evaluator we call list of values which cters its way
down the list of Expressions turning it into a list of values by evaluating each expression in the current
environment here instead we just give um
apply operands X in my lecture notes I did it a
slightly different way um if it confuses you to uh see things
is done in two different ways than just go with the books version but I don't like the books version because as you
see it requires us to pass the current environment to apply as a third
argument why because apply is going to take this actual argument
expression and if we're calling it primitive it's going to evaluate it in the current environment and otherwise
it's going to delay it in the current environment so either way we actually need the current environment in EV Val
so what I prefer to do is just delay it delay all the operands in uh
eval and then we can call apply with the procedure that we're calling and a list
of thks so a list of actual argument thunks and then if what we're calling is
a primitive procedure we can go through and actual value all of those thunks if not we just pass the thunks themselves
on and we don't have to give a apply a third argument so I think it's prettier my way um but again if you this is the
book's way what you're seeing on the screen now so what's printed in the lecture now it's a little different
don't get confused okay um
good now let's see what happens in p
okay so in ordinary apply for a primitive
procedure we just call the procedure with the arguments very straightforward because
in ordinary scheme we have already actual argument values which is exactly
what the Primitive needs so it's really easy to do that up
here what we have to do is call list of art values that uh essentially is a map
actual value over the arguments okay um no it's not because
we're given argument expressions in the books version so it's um evaluate it's
basically just like eval sequence um except that it remembers all of them uh
so it it it's like um list of values list of Arc values is
basically just like list of values we take the expressions and we evaluate them in the current environment and that
gives us argument values which we give to the Primitive uh what if it's a compound
procedure well an ordinary MC Val uh in the apply procedure we have to
extend the environment by binding the formal parameters of the procedure to the
actual argument values oops lost the a there we go and then we use that to
extend procedure environment um up
here we do the almost the same thing about extend environment except instead of
arguments it's list of delayed args so up here it was list of ARG values here
it's list of delayed ARG so we're going to take the actual argument expressions and we're going to delay them all we're
going to turn them into thks okay and we're going to pass those
to the user created procedure by binding the procedures formal parameters to
these thunks that we just made rather than to values okay and then everything else is
the same it's eval sequence procedure body procedure in this extended environment right just like
that okay questions so
far okay we're about 90%
done looking at the changes in the lazy
evaluator um lazy it's called lazy because it puts off evaluating argument Expressions until it
really needs them just like lazy people um this change to
eval to not evaluate the argument expressions and the change to apply so
that it either does evaluate for a primitive or thunks for a non-primitive procedure that's the essence of the
change it's a pretty tiny change we'll see that there's a few more details but this is is the essence of it and it
makes quite a huge difference in the interpreted
language um namely things go wrong if you try to do mutation in this
language and so um it's a move in the direction of a purely functional version
of scheme um rather than this sort of everything
for everybody scheme that the real scheme is is okay tiny change in the code big
change in Behavior right so this is one of the things um I'd like you to remember in
the course this comes up by the way quite a lot whenever any company comes up with a new version of a
program right they always take out these advertisements about amazing new feature
you know now we can do such and such um and the feature may in fact be amazing
from the point of view of usability but that doesn't mean it was hard to implement so you know before you're
impressed you should think about well what did they have to do to make this happen same thing here it really is a
big difference in terms of how the user interacts with scheme if we had been using a lazy scheme from the beginning
of the course we would have had a lot of trouble in chapter three trying to do object-oriented programming and sort of
simulation of time in the world with time in the program
um but it's not much code so what else is there in the code
um so here's list of Arc values and it just Maps um actual value over the
Expressions list of delayed ARS Maps delay
it um so what else here's an example of a
special form eval if is slightly different
namely right here if needs to know the actual value of its first
argument because it's going to choose either the second argument or the third argument based on the true or falseness
of the first argument so it needs to know right now is that first argument true or false it doesn't actually need
to know that act the real values of the second or third argument if the second
or third argument is a Funk turns out to be a funk that's okay so we can just call regular old MC
of Val and if we get a funk that's fine we return a thk but for the first one we need not a thunk we need an actual value
so we call actual value
um what did I just
do that's what I do okay
so here's something a little bit different the read Val print Loop is actually a read actual value print
Loop okay
um because you can't print a funk that would sort of confuse the user once the
user asks for the value of some expression the user wants to know the actual value right so here's a play so
if and Driver Loop are a couple of places where we have to change eval to
actual value so part of the work of doing this that that ablon in testman
had to do was to go through the whole metac circular evaluator looking at calls to MC valon deciding which of them
had to be thunked and which of them had to be actual valued so now we have to actually Implement
thks um so we Implement delay and force we don't
use stk's delay and force and this is the usual problem
about metac circular um it's not an STK Funk that we want it's a metac circular evaluator
thunk the evaluator that we I'm sorry the environment that we want to save
along with this expression is the metac circular environment the one with the metac circular schemes use variables not
the one with the interpreter's own variables in SDK so uh we're redoing delay in force
and here's How We Do It
um so here let's start with delay delay it expression
environment it could just say make procedure as we know
um thks are equivalent to procedures of no arguments but they actually don't do
that they make it a separate data type so instead of list quote procedure blah blah it's list quote thk blah
blah okay so that's what a thunk looks like so now we have to have thunk question mark and selectors for thunks
and um how do we force
something well first of all we do this conservatively so uh it's possible that
someone will try forcing something that isn't a thk okay because either by mistake or
because sometimes it is sometimes it isn't whatever the situation is we somebody might call force it with a non
thunk if so we just return the argument it's not a thk it's a
value but if so we call actual value and we pull out the expression and the
environment from the thunk and um evaluate that expression in that environment
okay so that's what foret does actual value is a little
complicated and I've lost it where did it go oh
sorry no actual value
um is simple but
here's a different version of foret so the original foret was just
Funk expression value here's a new one um that does
memorization so now instead of just thunks and non- thunks there are three
kinds of things in the world thunks evaluated thunks and ordinary
thans so if something is an ordinary thing
down in the else Clause here then we just return the thing as before if it's
an evaluated thunk this is a selector for evaluated thunks it's like CER or
something and we pull out um the already computed value so we don't do any
evaluation here we just pull it out and return it if it's an ordinary thunk
then um and we're trying to force it then we compute the actual value of the
the funk expression and the funk environment call that result now we um change its type tag
from thunk to evaluated thunk we uh change its um expression
into the value so this is a little ugly we're changing the value of
something and um we turn its remembered
environment into just the empty list because we don't need it anymore the we didn't have to do that it's an
efficiency thing um if this thunk is the only reason why we're remembering some
environment then we can let STK garbage collect that environment by not remembering it
anymore um so that's the version a foret that uh has memoization so you can do it
either way with or without um you really want to do it with most cases for efficiency reasons and that's it
tada now here's actual value I missed it before it's in between eval and
apply um actual value says evaluate the thing and then call force it so if
evaluating the thing if the thing is you know a number or a variable name or something then evaluating it just gives
its value and force it won't do anything it'll just return its argument but if it so happens that MC Val returns a
thunk um because it's the value of the formal parameter to some user procedure
let's say then force it will force that and force it calls eval again so if you
go look at force it um it calls actual value actual value Calles force it the
so it's a mutual recursion kind of the base case of it is when we get to something that isn't a thunk then force
it doesn't have to call actual value anymore and it just returns that
thing okay so those are a few more details about exactly how making a
delayed object works you have to understand that and there are a couple of places in the evaluator that aren't
obvious like in the special forms and in the reppel uh that you have to worry about do I need to know the actual value
of this thing right now in which case you call actual value but the essence of the change is a
little bit of a change to eval just for the case of procedure calls and a little bit of a change to apply to handle the
fact that uh we're given Expressions instead of values questions
okay
um all right that's really it for this evaluator I think it's worth your while even though we're not going to ask you
questions about it on the final it's worth your while going through um more
slowly in the book exactly how uh making a thunk and using a thunk are done um
because when you look at it in detail um you're very likely going to have some
confusion about the distinction between metac circular Ste scheme and STK scheme
um and it's good for to actually work that through and note by the way an important thing about this is doing this
doesn't change STK right STK is an applicative order scheme so we can use
an applicative order scheme to implement a normal order scheme we could do it the other way too if what we were given was
a normal order scheme we could invent an applicative order scheme if we wanted to
okay so that's important um all of these languages are equivalent in the sense
that you can compute anything in any of them it's just a question of what's easiest to do for a user and what's
harder to do for the user so functional programming it's easier with normal order evaluation because you don't get
into trouble the way Lewis did um and the book does also if you remember in
the book and when they were looking at streams maybe you skipped it over with glazed eyes but there was an example
about um a numeric solution of some differential equation for some electon
Ric circuit and they got in trouble where they had to explicitly delay something so when you're doing
complicated things with streams that are built on top of applicative order you do run into these problems it's not only
Lewis has trou troubles like that um so normal order evaluation would fix that
but at the cost of losing a clear model for how mutation works okay um I will see you Friday and
you're going to bring a pencil
UC Berkeley 