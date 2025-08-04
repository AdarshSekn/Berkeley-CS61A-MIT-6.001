Transcript


are not a l of people here I guess I scared everybody away last week with the analyzing evaluator or something but um
speaking of which on page 41 of volume two of the reader is this page called
exit information which talks about the final exam and in particular what you
need to know about all the different evaluators we're looking at of which
there have been several on a new one this week um you could ignore the part of
about the non-deterministic evaluator which we didn't do but other than that what it says it tells you um you know
you for this kind of for this evaluator you're supposed to know how it works and
for that evaluator you only have to know how it behaves all that's in the exit
information sheet also in there is be a lab assistant let me put in a plug for
that um next semester uh if you like the course
we always need lab assistance um if you a lab assisting is an unpaid position
although you can get uh credit for it one unit per three hours per week of lab
assisting um but also if you want to apply for a paid position down the road
as a reader or ta we give preference to people whove lab assisted uh both as a
bit of a reward for doing so and also because the more times you've been through the course the better qualified
you are to read in it or to teach it um and finally letters of
recommendation it basically says um when you're applying to grad school uh if the best you can do for
letters of recommendation is that you got a good grade in a freshman course three years ago um the people who read
your application will figure that out uh and you should really try to get letters
from people people um with whom you work down the road rather than me
nevertheless I always do get people asking for letters um because presumably everything's gone
downhill from there for them since this course um and you know I write a nice letter but all I can say is this person
took my course and got this grade unless I really get to know you because you're on staff or you know something or you do
research project with me then it's different okay
um this is a course about programming paradigms um we've been through two
major ones functional and objectoriented and we had just a look at client server and now we're going to
have just a look at uh declarative programming or logic programming which
is a really really neat idea in which um you don't have to write a computer
program at all there is there's no sequence of steps you're not not telling the computer do this then do this and
what's the value of this instead you just tell it things you know and then
you ask it questions and it figures out the answer um so it's very
magical um the most popular logic programming language in the world is called prologue
um if we wanted to teach you a whole other language we would use it but um
Aon and susman just did a very simplified logic programming system in
scheme um and that's what we're using so to assert things to tell it things
you say assert bang um this is a spe sort of a special
form of the query language uh likes
uh stickers solar and added to database so
let's put in a few
more
okay so here's our database of assertions and now I can ask
questions a question is something that doesn't start aert bang so I'm going to
ask question mark who likes poot
stickers and um in this system a word that starts with question mark is a very
variable and everything else is just text um and we get the answer Jordy
likes pot stick we get the answers Jordy likes pot stickers Brian likes pot
stickers right um so this is the first thing to note
about logic programming is that you don't just get one answer in this case we got two
answers um in some more complicated cases there may be infinitely any answers uh we don't have a
system where that would happen yet but uh it's theoretically possible for stuff
we're going to learn in a bit um so I can say
um Ryan likes question mark what uh by the way I'm trying to use meaningful
variable names here but as always in programming the query system doesn't care what name you use it could just as
well be X and Y as well as the query system is concerned and we get Brian
likes pot stickers um which is a little interesting because Brian also likes ice
cream um so why didn't it tell me that and the answer is that this system works
by pattern matching so
if I ask the
question if I ask the question Brian likes what uh the way pattern matching
works is for list you match the cars and you match the Cutters so recursively so it's a
potentially deep recursion um although I don't think it will be for
the queries that we're going to use mostly we'll see
um and the way you match a nonp pair is um two things match if they're
equal and something that starts with question mark in the query basically matches
anything okay so this does not
match Brian
likes
ice cream because okay Brian matches
Brian um and then we have to look at the cters and we find likes matches likes
and then we look at those cters we find question mark what matches ice that's fine then we look at these Cutters this
one's the empty list and this one's a pair so they can't match those are just
don't work um so we could solve that problem
by taking advantage of the notation that we have for improper lists so I'm going
to ask the question Brian likes dot question mark
what and now I get both answers because this query
is and instead of
this Brian likes do what is this so the cter is question mark what so Brian
matches Brian likes matches likes and question mark what matches anything
namely it matches this entire L
structure okay questions about that so far who's with
me awesome who's not with me
nobody okay um that's great that's not the way we usually
solve the problem usually we solve the problem by
um taking ice cream and putting in it a list so the assertion would always be
Brian likes and then one thing a list of length three and in fact what we really
do is this we say
likes Brian pot
stickers likes Brian parenthesis ice cream
oops uh oh now I'm in
trouble
whoops oh yeah all right let's try again start
thanes Brian I'm afraid it actually took that assertion though but we'll
see here we
go um so usually what we do is we take the name of a relationship like
likes and that comes first um it's just a convention as far
as the query system is concerned it treats every element of the query the
same way every sort of car of a list the same way or quitter of a list for that
matter um but people find logic programs more
readable if you put a a relation first and um the sort of arguments to
the relation after that um so likes is a relation between
two things a person and a think Al like
um so now I can say likes well like likes
Brian what yes see it took it did take it
twice never mind that pretend that isn't there or pretend it's only there once
although it does point up a problem which is that if you have the same assertion in the database twice it'll
find it twice um I can say likes who
what and then we also find out what Jordie likes um if I say
likes XX however I get no
answers uh that only works
likes narcissus
nissus now I can ask the question likes xx and I do find that um so the point of
this is that once a variable has been matched in a
query any repeated occurrence of the same variable in the same query has to
have the same value okay everybody get
that um I think this is all pretty simple so far
um let me say a word about relations up to now sort of the Bedrock of our
approach to almost everything has been functions and a
function can connects uh input values arguments to an output or return value
um and that return value can be anything but what makes it a function is that
every time you call the function with the same arguments you always get the same value so putting that more broadly
with functions there's only ever one answer to a given question
right uh relations are different um there can be dozens of things um that
are in the relation likes with Brian um there can be you know lots of
people who like the same thing who likes ice cream yeah
um so a relation one way of looking at it is
that it's a Boolean function a predicate function I should say um
that returns true or false so a relation you give it a bunch of input values and it's either true or false
that this relation holds among these values so what in functional programming
we would think of as the answer is instead just one of the
arguments to the relation do that makesense sense um
footnote if you're a mathematician you think about it differently if you're a
mathematician uh first you define what a relation is
um and then you say well a function is a relation with certain
constraints um so you can do it either way but for programming purposes I think
it's easy is to start with the idea of functions which you've seen before um
actually you've seen relations before back in high school algebra relations are things like less than or equal
to and in math notation you put the less than or equal to in between two values
um but we move it out to the front for the same reason that we moved function names out to the front like plus namely
uh you can have any number of arguments so we will have complicated relations
among four different things so uh for example
um division is a relation
among a dividend a divisor a quotient and a
remainder okay so this is integer division so this is true if dividing the
dividend by the divisor gives that quotient and that remainder
okay um but relations in general
[Music] can uh have many many different ways to satisfy them so um three is less than
what okay that would be an example of something with infinitely many possible
answers three is less than four three is less than five three is less than six three
is less than a million three is less than a Google Plex and so on
um so in principle if I could put in that relation into this system and then
ask three is less than what I should get out an infinite number of
answers okay
um okay so
far uh this is probably seems pretty boring and limited to you because the
system only knows exactly what we told it so any question that I ask I have to
have already provided exactly this answer
um so if I say um
uh it tells me that Brian hates cheese but you know that's really inadequate Brian hates racism and Brian hates lead
Zeppelin and you know I there's lots of things that Brian hates
um and similarly there's lots of things that Brian likes that the system doesn't know about um it doesn't know brand
likes the Beatles
um okay we'd like to be able to generalize this a little bit so I'm
gonna put in a little bit of data
here oops
did that work probably
not yeah it did
okay
right so so and so is the parent of so and
so
yeah um so now I can ask um who Brian's parents
are I get two answers and I can
ask who Brian's children are I get one answer but I can do more than that I can
do also so do this here's where it starts getting interesting so there's a special kind of
assertion that I can make called a
rule oops
there ah this isn't going to work we'll
see okay um let's see if it worked
y it
worked okay so the important thing to note here is that I didn't tell the
system explicitly that I have a Grandpa Joe and a grandma Minnie and a grandpa
Max um the system inferred that derived
that from information that it had about Parenthood plus this
rule so rules are the logic programming
equivalent of procedures so a
rule looks like this
um by the way don't be misled by the
fact that we have parentheses around anything in this query system we are taking advantage of schemes read
mechanism that turns stuff in parentheses into box and pointer diagrams but we're not using schemes
evaluator there isn't a procedure called Rule that we're calling there isn't even
a procedure parent or procedure grandparent all of these things are just
essentially strings of text although you know what they really are is lists um
being matched one against another so the way rules
work is this um well first of all when
you type in a query to the query system the first thing it does is look
for assertions non rules in the database that exactly match the query use exactly
in this sense of question marks matching anything um and any assertions like that
that it finds it gives you as a result so if I had made any direct assertions
about who's the grandparent of whom then um we would see those then it looks for
rules but it can't look for a rule that in its entirety matches a query because
this rule is too complicated for that it looks for a rule whose conclusion
matches the query so my query was grandparent question mark H Brian
and this rule says grandparent question mark old question
mark young do those match yeah they do grandparent matches
grandparent question mark who matches question mark
old and uh Brian matches question mark
young okay so the query I asked does
match the conclusion of the rule if that isn't true then we just
skip over that rule but if it is true if the conclusions match then we take the body of the rule
as a new query to evaluate and I'd like you to understand I hope
you should like just instantly understand but if you don't let me help you understand that this business
of set up the values of variables old and young and now evaluate the
body that's a lot like how scheme handles a procedure
call um it's a little bit different because it's the query evaluator not the
scheme evaluator that we use to evaluate the query and the result of that evaluation
is true or false so we want to know um is this true this is the body of
the query and is like a special form in
queries uh and or is another one and not is another one
um so assert bang Rule and or not those are the only kind of reserved words in
this system that have special meanings so what and means is if all of its
subexpressions are true then this is true so a lot like the procedure well
special form and in scheme which says return the value true if all the
arguments are true uh the difference is you don't true
printed out instead what happens is if the result is true then the query system
says this is a match and what's actually printed out is the original
query but with specific values substituted for the
variables so the query was grandparent question mark Hub Brian and every time
it succeeds in matching that through the use of this rule it prints out out
grandparent so and so Brian by finding out the value of
who um well so now what it has to do is try to
um match two queries about parent namely parent question mark old question mark
middle parent question mark middle question mark young but just as in scheme evaluation
queries are evaluated in an environment the environments are a little different in details but to a
first approximation it's the same idea so when we matched my query grandparent
question mark H Brian against the conclusion of the rule we came up with
some constraints on these variables so question mark who has to be the same as
question mark old we don't know who it is yet but whoever it is they both have
to be the same uh and question mark young has to be
Brian okay so now we look for parent question mark old
question mark middle since we haven't yet constrained
either old or middle we're seeing middle here for the first time every single parent assertion in
the database will match that first parent clause in the
an it's just parent variable variable and we get every single one matches so
you know parent Tessa Bob matches um but then we have to also
satisfy parent question mark middle question mark young so in the case parent Tessa Bob uh We've bound Tessa to
Old I'm sorry old to Tessa I should say we've bound middle to Bob and now we
have to match parent middle young middle and young are both bound middle is Bob
Young is Brian is Bob the parent of Brian no he's not so we reject that
particular set of bindings now we look and we find another assertion in the
database that says uh parent question Mark mini I'm sorry not Pastor Mark
parent mini Tessa okay fine um old is Minnie middle
is Tessa and now we're looking for an assertion that matches parent question
mark middle question mark young but middle has to be Tessa it's constrained it's bound already and young has to be
Brian so we're looking for an assertion parent Tessa Brian and we find one Tessa
is is my mom and as a
result this line is printed as a result of that set of circumstances
yeah uh so would it be more efficient if the two and clauses were flipped in
order um it would for this particular
query but remember you can also ask the question Grant parent mini question mark
who and for that it wouldn't be more efficient um but it's a good thing to
think about and sometimes it's a crucial thing to think about because what you get is
so inefficient that it never gives you an answer at all since they're looping so we're going to see some things about
that coming up later on okay any further questions about this
parented example
yeah sure grandparent oops question mark x
question mark
y there they are
okay um by the
way when a variable is used twice um in a query I told you they have
to match the same thing both times like if I had said likes question mark x
question mark x um for rule the same thing is true once
a variable is bound in a rule uh any later uses of that variable have to
agree with the first one but it's not true across queries or across rules or
even across invocations of a rule so if
I want to know about great great grandparent I might have a rule that
says um you know this person is the grandparent of that person and that person is the grandparent of another
person um and then we might end up looking for grandparent a couple of
times and there'd be different bindings for young and old each time so it's only
in a particular application of a particular rule that
um a binding is in scope uh
that's still a little vague we're going to talk today we have talked today and
we'll finish talking talking today about what you can do with the query system and on Wednesday I'm going to try to
clear up what I'm sure is some uncertainty about how it actually works um but first I want you to
appreciate what it can do so it's it's looking at a huge abstraction today from
above the line and Wednesday from below the line okay um so I used grandparent and
parent in my example a more complicated example
would have assertions mother and father and would have a
rule like
this
okay so here's a new rule says somebody is somebody else's parent
if either they're the person's mother or the person's father and we could use this rule along
with assertions about um mother and father to do a whole family tree thing
you can ask you know is somebody my cousin once removed and all those things
that you never remember what they mean um but the database could figure it
out so this is a database use of the query system and in
the book um their first example I think of the query system is also kind of
datab basy uh they put in data about the employees at a company a fictitious
company and their job titles and their salaries and then you can ask various
questions um and something like this a different notation but this basic idea
is how database systems work in the real world you can ask queries with ANS and
ores in them and you can invent rules and all sorts of things
yeah
okay what predicates is the question does this implementation of logic programming have access to um I'm going
to give you two answers to that question the uh elegant logically
correct answer is none all it knows about is pattern
matching and any relations you want you have to build um the quick and dirty grubby
answer is um in this implementation there is one I lied there's one more
special keyword called lisp value that lets you evaluate any lisp
predicate uh they use that for questions about who makes more than $40,000 a
year um but you should try to avoid using list
value because you end up leaning on list to do all the work for you um we can in
fact invent arithmetic purely in the query system and uh we actually do that for positive
integers and if you look at some of the old exam questions in the course reader
um there's things like invent plus we you represent the number five as the
sentence AA AAA okay so that's how you represent
positive integer non- negative I guess integers and then you can build addition and subtraction and multiplication and
division on top of that system um let me note you don't have to build subtraction
separately from addition because supposing you have addition um you can ask questions
leaving out you know using as a variable any piece of the relation so uh you
would have a relation like that would be true for something like add 3 4 7 so
notice the difference between a logic programming relation and a scheme
function and the scheme function would be add three4 that would be the question you ask and you get the answer
seven um in the query system you ask the question adds up to three four 7 and the
three numbers would be like arguments to the relation and what the relation tells you
is yes that's the case 3 + 4 is 7 or no it's not if you asked it a question that
was false okay so your relation will
have one more component to it than you're accustomed to in functions like
take even parent if we were writing a parent function in scheme it would be um
well let's talk about father and mother where it's more or less unique apart from
exceptions um there'd be a function parent quote
Brian that would return the answer no I'm sorry father quote Brian would
return the answer Leonard mother quote Brian would return the answer Tessa and those would be unique answers note by
the way in scheme you say quote in front of constants in this query system you don't
quote constants instead you question mark variables
so it's sort of the the default thing for a word to mean is a constant rather
than a variable and note also that these names
of relations they're just words so here in in this rule I put the
relation first but I didn't have to I could have said rule question mark old
parent question mark young and then you know the same thing further down um the
query system itself really doesn't know anything about what's a relation and what's an argument to a relation all it
knows about is pattern matching um and it's really quite
surprising that that turns out to be enough to do Computing um and we'll talk more about
that part of it on Wednesday how amazing the algorithm is
yeah um I'm
sorry oh yes the order certainly matters yeah absolutely
um so for instance earlier I put in two different kinds of likes one infix and
one prefix and they didn't get the same results um
okay here's the fun
part
okay look down here um this is a piece of scheme code
it's the procedure append takes two lists it says if the first list is empty
return the second list otherwise cons the first element of the first list onto
aend cter of the first list to the second list right you've seen this before back in chapter two it should all
be totally familiar to you so now
look up here um where it says AA pretend
it says add assertion this is a uh because I the query system doesn't have
a load command but scheme does so AA is a scheme procedure that is equivalent to
the assert Bang thing in query system um
so here are the rules there's two rules this one
and this one and as we talk about them I'd like you to compare them to the
scheme code so the scheme code has two cases the base case and the recursive
case and the two rules correspond to those two cases so the one that's highlighted now corresponds to the base
case in the scheme code the base case says if a is empty return
B this rule says the relation
append holds for the empty
list any list Y and that same list Y in other words if you append the empty
list to anything you get the anything okay everybody clear on the relation the connection between this
append Rule and the base case of the append
program okay a couple of sideways somebody ask a
question so we're comparing this rule with just this much of the scheme code
if the first argument is empty return the second argument this
says if the first list is empty and here's the second list this is
like B it's like this is the a value this empty list and this variable Y is the B
value in the original scheme code so empty list appended to B
gives B and the same thing here
yeah okay I'm going to move on um now let's look at the other rule that's a
little more complicated first we'll look at the scheme code what if a isn't
empty this says split it up into its first element and the rest of it its car
and its cutter and we're going to recursively
compute a Penn cter a be and we're going to stick car of a in front of
that okay and that's going to be the result so the result of a pend where the
first argument is not empty is a pair because cons makes a
pair the car of this output pair is the car of the first
argument the cter of the output pair is the result of doing this a
pend okay so now let's look at the conclusion of this
rule so first of all this rule applies
only in the case where a is a non-empty list right that's like the if in the
scheme code only if null a is false do we get to that
cons so since the first argument is
nonempty we can think about it in terms of its car and its cter that's what this
is this is scheme dotted pair notation says this argument is a pair
whose car we're going to call U and whose cter we're going to call V okay so
um question mark U is r a question mark V
is cter a um and then question mark Y is
B right okay
well we don't have to divide B I'm going have to divide y here into its car and
its cter because the scheme code doesn't div divide B into its Carnet cutter the only use of B is right down here right
that's the whole B so a is replaced by this pair u. v b
is replaced by the variable Y and now what do we know about the result in this
case it should be a pair because of that cons whose car is equal to the car of
a now what you're going to be tempted to do every single one of you is going to
be tempted to say something like question mark U
dot append question mark V question mark
y right because you're going to want to take the cter of a and appended to
B if I had some red chalk I'd use it but I don't so I'll just do
that there's no composition of functions in query system because there's no
functions first of all in the query system so you do that on the final zero
for that question um so what can we
do well I don't have
an exact expression that I can put in here yet so I'm just going to make a variable
Z which is the cter of the result and then I'm going to assert
something about the relationships among these variables that gives me the right value of Z namely Z should be the result
of a pending V with Y that's what this says
so if we get a query an a Penn query in which the first thing is a
non-empty list and the last thing is a non-empty list and if the cters match up there's
this question mark U here and question mark U here if the same variable occurs
twice it has to match the same thing and then we evaluate the the body of the
rule which is this recursive invocation of the same rule it says um I want to
assert or in order for this thing to be true in order for this rule to match the
original query it has to be the case that
appending cter of a to be gives cter of the
result okay and it's a little bit of a convoluted way to think if you're not accustomed to it but it gives us some
remarkable results I can say
append AB b c d e AB B CDE
e oops what happened uh uh did it not
load wait I'm really confused
nope all right let's try this
again
but oh I'm still in SDK oops I'm very gdl but I defined
it okay let's try again hope this works because it's kind
of the big moment of the lecture coming
up yes corre three results there we go so that's not a big surprise but I can say
append ABC to
what gives a b CDE e that works I can
say append what to
De gives a b CDE e and that
works and finally I can say aend
XY to get AB CDE what are all the things I can append to each other to get
ABCDE and here they are okay functions won't do that only
relations will do this piece of magic sorry for running over see you Wednesday
UC Berkeley