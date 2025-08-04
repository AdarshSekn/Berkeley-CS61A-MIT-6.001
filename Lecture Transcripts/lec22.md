Transcript


okay so I guess let's get started it's about 210 so as you might have noticed
drawings not here today I'm Eric one of the TAS will be lecturing today in place
with him and then Darren will come in in a bit so um a couple announcements recall midterm two tonight hopefully all
of you know from 7:00 to 9:00 p.m. 20:50 vlsb same place as last time so
remember if there's no group portion for this midterm so you don't have to like coordinate with your groups before the exam
okay so recall that last lecture Brian left off talking about the environment
model of evaluation which we're covering today and I find if we're going to learn
something called the environment model we might as well define what environment is so so an environment is just two
things um one a frame and a frame is a frame
just um it basically is a binding from symbols to values so it's just like a
variable list
so we could represent this as let's say we had a variable foo and a variable X
defined in our current environment we could show this as like food mapping -
let's say it has value 42 and then on the variable X let's say it has value 2
so this is what the frame would kind of look like high level foo maps to 42 X
maps to 2 and then in addition to the frame an environment consists of
so it also contains a pointer to like an enclosing environment also like a
parents environment we'll get into what exactly this is a bit later but just
remember these two facts about what environment are okay so let's talk about
um it's actually kind of helpful to think about the environment model
um related to the substitution model so it's kind of remarkable how similar the
two are
okay
so in the substitution model so when we're doing a procedure invocation we're
called out in the substitution model we first have to evaluate all the sub expressions so it's like evaluate the
operator and evaluate the arguments
and as Brian said this is still true in the environment model so after we
evaluate the sub expressions the next step we want to do is um we want to apply the procedure to the arguments and
this is still true in the environment model so far everything is exactly the
thing but the way they differ is right here the way the substitution model applies a function to an argument is we
call that kind of nasty function called substitute where we substitute all
formal all like formal parameters with its given value so substitute how do you
say our values for the formal parameter
weight the modified body with all the formal parameters substituted in for values that we've given it though
modified Oddie great so this hopefully
looks familiar this is what team one did so now we're learning about this new guy
and now when we apply procedure and when we apply procedure two arguments we're
going to do something else
so we're going to make a new environment and have the formal parameters of the procedure bound to the values we give it
okay and then the next step we do is so
now we evaluate the body of the procedure but within this new environment we just created and I'm
running out of room sorry
so to compare contrasted to let's go through an example using a substitution
model let's say we're evaluating this
end of X and I don't know let's just add to it plus 1x and we invoke it with an
argument for substitution model says evaluate our ya substitution model says
evaluate see all the sub expressions this is a lambda so it's self evaluating in t1 a number is also self evaluating
so it valuates to 4 then um we call a substitute for into every instance of X
in the body so we end up doing plus 1/4
which yields 5 nothing crazy here but things start to break down when we have
something that looks like this
let's say I have this procedure foo that just set things it's given parameter
right in increments of by one if we try to evaluate this call foo of four in the
substitution model something funny happens because we'll do exactly what we
did before just substitute for in for every instance of N and then we get
something weird we got set bang for to be plus one for this is kind of strange
and this is why the substitution model is no longer sufficient for our needs in
this class it fails at trying to do stepping so yes but then let's contrast
this with what the environment model does now if we invoke foo for so bear
with me I'm creating first the global environment will define this in a bit but just think
of this as the environment that um you're using when you're typing at the SDK interpreter when we invoke foo we
create a new environment just like this says I'll call it e 1 and then we bind
the formal parameters to the arguments we give it what are the formal parameters of su well it's n so we write an N and what
value did we give n we give it four three right four and then we say okay
now evaluate the body of the procedure relative to this new environment so
stepping n plus one n so we find an N and we
incremented by one alright we did the right thing cool but notice that this is
kind of suggesting that all evaluations are done with respect to some awesome environment and this is always the case
in the environment model evaluation you're always evaluating something relative to some environment it doesn't
make sense to try to eval something without giving an environment so as
brian says you can't eval in a vacuum you have to do it in some environment so
let's start up a list of facts
okay so I've kind of used this thing
called the global environment so let's kind of formally define it right now so
the question is what is this global environment and part of answering this question is asking what should be inside
the global environment so when you think of like when you're using the terminal
like on the lab machines and you're just kind of typing away at scheme what kind
of things do you expect to be inside the environment already
yeah I heard primitives and that's great um so stuff like plus actually this is too
small so you notice on day one that you
could ready use stuff like plus or times or first or rest or coder or car actually not coder car first and rest so
in reality you can think if you'd like that the global environment has all these stuff plus maps to recall that
this is what procedure looks like an SDK so we have a binding from plus the simple plus to a procedure we have
multiplication already bound to its own
procedure we have first down to its own
procedure not really writing and so on and so forth for every single primitive
that you can think of an SDK you can imagine that writing all these can be
really tedious if you have to do it each time so you can omit these when you're drawing your own environment diagrams
but conceptually realize that these are there so just implicit because they're
built-in primitives to the SDK so right
so as I said before the global environment it's pre-installed with all these derivatives primitives so if all
evaluations are done in some environment that implies eval like the the function
header now looks something like this takes an expression and environment in
which to evaluate the expression in any
questions so far right move on okay
so we've just defined what environments are so far now we have to ask when our
environments actually created it turns out we only create a new environment
whenever we invoke a new function so so
create a new environment one you VOC a
procedure and in this class after seven odd weeks whenever you think a procedure
or function you think goes yeah lambda so naturally let's proceed to how
lambdas are treated can I erase just
like you just
okay so the next part it's going to sound a little weird at first but just kind of bear with me it'll make sense
why I'm doing this so in this new model we're going to represent a lambda as
these two bubbles okay so say I defined
a lambda in the global environment called su so if I wanted to draw the
environment at this point we have a new
symbol foo that's balance of something
foxes too big now and this thing is a
lambda and in the environment model a lambda evaluates to this funny-looking thing
these two bubbles where the left bubble represents the actual lambda expression so it contains the parameters here's
just X and the body which is multiply X
by X and then this right bubble it these
lambdas are going to remember where they were born like where they were created in so because this lambda was created in
the global environment this right bubble will point to the global environment why
we did this will be clear in about 10 minutes but anyways so let's say we
actually invoke foo now we say foo of for a nice number let's refer back to
these rules so remember when the environment is function call we're going
to evaluate the sub expressions easy then we apply to proceed to the arguments and that involves we create a
new we create a new environment and
we're binding the form parameter X to the value we passed in which is 4 and
then we can evaluate x times X within
this environment which yields as expected 16 so that was a fairly like
procedural process you guys will all learn how to do yes question
you can think of it in you're right I forgot to drive this arrow to points to this lambda yeah oh yeah oh yeah oh I'm
right here yeah Oh
could you repeat that question
not quite it's rather it's not that this environment is like contained in here
it's rather that this expression is being evaluated within this environment
yes and here that's what it would try to do in the substitution model but this is the evaluation the environment model
where we created this new environment we set N to 4 and then we just say a set
bang n to be plus 1 n so following just the regular stuff you know we say set
bang it's n to be 1 plus 4 is 5 so yeah
you know so back here so some of you
might have noticed a slight problem remember that I said all the parameters were only defined in the global environment I did not say that when we
create a new environment that they're kind of copied over so right now this environment if I try to evaluate x XX we
do find an X binding but we don't find a multiplication binding so then the
question is this is a problematic we don't want an unbound variable x when it's clearly defined the global so what
we intend is we want everything that's visible in the global environment to be also usable in any environments we
create so how do we show this
relationship in these diagrams remember when I define an environment I said
environments two things one it's a frame that binds variables to values or a symbol to values and two it's that
pointer that points to another environment right now I have the frame you know X is down to four but I don't
have that pointer yet and I'm going to show that relationship I'm going to draw this pointer to represent that this
environment is enclosed by this environment so what this means now is
when I do variable lookups we do the following
I'm trying to find the symbol times I don't find it in my current environment I asked my parent environment to see if
my parent has that variable so here no x so I look in the global environment and yup there's a x in here so we returned
it and we know how to do multiplication in the child environment right so
actually I should probably write down those rules if I have another board
okay so if I'm trying to find the variable look up the value of variable food the first thing I do is I look in
my current environment if I find it like
here trivially l-n is ready in the environment great I can recur it and I'm done is found return it but if I don't
find it in the current environment then it's not you know all hope is lost I just look at the parent environment
okay so it's it's exactly what like
you've kind of intuitively known if you don't find a variable in your current scope in like a procedure body you like
you've known that you can look in the global environment also but what happens
so like you can imagine you can have also change environments together linked but um if I'm trying to find a variable
at the end of the chain what happens if it goes all the way to the global
environment but it doesn't find it in the global environment what should it do
yeah it should it should throw an unbound variable error because if it didn't find it in even the global
environment that means it's just not visible so we say if
so we only reach this third case if we've reached the parent the global
environment we don't find the variable then we throw unbound variable error so
the final question we want to ask is I didn't really justify why I had a
one-point to the global here it's kind of obvious it has to point to the global
because it's the only other choice but you can imagine a more complicated scenario where we have no
okay so say I have these procedures defined through a procedure foo and bar
and then name to find their global scope and then I call foo with argument Daren
well we're going to draw the global environment as always where we have
named this chalk is named down to Eric
we have foo and bar and foo is this
lambda that takes in a name right yes
and it's body is to call bar with argh or name
so two points to this lambda and then bar is going to point to this lambda
this is the one that has an Arg and I'll spare the body just remembers that came
from here so understand why these lambdas point to the global environment it's because they were created in the
global environment kind of like I just typed them at the terminal okay so I say
food Erin we're doing a procedure call so we create a new environment with a
formal parameter name down to whatever we pass in this case it's Darren and
we'll just say at this points to the global environment at the moment but
then we're going to call a bar while we're inside this environment I'll write it here
so I'll call this new environment e - it's the environment created by invoking bar here Arg is also Darren so then
here's a big question the body of this e 2 is set bang named to be argh
which environment do I have e to extend do I extend the global environment or to
extend ee1 yeah I heard an e 1 but you
um so this brings up kind of a design choice um there's two real this really
two cases for deciding which in very
environment you need to UM like I extend
so so one way you can do it is you can
have your language always extend the [Music]
I always extend the Landers environment so in this case we would have um II to
extend naughty one but the global because this environment is associated
with this lambda in this lambda says I was born in global so if I did that then
um we kind of we will do this we will say set big name to be argh we try to
find name within the current environment and we don't find it following those rules up there we go to the global the
parent environment we find name in the global we set thing Eric to be Daren
great this is exactly like this shouldn't be any surprise because this is what scheme does socks I'll write
that down
and this happens to be called lexical scoping and i'ma look I guess I'm a
little biased but I like to think that this is the same way of doing things you'll see that trying to do it the
other way leads to code that's just kind of crazy to follow but it is there so
let's talk about it let's consider the other option what if we always extended
the current environment well this
picture now changes this arrow e to does no longer extend the global and instead
now e to is going to extend a 1 because our current environment was you want one being invoked bar misplaced chalk okay
so if we have this picture now things start acting a little funny let's say it's that big name to be Darren I don't
find name here but I find it here so I change this to be Darren it was really
do much here and then that's it so then at the end um name is still Erik in the
global environment which kind of looks
weird so but that's what dynamic scope does and it's um it's a valid choice I
guess for project four you'll actually be working with a language that does do dynamic scoping logo but most languages
do use lexical scoping so um any
questions before I hand it off to Jeremy oh yeah extend means um so if e to is
extending environment one that means that if I don't find a variable here I'm going to look in here so that's yeah yep
you can in this case they'll still be there they'll just you'll never be able
to reach it again but in the next lecture or actually what Derrida could
talk about is one environment do persist and then we can use them for some pretty cool features yeah okay so and off to
turn hear me now so pretty bad good all
right so Eric talks all the way up till that bang let me clarify a little bit up
here someone asked if we could see or just think that this lambda belongs in
this frame you shouldn't think that because you should take this bubble it
just exists somewhere and we have references that point to it because you could later have codes like
let's say function f takes a function G and X some value and apply is gtex and
later we call f2 on 3 something so
expect us to get those 9 right on the
diagram we will see that all right get
some this bad color but all right so f
will point to pair of bubbles because when we define a function we draw two
bubbles what's here parameter is Chi and
X
and the body is applied GE objects and
when we make this call we will have a new frame so let's draw the frame here e to this
famous associated with the planet Earth oh forgot to find us so inside there
should initially be two bindings G and X G will be the function foo X will be big
so now G is to raise what to hold
so what Suho is a lambda so here we could point like that right so that's
why you shouldn't think that these bubbles belong in this frame right because if it it's basically variables
pointing to a construct of lambda and any frame could have references that
point to fill tea bowls so do you clarify it
okay so Eric introduce that Bangor party binded step bang what it does is it
looks for the closest variable with the rebel name name and then set it to
argument straight so we can think of set bang as a lookup plus a assignment it's
nope so inside inside eetu we only have two things right we only have GNX if we
won't have two in there right so sorry I
forgot to point the string right good it
will point directly to both yes right
because of applicate border is play of order we evaluate your arguments before you go into the body so when we draw the
frame we already got turned into this lambda so it won't point to like the food name and then look up food oh right
alright so you should be stepping as a look up plus a assignment or change and
by what Eric wrote over there that bang
so if we view it as a variable look up you look through frames and then look
for the closest variable to separate so
maybe some of you might have a question of what's the difference between step
bang and defined right step bang looks through to find a closest thing and
define essentially just so here if we
change this to define we won't have a
knee look up it will just create a new binding here and point it to learn
instead of looking for the closest rival so let me repeat again distinction
between define and set bang define is really lazy you don't do any lookup you
don't care that you're never get an unbound variable right because you're defining the variable you'll just define
this new binding inside your current frame and just write down value for set bang you'll look for the closest
variable and send it to you any value so set bang doesn't create new findings it
changes them okay so one thing to check
is whenever you evaluate the fine you should not find yourself trying to look for like where's the closest guy or
changing stuff you should just write it down and of course if there's already a name finding you just supersede that
just cough it out there right anyone question
huh
okay
so we don't okay so
this is more like a evaluating precise order matter because if you are saying
that we could keep this as G points to sue and then later look at us right
okay so primitive you shouldn't think of them as inside the frame I'd erase when
Eric through the global with plus and
minus and this and so on either you can
think of them as all bamboos and so on
they still take this form yeah I mean you might make more sense if it's inside
the frame for you but it's like this convention that we all use so you want to pictures right cool so
any questions on step bang in the fine
all right let's move on to a global and
local space
okay so I'm going to introduce a make counts procedures that creates a counter
see if we have time to finish this thing
okay so let's make count is a function right so they're on degree so the main
part is like right here is definition of main of make count starts here the
reason why I say it starts here is because when we define it we know from
midterm one lepprince into lambda creations and also
a mandate valuation right because we can rewrite let into like disk form whoa
that's the one right so it becomes making lambda and calling here by the way so essentially after we're done
defining make count make count that's just this monthís and everything is like
so looking at this we can see that this
part is executed once and then later if
we do count one
and I will get the results of you
valuating the rest so just looking at this code can someone tell me what count
one is going to be like the second Latin
expression right right and what does this look like some procedures I'm huge
compost procedure that takes as a message and depending on what the messages they'll do something right so
we should all know the name for this by now
UC Berkeley