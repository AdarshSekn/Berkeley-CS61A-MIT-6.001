Transcript


sorry I'm like getting started by minute we're we're writing this big proposal to
take over the world with cs10 and today is the deadline and the institution
we're collaborating with on the East Coast had until 2 o'clock our time to
submit and as of 12 minutes of they hadn't done it yet so things are a
little rushed okay um so last time
Oh
so we left off last time with this kind of miraculous result yeah oh you don't
see anything huh oops oh that's not what I want that's
what I want there we go thank you so this very
miraculous result right here in which there are exactly six different ways to
append to list to get the result ABCDE and the query system found all of them
working with what's essentially just a rephrasing of the scheme append
procedure but the schema pen procedure only runs forward you say to little list
and it gives you a big list and somehow by couching it in logic programming
terms we get a relation that can figure
out the constraints forward and backward give you what you want now it can't do
something that can't be done so if I gave it three variables so it's a pen
question where guys close from our question mark Z it's going to run forever giving me
gibberish results so there has to be enough information in your query that it
really does constrain the problem also I should warn you that not everything
works backwards so one example that you're going to see in homework or the
lab is um if you try to write a reverse
set of rules a reverse relation in the obvious way you know reverse this list
that list is true if one is the same as the other only with the elements in the
reverse order you're almost certainly going to end up on your first try with something that works in one direction
but doesn't work in the other direction and I think the extra for experts this
week is to try to come up with a version of Reverse that really does the job by directionally so what that means is that
this abstraction as we're presenting it here is not perfect so in order to make
sure your program works you have to think a little bit about how does the query system actually do the job that
it's doing I should say that this is a
little toy query system that Abel's an assesment wrote just for the purposes of this class if you look at a real logic
programming language they've made great strides in being able to solve some of
these problems but I think it's still not perfect sometimes you have to help
it out a little bit by saying ok don't go down here if you do you'll get into
an infinite loop so we want to see how the query system works that's our job
today and I guess there's two pieces to
that and let me start with the piece
that is sort of big in scope which is sort of stepping back and looking at the
big picture which is right here so here's schemes evaluator it takes two
arguments an expression and an environment I've drawn the environment off to the side because if you think
about what it is you really want from scheme you give it an expression and it gives you a value and the fact that there's an environment involved is just
sort of a detail so this is sort of the main pipe through here so I want you to
compare this which is scheme with how the query system works it takes a query
as input a query is like a scheme expression it's something you type at
the prompt right you can type a scheme expression at the prompt and outcomes the value you can type a query at the
prompt outcomes your query back again with
values substituted for the variables that make it work well what Q eval returns is not a value
and what it takes in is not an environment exactly it's written to take
a stream of environments so you could think if you had a lot of environments
you could just do them one at a time um in some situations there are infinitely
many answers to your question or at least infinitely many potential answers but it's worthwhile seeing them
one at a time as they materialize and you can just stop the computation when
you're happy so on the other hand we don't want to write a program that does
find something print the value find something else print the value that's not very elegant and so what we do is we
use the technique that we have for reordering computations namely streams
so the queue eval kind of on the side input here is a potentially infinite
stream of environments and in principle we go through all those environments an
environment is a binding of variable names to values right just like team basically and we try this query on each
different environment and whatever answers we get take the form of a new
environment and so the result is a
stream of environments again potentially infinite each environment this is unlike
the meta-circular evaluator each environment is just one frame and so you
should ask yourself how can that be because they have a scoping problem the
same as scheme does having a local variable and a particular rule that might be the same as a
variable in some other rule and they resolve the problem differently which is
as you're applying a rule you systematically rename all the variables
in the rule so if the rule has a variable question mark foo then for this
invocation of the rule it's going to be question mark food 27 or whatever and we
slipped it to question mark foo 27 for every place for a question mark rule appears and the next time through it
will be question mark foo 28 so there's a global counter of how many rules we've
applied that are used to make these names and therefore every variable name is unique it only appears in one rule
but the same variable can appear in the body of the rule and the conclusion of the rule and it really is the same
variable as that the same value okay so an environment is a single frame the
frame is you know just like a team frame almost I'll talk about that a second and
the input and the output from Q eval is a stream of frames now how could it be
infinite um when you start out well what do you
start out with when you are typing something at the query system prompt
what's the equivalent of the global environment and there aren't any
predefined variables because unlike scheme there's no such thing as a primitive procedure because there's no
such thing as a procedure period okay so
the things that you might be misled into thinking our procedure names like append
up there that's just a piece of text that's the word ap PE nd it isn't bound
to anything because it's not a variable it's as if you said quote append in
scheme it's just constant text the only variables of the things with question marks at the front
so what we start with is no bindings and
so you might think that the a good starting point would be an empty stream
but it turns out for technical reasons that doesn't work now what you need to
do is start out with a stream of length one containing an empty frame because
nothing's going to happen unless there's an environment for it to happen in so we start out with one environment ie one
frame that's empty now the way Q eval
modifies its stream of frames in producing the output new stream of
frames there are three things it can do
I think let me make sure I'm getting this straight one thing it can do is take a frame and add new bindings to it
so that would be we've already bound some variables let's say from your
original query and now we're trying a rule and we match the conclusion of the
rule against your query and that works but that gives us some new bindings because the rule has variables in it so
we would add those bindings to the frame and that would make a new bigger frame
the second thing that can happen is we can do what I just said more than once
we can take the same input frame and produce several many maybe infinitely
many output frames why is that because
in order to get from the input frame to
whatever output we need we're going to not what to eval does is it tries all
the assertions and all the rules to see if they match the query that you're
making and so for every assertion and rule that matches we get a new set of
bindings and it can get to be infinite because of recursive rules so you can
end up generating an infinite stream of frames that way and of course as usual
with streams what's really happening is they get generated one at a time and the
next one is generated only when we force a promise by taking a stream coder just
you know when we learned about streams the other week okay so I guess one thing to add to this picture is that there's
kind of an implicit input to every cue Eve alcohol namely a database that
contains all the assertions and rules so whenever you say assert bang such-and-such you're adding to the
database in queue eval the Gator basically you know it's a global thing in the evaluator queue eval always looks
through the database to look for things that match your query okay oh the third
thing that can happen to a frame in this stream of frames is that it can be
rejected you can say well I'm sorry you've had a partial match and then you
try to apply a rule and now I'm evaluating the body of the rule and I can't match that so this set of bindings
that you've given me is not going to work okay so we can add to a frame we can add new
frames and we can remove frames from the stream of from the output stream of frames it's not done by mutation or
anything it's producing a new stream of frames um functionally so that's pretty
amazing by the way this is all functional programming in the implementation except for adding to the
database so that's the only non-functional part of it okay now let
me talk next about um how a query is matched against things in the database
so we have our query like
like Brian what okay and we're going to
[Music] let's say we don't have any bindings I don't know what what is we're going to
match this against every assertion in the database an assertion is something
like like Fran broccoli right
so likes matches like Brian matches Brian what question mark what matches
anything so it matches broccoli and so we make a new frame out of the old frame
in which we've added a binding so now we have a frame that says question mark
what equals broccoli and that would be
one entry in a stream of frames okay this kind of pattern matching is very
very straightforward and easy okay if you remember the equal question mark
that you wrote in the first week I think of chapter to give an EQ you were
supposed to write equal for homework remembers that okay matches exactly like
that it goes through all the cases is this a word and if so is that a word if one is the other isn't false if they're
both words EQ them are they both is one a list and the other not a list false
are they both lists equal the cars equal the cutters if both of those are true
it's all equal match works exactly the same way except that in the query this
is and this is something in the database an assertion in the query you can have a
variable but not in the assertions in the database when you say assert bang
and you don't say rule you can't have any variables in what you
say it's got to be a particulars in Mike likes brand broccoli okay what about rules here's where it
gets interesting so in the database I
have rule grandparent old young and
that's true if and parent
old middle parent middle okay that's
what's in the database and my query is
grandparent who Brian okay
okay so when we make this query first we
go through all the assertions in the database let's say there are no assertions no plain old assertions about
anybody being anybody's grandparent all the assertions are about Parenthood now
we're supposed to deduce who the grandparents are so we we go through the rules and we find this rule and the way
evaluating a rule works is you match the
conclusion of the rule which confusingly is the first part of the rule with the
query okay so if I do that I say okay
this matches I get the bindings old one
equals who and young one equals Brian so
this is a frame that comes out of matching the query against the
conclusion of a rule but this kind of frame is something you can't get in the
scheme evaluator in the scheme evaluator it's always a variable equals of value
and it's perfectly clear which is the very bone which is the value and you're not allowed you know if I say define an
X something or other and then I say define Y X and you draw an environment
diagram that has Y bound to X instead of Y bound to something or other then you
lose points right variables aren't bound to variables in the scheme variables are bound to values and that really really
simplifies life here we have a variable bound to a variable even more
complicated things can happen right so if I have
um a rule that has question mark you question mark V and in my query it says
something like question mark no it says Fuu dot question mark X now we're going
to go through and make two bindings from question mark u1 to Foo from question
mark v1 to question mark X okay so all that kind of thing can happen as you're
matching up queries against rule
conclusions and this is because reason is more complicated in the assertion
case only one of the things you're matching is allowed to have variables in
it in the rule case both of them can have variables okay so now think about
remember that one of the rules here is not I mean rule I mean like one of the
rules is if you use the same variable name twice it has to mean the same thing
both times right so if later on in this evaluation process we make another reference either
to question mark old one or two question mark whoo so there'll be another binding
someplace later on and you have to be able to chase down more than one binding
to get from a variable to its value and maybe we don't know yet what its value is so if that's the environment we don't
know what the value of old is or what who is rather we know it's the same as
some other variable but we don't have an actual value for it okay
this much more complicated kind of matching where you can have variables on
both sides is called unification
there's a whole section in the book about how unification works there's a
big chunk of the book about how the query system works all together but the
part that I'd really like you to read is the part about the unification algorithm not because god forbid you're going to
memorize it it's really complicated but I really would like you to get a feel for what it does and for how complicated
it is I would like you for example to be able to do a fairly simple unification
by hand so a fair exam question would be
here's a query here's a rule what findings do we get when you unify
them unification was invented I think in
the early 70s and as often happens
there's a dispute about exactly who invented it there's a footnote about that in the book everybody outside of
MIT says it was this guy in France everybody at MIT says it was Col Hewitt
and a mighty the reason for the dispute
is that Hewitt wrote this enormous Li long thesis that nobody understands is really dense do you think our textbook
is dense you should see Hewitt's thesis so it's not clear what he did or didn't invent unless you read very very
carefully anyway be that as it may the unification
algorithm all by itself is Turing complete meaning anything you can
compute with the computer period you can compute with this algorithm so we can
have this query system that basically does nothing but unification and that's all you need to to compute any
computable function okay when I say computable the bad news and you learn
this if you do a time of the theory 160 or 162 or something is that of all the functions
that there are in the world only a teeny teeny sliver are computable it's
infinite there's an infinite number of computable functions but there are degrees of infinity and this is a teeny
one is way way more functions that aren't computable but if it's computable
at all that's the sense in which I'm saying that this is universal any function that's computable at all is
computable this way so that's what makes logic programming interesting is the
fact that it's universal and people didn't realize is universal until the
unification algorithm came along so you're going to read about it in the book you're not going to try to remember how it works but you're just going to
see boy they sure have to deal with a lot of special cases to get this right
so the result is beautiful and elegant above the abstraction barrier when we do
logic programming but the algorithm itself is messy okay so that's the
thrown unification so when we see a rule
we unify your query against the conclusion of the rule if that works
the result is an extended frame right because we had some bindings on the course of doing this unification and a
new query namely the body of the rule in this case it's that and so we're going
to take and parent ba ba ba parent ba ba ba and we're going to try to evaluate to
Q eval that starting here starting with these bindings so old one and young one
are constrained well old one isn't really constrained what's really going
to happen is later on we're going to constrain old one and that will implicitly constrain who to have a
particular value young one we know the value already and it's got to be that to match so we're going to end up looking
for everybody who's a parent of Brian in
the assertion okay that's an end that body and is
special remember I said and or and not are kind of like the special forms of the query system so we don't try to find
a rule whose conclusion is and blah blah blah we don't do that instead we take
all the pieces there could be you know in this case is exactly two but there could be any number but I'm showing you
how to works and you can see the obvious extension two more and we're going to
see how an the or and not are evaluated so starting with in what I've drawn here
is the initial situation when you're typing a query at the query prompt
mainly we start with a stream that's what these braces min and inside the stream is an empty frame now if this
that's not what's going to happen here because in this situation this and is
the body of a rule so what's going to come in here is a stream that includes
this frame and maybe some more frames if there are more matches to other rules
probably there aren't but so it's going to be at least this frame where I've
drawn this empty stratum the stream with an empty frame so this is just to remind
you what the initial conditions look like but what's coming in here can be any stream of frames and we want to
evaluate and PQ and I think this is one of the most beautiful things in the course up the air with tree map not
quite but almost we take whatever our initial stream of frames is we query
evaluate P the first piece of the and the result of that is a new stream of
frames which we use as the input to a to eval that evaluates Q because what's
going to come out of here is every possible way to match P every set of
bindings that make speech and then starting with those bindings
we're going to look for ones that also make Q true and that's what's going to come out the side here so when you sort
of cascade q eval calls one after another in this way you're computing an
and I'm not beautiful and one thumb up
okay few people like it I love it I don't like or so much I mean it's okay but
it's not mind-blowing like and because
what we're going to do is evaluate P and Q independently because for or you don't
have to have one set of bindings that satisfies both of them you're going to take any set of bindings that satisfies
either of them if it satisfies both that's a bonus in fact if you've played
with the query system in the lab at all you will have noticed by now if it satisfies both of them you might end up
with the same result printed twice because it means there's two ways to
reduce the same set of bindings the same frame okay so starting with whatever
we're starting with in both cases it's the current environment stream goes into
both Q evals we value ap we evaluate Q each of those gives us a stream of
frames and now we have to somehow merge this stream of frames how do you merge two streams yeah interleave
this is why the when you do a query
that's at all complicated you're sometimes surprised by the order in which the results come out it might look
a little messy why because what you're seeing is the result of an inter leave
and you know that gets a little messy so
that's the explanation for that okay now comes the really ugly part like the good
the medium and the ugly I think that
would be a good movie the good the okay and the ugly and that's not not ugly and
not ugly because it can't really do the
job that it's supposed to do in actual mathematical logic so let's say I put in
the database a bunch of assertions and I
say Brian likes ice cream Brian likes pot stickers Brian likes the Beatles
Brian likes the kinks Brian likes broccoli Brian likes the zombies okay
that'll do and now let me ask you how
does Brian feel about asparagus does Brian like asparagus you don't know do
you maybe Brian likes asparagus and just hasn't bothered putting that in the
database maybe Brian doesn't like asparagus suppose I ask who likes the
Beatles how many people in here like the Beatles okay I don't know most of your
names so they're not in my database so
if I ask who likes the Beatles I'm going to get not every possible answer so if I
say who doesn't like the Beatles and if there's no dis
like information in the database it just sits there and gives me no result at all
it doesn't tell me who doesn't like the Beatles what we can do is say something like who
likes broccoli and doesn't like the Beatles because we can go through the
database and get a bunch of people who like broccoli okay and then for each of
those persons pricks each person we can say the so-and-so like the Beatles if
it's in the database and we say yes if it's not in the database we don't know
for sure that they don't but we don't know that they do and so that would be
included in the result so as far as we know so-and-so likes broccoli and doesn't like the Beatles all right the
upshot of this is that not never ever generates new bindings you never find
out something you didn't know before because if not the only thing not has
the power to do is eliminate a frame an
environment from the stream the output stream okay so not over there is a
filter it takes a frame stream and what
you get out is a subset of that frame stream namely the ones for which we
don't we are not able to prove that p is true for this set of bindings so for
each frame we run the frame through Q eval with their query P and then we say
okay was the answer to that empty no frames if so then the original frame
that we started with goes in the result if we do have a frame in the output
which means we did find a way for P to be true then we remove that frame from
the output so anything that could make P true we eliminate that's what not does
so this is why it's pretty much guaranteed that is you just typed at the query prompt a
query that starts with not you're not going to get any output at all there has
to be some variables bound in order for not to do anything and there are two ways that can happen one is that the
knot is in the body of a rule and the conclusion of that rule matched your
query unified with your query and not produce some output frames or the knot
is part of an end and it's not the first Clause of the end the first Clause of
the end created some binding some constraints and the values of variables and then the knot comes along it says
well ok you said you can handle this this in this set of environments but
sorry I'm rejecting this one in that one it's only we're only keeping this other
one namely the one for which P cannot be satisfied questions about that if you're
confused about this it's okay you're just learning about it the book talks
about it at length about the problem of knot and why you know we we can't just
exhaustively be sure now footnote sometimes we're dealing with a known
finite universe okay so like there's
only four people in our universe there John Paul George and Ringo and we put in some some assertions about
them like you know John wears glasses or something and then we can say is P one
of John Paul George I am so not P is is X person one of John Paul George Ringo and not such-and-such
so if you're in that kind of situation then you can sort of find out all the knot cases
provided that you know everything there is to know about or everything that's interesting to know anyway about those
four people that comes up sometimes in logic puzzles so one of the things
you'll see maybe in the book is trying
to solve you know who lives in the yellow house kind of puzzles in the query system and you can't solve them
unless you tell the query system that everybody has to live in the yellow
house or the green house or the blue house or the orange house before you give it the particular clues that you
have all right so and or not let me try
to sum up everything this is an imperfect abstraction in the same way
that streams were an imperfect abstraction remember we said sometimes you had to put an explicit delays and we
could fix that by having a normal order evaluator this is an imperfect abstraction also and as far as I know
they haven't really fixed it they've worked around it and the workaround is in Prolog which is the logic programming
language everybody uses is the thing called cut it's another special form it says don't go down this branch you know
if you just match this don't try to apply this rule recursively and and that
way if you think about the order in which things happen you can prevent infinite loops in your queries and your
rules okay so that's one thing about
logic programming another big thing is unification unification was a huge step
forward in computing it was a non-obvious invention nobody knew it
could be done let alone how to do it until somebody did it and it's at the
heart of making logic programming work it is the only algorithm basically
in the query system so in every other kind of programming that you've seen where two algorithms come from they come
from you the programmer right for every particular problem that you're trying to solve you invent an algorithm for
solving it in Clarice's them you never talk about algorithms you never say first do this and do this and so on or
you know what's F of G of H of 23 you know do things like that instead you
just say here are some things that are true and the query system uses it's one
algorithm unification to find amazing
results including the ability to kind of work backwards if you think about it in functional terms but it's not the query
system doesn't think of it as backwards because in that set of rules for upend
the three slots that go after append you know they're all just data it's not like
one is privileged in some way um okay so
unification 3 is the difference between
eval and Q eval I'd really like you to understand this that when you ask a
question in scheme you get one answer because what eval gives you is its
result is the answer to the question you ask you know what's the square root of
49 it's seven thank you
but in the query system you can get multiple answers maybe infinitely many
answers just because of the way the
algorithm works and the way rules can be recursively applied even though they're
not procedures
okay so QE valves therefore doesn't return an answer it has to somehow
handle the fact that there might be infinitely many answers and the way we handle situations with infinite datasets
is using streams so here's an application of streams you wouldn't have
to do it this way just as when I first started talking about streams and I wanted to know if a number was prime you
could write that little loop let you know I equals two bah-bah-bah try I plus
one and keep going like that you can do the same sort of thing for inventing a
query system but the cool functional way to do it is to use streams and it means
that as you read the program we are doing the evaluation for all the
different possibilities in parallel kind of even though it's not really how it happens so at the very end
think about the read eval print loop in the query system it can't just be print
queue eval of blah blah blah because queue eval doesn't return anything
printable it returns a stream of frames so what the read eval print loop has to
do is keep covering down that stream of frames taking each element and remember
each element is a set of bindings and then looking in that set of bindings to
find the values of any variables in your query and again that might involve
chasing down a whole bunch of bindings because your variable might be bound to another variable just bound to another
variable which events another variable which is finally bound to a value and has to be able to work its way through
that and get to where it has values for all the variables if possible and then
print that so the revell print loop is a
little more complicated than it is in scheme because that's where you turn this stream of frames into something a
human being can read any questions let's point Lou Thesz
logic programming is really cool good who's totally lost to people now I
totally lost people see what your TA has
to say in Section ask me questions you can ask questions now if you have any you can come visit me in office hours
again you're not expected to know every detail of the implementation but I would
like you to read through the details of unification this is the thing at the heart of the system okay now um in my
lecture notes on the next page which is
page 372 is an example involving a penned completely worked out so the
question is upend what - what - get this - element list AABB they used a a rather
than a so you don't get it confused with the variable a which there also is one of so here's my query and you can't let
me go through all the steps of calling unify match unify match takes three
arguments the query the conclusion of a
rule and a stream of environments I'm not sorry and environment cue eval knows
about a stream of environments the unification algorithm knows about only one frame at a time so it's an
environment so it starts out being the empty list in this first evaluation now once I actually tried going through this
in lecture all the students fell asleep
so I'm not going to do that but if you're the kind of person who really needs to see step by step how something
works it's not so difficult to go through this and work out for yourself there's one
two three four five six calls to unify
match in here so you know six was a pretty big number bigger than I would
want to do in lecture but it's not five hundred or anything yeah
we're you likely to see the core system in the wild that's a good question Europe remember I said invented in
France Americans for some reason mostly
aren't very interested in logic programming there are little exceptions here and there um I'm not sure if it's
still true but I think it is u-dub University of Washington it's kind
of a hotbed of logic programming the closest thing to it that you'll see in
the wild in this country is database
query systems like SQL which are very similar in spirit to this at one time
the Government of Japan had a regulation
saying that all the programming for I think then we were up to fourth generation and computing was going to be
done in Prolog it's just like in this
country the Department of Defense has a rule that if you want to program anything for them and has to be done in
Ada which is this really terrible language Don't Tell Paul he'll finger I said so
you like data it's just so big in there
anyway in Japan it was prologue and they've backed off from that but you see
a lot of still prologue code in the wild there that's I can do any questions
it's not alright on Fry oh yes good is it massively inefficient
no because of the reordering and the memoization of streams so it's much more
efficient than it looks yeah no it's not bad is that a hand up
are you yawning he's yawning okay on Friday we're going to try to attempt
to review of everything please bring the lecture on Friday something to write
with and something to write on I'm not collecting anything but you're going to do an exercise your computer is fine if
that's what you have but some way to write things and I'll see you Friday
UC Berkeley 