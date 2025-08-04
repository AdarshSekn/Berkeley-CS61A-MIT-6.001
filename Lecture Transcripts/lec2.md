Transcript


okay good afternoon welcome to Co 61 a session - that's Jordy he said ta you
have a problem talk to him not me they're good um okay so apparently something I said last time
started a huge panic and like half of you showed up at the health of the self-paced Center wanting to know about
3s and I'm trying to figure out what it is that I said that's different from
every other time and I can't think of anything what I did say was if recursion
with that example up there we looked at that's recursive is new to you then you
don't have the programming prerequisites but I'm really surprised if so many more people this semester than usual haven't
seen recursion before so if you have seen recursion before but it's just that the course is going fast well the course
goes fast you have to get used to that so try not to panic what you do is like
do this week's reading do this week some work if you don't understand something ask for help and then if you're feeling
lost then panic okay who still doesn't
have a computer account good okay
ergonomics right now as we speak on the computer science education mailing list
there's a big discussion going on about computer ergonomics because apparently a
lot of people your age are reporting risk problems
how many people have wrist pains regularly how many people have wrist
pain sometimes okay that's serious speaking as an old guy
with problems in this respect it is way way easier to not get repetitive stress
injury in the first place than to fix it later so the first twinge of wrist pain that
you have go over to tang and see a doctor about it and change the way you
work on computers we think we the world think that mostly people
you're ready to have wrist problems it's because the video games not because of computer programming but the same
principles apply the most important principle is take a break every half-hour every 20 minutes something
like that other important principles there's actually two pages of ergonomic
stuff at the back of course read your volume to which you should read take that as homework but one thing is how
many people use a laptop is your main computer Wow okay laptops are an ergonomic disaster
because either the screen is too low or the keyboard is too high so I mean
that's okay for you know out in the field like us but when you're at home working on your
computer you guys with laptops should invest in at least one of an external
keyboard and an external monitor you can get external keyboards and then put your
laptop up on top of a cardboard box let's lie down on your desk so that your eyes are pointing straight ahead or put
a monitor on a cardboard box and have the keyboard down at your table so that your arms the top part of your arms are
up and down and the next part of your arms are horizontal and this is more or less a right angle a little bit more
than a right angle so anyway economics and do wrist exercises and stuff like that
please don't develop repetitive stress injury it's a really bad idea okay
last thing of this sort last time
understandably about a million of you came rushing up to the stage at the end of class to ask questions that's really
not a good idea because there's another class coming in I'm going to hurt you to
get things put away and get out of their way and I get kind of snappy with you so
there's two kinds of questions if what you have is an administrative question like can you sign my form or something
come to my office that'll be better because there I can look you up on the computer and see what your situation is
and all that if you have an intellectual question stick your hand up in class and ask it the two reasons I think that
people don't do that one is those of you who were brought up polite to your elders are afraid that I've made a
mistake and you don't want me to look bad so it's okay if I have in fact made
a mistake which does happen you know once over here the semester or so I would much rather that the whole class
hear about it then that you all go away thinking the wrong thing or being confused because what I said didn't make
sense so if you think I'm wrong about something stick your hand up the other reason people are afraid is they think they're going to ask a stupid question
so here's the story about stupid questions what's the very worst thing
that can happen because you stick your hand up and say something stupid in class here's what it is you stick your
hand up and say yes you say something really stupid I give you a sarcastic
answer everybody laughs at you and you see like an idiot okay that's the worst
thing to happen doesn't it happen every evening in the dorm anyway
whereas what if you don't stick your hand up and ask the question or say the stupid thing what's the worst that can
happen then well you go on not understanding whatever it is you failed
of course you drop out of school and you spend the rest of your life on Telegraph
Avenue asking for change so it's really worth asking the question during class
instead of coming up afterwards to ask it okay on your homework yeah your name
your login your TAS name it I said this I think last time but let me say it again the physical piece of paper that
you turn in for homework one is the way that each reader knows which students he
or she is responsible for grading so if we can't figure out who you are from the
piece of paper nobody is going to gray your homework and that's another way to flunked of course so that's important do
all that stuff okay big lad just one
more time quickly the crucial point here is that this is a recursive call we're
calling the same procedure that we're writing how can that work well the right
way to think about recursion is this inside the computer there are a lot of
little people that's how computers work and each
little person is an expert on doing something so we have you know member
question mark experts and but first experts and word experts and if experts
and we have piggle experts and when you make a recursive call what you've done
is you hired Peter to do piggle of scheme and Peter hires Paula to do
piggle of teams and Paula hires Paul who
hires Pamela right and each little
person has its own idea of what the task is and finally one of them has a task
where the word starts with a vowel and then that one reports back to the previous one who reports to the previous
one and so on so that's the way to think about recursion and then it doesn't seem like you're cheating you know um what
you don't want to do this is really really important any time the words go back appear in
your head as in you say piggle down here and it goes back to the beginning route
that out if you think like that you're not going to understand recursion you'll be confused and you know your life will be erect
okay the other thing I said about this example is that if is a special form
that's important because when we get to the base case namely PL dun returns true
we want to compute this non recursive thing and we don't want to compute this
recursive call whereas if if we're an ordinary procedure the waste scheme handles
procedure calls is first it evaluates all the sub expressions so it would do
the recursive call before it realized that we're down at the base case so if has to be a special form so that only
one of the two branches is actually taken ok that's sort of where we left
off last time now somebody came up and
asked me this question just before class and I promised to answer it luckily it's the next thing in my
lecture notes computer science is kind of the wrong name for our field because
it's not a science and it's not about computers it's not a science because
what scientists do is ask questions about how the world works for the most
part what we do is much more like engineering where we take as given how
the world works and we build stuff right and the stuff that we build is software
but it's the building not the finding out that's important that's not entirely
true because part of computer science is theoretical computer science in which we
do ask questions about how the world works and surprisingly least it
surprised me when I learned it these really abstract things that consider computer programs actually obey certain
rules so you will learn that certain problems that just cannot be solved by a computer program period it's not a
question of the computers too slow even in principle if you had the fastest computer in the world you know times of
Dillion you still couldn't solve the problem that's an interesting thing
and that's a kind of finding that out was the sort of exploring the world and asking questions about it but mostly
what most of us spend our time doing is really engineering rather than science
and the other half of it is a computer science isn't about computers the field
that's about computers is called electrical engineering those are the guys who build computers and understand
how computers work and stuff like that we build software so what our field
should be called is software engineering but unfortunately that term is taken for
a particular sort of philosophy about how to do computer programming so if you
say I'm a software engineer there's a whole lot of baggage ideological baggage that comes along
with that name in non-english speaking countries there's a word informatics it
sounds kind of you know frou-frou in English but F o matic is just the word
in French and so on in most of the world's latin-based anyway languages and
that would be a good word for a field too anyway so that's the deal about computer science so what exactly is it
why do we need a whole field about this when I was an undergraduate there was no
such thing as a computer science major so I was a math major and some of my
friends were EE majors and that basically was the choice that you had if you were a geek you know there wasn't
computer science and you know we wrote computer programs anyway and we just sort of forged ahead and did it and the
deal is this is kind of a secret so don't tell anybody but computer programming is like the easiest thing in
the world that people get paid a lot of money for computer program is so easy as
long as the program that you're writing is small so the can all fit in your head at once which
is how it used to be in the old days you know because computers were small and they were big physically they took up a
whole big room that they were small in capacity and so you could fit your whole program in your head and they hadn't
invented window systems yet which helped a lot but once you're writing a big
program which basically all programs are now in the sort of graphical user
interface world you can't write a program to add 2+2 anymore without first
saying well let me pop up a window and let me make it a text window and we put a scrollbar on it maybe a little go
button you know and then we'll put for an answer you know so programs are all
big and complicated and what computer science is about is the control of complexity okay so another thing you
could call our field is complexity engineering and how do we do this
control of complexity thing well there are two answers to that the
old-fashioned answer is you go out and hire 5,000 programmers and you put them
to work on this program and that was the way people did it for a while and what
they found out the companies that tried this is the more people you put on a project the longer it takes so instead
what we have to do is somehow build our ideas out of bigger chunks so instead of
thinking about every little detail you can think about big chunks of things and that way you can fit the whole program
and you have the whole structure of your program and those sort of bigger chunking techniques are called
programming paradigms and that's what this course is about programming paradigms and there's a list on the
board which I'm not promising is complete in terms of the world but it's
complete in terms of this course this is what we're going to be talking about right now we're doing functional
programming we'll do that for a month or two and then we're going to do object-oriented programming for
another chunk of time that one you've heard of I'm sure and the last two we're
just going to touch on briefly client-server programming and declarative or logic programming not
because they're not important but because there's only so many weeks in the semester we want you to know they exist so you know we can't actually
teach you the entire contents of computer science hard as I try just in
one semester so those are programming paradigms the programming language people by the way these days tend to say
that you shouldn't talk about programming paradigms anymore because the way people really write programs
take something from this or something from that and mixes them together and that's all true but that's a good way to
think about it once you understand what the programming paradigms actually are so for now we're going to start as if
you did everything queue early one way or another okay
this picture behind me is a picture about abstraction abstraction is one of
the central ideas of this course the book uses the word a lot but never
really quite defines it and in a way that's too bad because the technical
computer science meaning is a little bit different from the ordinary you know
conversation with your friends back home meaning so behind me is a chart of
layers of abstraction and at the top we are writing an application program and
we do that in a higher-level language of which scheme our language the semester is an example high level languages are
implemented in terms of lower-level languages low level is not an insult it's not high as good low as bad it's a
low level language is one that keeps the
way the computer actually does things in your consciousness so you're really thinking about okay where exactly is
this in memory things like that whereas a high level language tries to hide all that under the rug and
let you think only about the problem you're trying to that's the difference a lot of you will
spend a lot of time working in Java which is a kind of medium level language that's high in some ways alone others so
these aren't rigid boundaries but nevertheless low-level languages are implemented in terms of the language
that the hardware actually understands which is machine language which is coupled with an architecture
architecture is sort of electrical engineers way of looking at that same level of abstraction it's sort of what
pieces do we put together and what arrangements in order to make a machine that understands this language so they
talk about things like well does the memory over here and here's the arithmetic units on those things are
done in terms of logic gates which are circuits that compute boolean functions
true/false functions the reason those two false functions are so important in
building computers is that you can represent a true/false value on one wire okay so all the big more complicated
things like doing arithmetic on numbers are built up out of a bunch of little one wire logic gates logic gates and
term in turn are built out of transistors from our point of view a
transistor is basically a remote controlled switch but the way it actually works is a little bit more
complicated and electrical engineering people teach you about that if you really want to understand how a
transistor works it's built on top of quantum physics is how the behavior of
subatomic particles are what make transistors do what they do so each
layer of abstraction is built on top of the one underneath it most abstract
least abstract the way people talk about abstraction in sort of normal conversation the at the less the
opposite of abstract is concrete as in something you can hold in your hands so
an ordinary conversation people would say well the computer is something I can hold in my hands and a lot of people
actually try to understand and computer programming starting from there let me take this thing I can hold
in my hands and then I can build on top of that the different programming techniques or I can look underneath it
to see how the circuitry is built and so from that point of view the things that
are abstract are the extremes abstract kind of means weird right so quantum
physics that's as weird as it gets right and higher-level languages are pretty weird all your friends will tell you why
are you using this weird language for example your computer science class when
we say abstract we don't mean weird yes
yeah abstract abstract means built on top of other pieces okay so we take
pieces we put them together we actually don't use abstract that much as an adjective we talk about an abstraction
which is a way to take little pieces and put them together into bigger chunks
that we can then treat as black boxes okay so the standard example people
always use is under the hood of your car what is there there's like little hunks
of sheet metal and little hunks of metal curlicues and stuff but you don't
ordinarily think of it that way you take a bunch of those things and put them together and say this is the engine right this is the alternator this is the
transmission that's what we're doing in abstraction is we're making big pieces out of smaller pieces does that answer
what
yeah abstract versus something you can hold is the sort of laypersons version
of abstract our version is built on top of something else okay so for ordinary
people the picture goes abstract less abstract less abstract concrete more abstract more check marks track from our
point of view down at the bottom is fundamental building blocks and then we
have more abstract pieces and more abstract and more abstract and more abstract and we're done okay all right talk to me later I'm not
getting your question okay um okay that's my writing on the chalkboard for
today oh yeah what's a function we're
doing functional programming we should know what a function is um you know what a function is you learned in high school
where we said X equals 2x plus 6 right
that's a function and probably your teacher drew a little box like this put
like 2x plus 6 on the box and you can put like I don't know 76120 yeah good
and if your teacher was a better artist than I there was maybe a crank on the side of the box that you could turn you
know so that's a function that is to say it's a relationship that has zero or
more inputs and has one output right and
what makes it a function is every time you put in the same inputs you get the
same output so this function if I put in seven and I got out 20 today tomorrow if
I put in seven I'm not going to get 46 I'm going to get 20 again regardless of
anything that might have happened in the meantime okay
so why does that matter so much what's why is function why is the idea of
function important to us and the answer is twofold one is functions are pretty
well understood by theoreticians and it's easy to do reasoning about a
computer software system that's built functionally so we can prove theorems about functions and stuff like that
that's one reason the other reason is these days computers are doing more than
one thing at a time that's always been true because of time sharing that the
computer would run your program for a tenth of a second and then run a different program for a tenth of a second and so on
now it's especially true because you buy computer and inside the box there's two
or four or eight processors in one chip right there they're called multi-core
processors they do that because for like
four or five decades every year they made the computers faster and they're
pushing limits not really fundamental speed of light kind of limits the one
that we're pushing on right now is temperature so it turns out the faster
you make a circuit the more heat it generates and we're at the point where little chips melt if we try to make the
computers run faster so instead of that we make computers run a little slower but we put bunches of them in one chip
because they are getting better at cramming more circuitry into the same amount of space so if your program is
doing a bunch of things at once and if the behavior of this piece of the
program depends on what some other piece is doing you can get in trouble later on
we're going to look in more detail about the nature of that trouble but for now the important thing to understand is if
your program is entirely made of functions this function by definition doesn't care
what the rest of the program is doing is nothing about the sort of larger state
of things in the computer that effect the fact that this function applied to seven gives the answer twenty so if you
use functions in your programming you can much much more easily get a program
running in a situation that involves parallelism and that's really super important these days so until a few
years back people kind of looked on functional programming is something that only professors cared about and we don't
use that in the real world but because of parallelism people out in the real world are starting to pay attention to
it as an important idea okay okay take a
vote question is our F and G the same function or different who says the same
this is different some of each okay trick question we are going to say they
are the same function but different
procedures they're the same function
because a function doesn't really care what's inside the box it cares if I put
in seven what answer do I get and it's 24 both of these trying the same for any other value of x
that you put in so as a function they behave the same way a procedure is a
sequence of steps for computing a function f says take the argument
multiply it by two then add six G says take the argument add three and multiply
by two so it's a different sequence of steps different procedures to compute the same function um
inside the computer there aren't really any functions there's only procedures okay
so the way we represent the function in a computer program is to provide an
algorithm a sequence of steps for computing that function because of that
it's kind of like what I said about the different kinds of names for arguments last time because of that almost always
I will use the words function and procedures if they meant the same thing
but every once in a while it's important to call attention to the difference and I'll say well these are the same
function but they're different procedures or something like that and you understand what I meant yes right
what he's asking what if the function were to X plus B instead of 2x plus 6 so
we had what we call a free variable a variable that isn't an argument to the
function ah and so it does depend on what's going on outside for what the
value of that variable is the answer is if that's the case it's not a function okay it's still a procedure but what it
computes is not a function because you don't always get the same answer for the same argument okay good question is that
clear what he's asking what the answer was good yes
ah could there be a function for which
different procedures take different amounts of time yes absolutely we're going to talk a little bit about that in
two weeks and it is them one of the main topics of 61b for the most part in this
class we don't worry about efficiency most of the time and you know to an
engineer that's kind of horrible but the reason is um in practice even it's a lot
easier to take a program that works and figure out how to make it faster than to
take a program that's fast and figure out how to make it work so we're going to concentrate on how to get a program
to compute the answer you want and later on you'll think about how to do it faster okay okay
moving on I hope
okay who knows how to play buzz not very many people God you never had childhoods
or something okay so you're sitting around the campfire alright what you
know waiting for your marshmallow to get hot and you start counting but if the
number that you're up to is divisible by seven you have to say buzz instead and
if it has a digit seven you have to say buzz instead alright okay go you to see
buzz good
this game okay nope buzz okay get it alright so here's
this procedure that plays buzz and the way it works is you give it a number
like you say buzz 15 and it says 15 you give it buzz 17 and it says buzz okay
how does that work look up at the top half of the screen it uses conned conned
is an alternative to if that's designed
to be easier for situations where there's more than two possibilities so
in this case there's three possibilities
represented by this con clause this con clause and this con closed those three
okay so what's a con clause the reason I want to take a minute to talk about this
is that the notation boring flow is a little unusual I remember I told you
last time there are a handful of situations in which parentheses means something other than call a procedure
and this is one of them so the way it works you say cond and then a clause not
clause and so on how many causes there
are those are ordinary parentheses but what's a cause a clause is parenthesis a
test and an action
these green parentheses do not mean call the procedure test with the argument
action these are the ones that are special now test and action may involve
procedure calls so test could be function argument argument etc and
action might be typically is in fact function argument argument etc so when
you combine all of this and collapse it into one thing you see cond
yeah up nope great what's it called it's
called in okay because the notation is
like this you're going to be very very very tempted to say oh the way cond
works is in each clause you have to say open paren open paren it's like they're
double parentheses are in a conquest please don't think like that you have to
think the green parentheses is special and then this parenthesis that comes right after it is a plain old scheme
procedure call parentheses okay any questions about that yep
yes Conda is a special form and the way it worked is it starts with the first
Clause evaluates the test if the test is true then it evaluates the action part
and it's finished whatever action returns the whole cond returns and it never looks at the other clauses if the
test returns false you go on to the next clause do the same thing and then at the
very end this word else here maybe I should have done that in green also it's what's what's called a key word it's not
the name of a procedure or anything it only is meaningful inside a cond clause
and basically you can think of it as meaning true so it would work perfectly
well if they just had a variable named X whose value was true because this test
always succeeds so if none of the other things work then we do that so the order
of clauses within a cond matters you have to for example if you're doing base
cases for a recursion the base case tests have to come before the thing that does a recursive call otherwise you
won't find out that it's the base case yeah do you have to have an else at the
end of the cond technically no you don't if you don't the return value is it says
in the standard unspecified which means every scheme system does something
different okay some of them actually return number sign unspecified but some
of them return something else so basically the short version of that is
yes you can but don't okay good I think
we'll make it um if I skip over all this stuff about recursion and go right to
normal on applicative order so remember I said that when we do a procedure call
and scheme step 1 is evaluate all the subjects
questions so that you turn actual argument expressions into actual argument values and then we give the
procedure the actual arguments values by substituting the values for the formal
parameters in the body of the procedure so that way of doing things is called
applicative order what scheme does it's not the only way of doing things there
are bunches of rules you could have another important one that we're going to be revisiting later is normal order
evaluation in normal order when you call a procedure you take the actual argument
expressions and substitute them into the body and we don't ever actually evaluate
anything until you call a primitive so your procedure calls it for helper procedure that calls the helper
procedure that calls Plus that's when the arguments get evaluated okay so I'm
going to whoops I'm going to load in a
little scheme interpreter namely
forgotten and it doesn't say in here wait a minute okay
order okay so I'm going to define a couple of
functions just like in my lecture notes oh it does say I just missed it for blind deaf is like the define for this
special scheme system that I'm about to show you so pretend it says define so F
of a and B is plus G of a B and G of X
is x 3x and now I'm going to do in
applicative order F of plus 2 3 and
minus 15 sex
- all right so what happened up at the
top here is the actual expression that I
typed in and we're going to watch sorry the process of evaluation as it happens
so in applicative order what scheme actually does we start by evaluating the
argument sub expressions so I evaluate plus 2/3 and that's actually complicated
- we have to evaluate plus sign and evaluate - and evaluate 3 but those things are easy and so we finally get 5
we evaluate 15 minus 6 and get 9 and now
we take the actual argument values and call F with those values so first
evaluate the argument sub expressions then call the function so here's the
body of F substituting 5 for a and 9 for
B let's see can I get the definition of s up here yes I can so here's F of a B
is plus G of a B so we're doing plus G
of 5 9 you're comparing the very first line on the screen with the one where the cursor is blinking okay so you see
how we substituted actual argument values into the body of F and now this
is a new expression to evaluate and we start by evaluating sub expressions so I
have to do G of 5 well the value of 5 is just 5 so I'm not showing that step and
so we substitute 5 for X in the body of G we get instead of times 3 X we have
times 3/5 the value of that is 15 and finally we can add 15 to 9 and get 24
and here's the answer 24 ok now we're
going to do it again in normal order bang
okay this time I'm not going to start by evaluating the argument expressions I'm
going to take the actual argument expressions and plug them into the body of f the body of F was plus G of a B so
I'm going to make it plus G of plus t3 minus 15 6a s plus 2 3 B is minus 15 6
now plus is a primitive it's an arithmetic operator it actually needs
numbers to work with so at this point I'm going to evaluate argument expressions the first one is G of plus 2/3 G is not
a primitive so following the normal order rules we take the actual argument expression plus 2/3 substitute it for X
in the body of G we get plus I'm sorry we get x 3 plus 2 3 times as a primitive
so now I figure out what plus 2 3 is it's 5 we do times 3/5 that gives 15
minus 15 which is 9 and 15 plus 9 is 24 I get the same answer in a different
order ok so if we get the same answer
what difference does it make well here's the case where it makes a difference
so I'm defining a function called zero takes an argument X it computes X minus
X so the answer should be zero right
okay so let's do in applicative order I'm going to do zero of random ten
random takes a positive integer argument and it returns a non-negative integer
strictly less than the argument so some number between zero and nine so here's
what happens when I do this oops that wasn't supposed to happen
okay why did that happen oh whoops all
right never mind let's just start again def here I said Z here okay mine is easy
thank you that's interesting all right a flick of Rand 10 no app lick
of zero of random 10 this time for sure
okay so in applicative order we evaluate the argument expression first random 10
happen to give us the answer 8 so now i compute 0 of 8 substitute 8 for Z in the
body of 0 I get 8 minus 8 which is indeed 0 now let's do normal of 0 of
random 10 oh look at that in normal
order I substitute the actual argument expression for the parameter in the body
so that gives me instead of minus VZ I have minus random 10 random 10 ok so now
I'm doing - which is a primitive so I need a value so i compute random 10 I get the answer 8 that can be random 10 I
get the answer 1 8 minus 1 is 7 and that's my result so here's a situation
in which it does matter if you use normal or applicative order how come now
let's not always do the same and yep
yeah random doesn't always give the same answer every time we call it or in other words random is a procedure that is not
a function right the answer to you call random with the same argument you don't
always get the same answer so it's not a function this is just one example but it
generalizes it turns out if you write correct functional programs purely
functional programs then you get the same answer no matter which evaluation
order you use if you do something that isn't functional then all of a sudden it
matters what order things happen in inside the computer ok so again we're
going to come back to normal order will see uses for it later on but for now the takeaway point is that functional
programming protects you from having to think about what's going on when inside
the computer alright see you Monday