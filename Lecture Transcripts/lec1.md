Transcript


all right how are we doing you hear me hear me yeah good okay welcome to
computer science 61a uh the best computer science class in the world um
and I'm allowed to say that because it's not because of me it's because of this book uh which is called structure and
interpretation of computer programs uh which uncoincidentally is also the name
course that you're taking um best computer science book ever written uh you're going to learn an awful lot um
okay uh we're using a programming language called scheme I want to emphasize right at the beginning that
this is not a course about scheme in fact you're going to learn all of scheme in the next
hour and then we can talk about Big Ideas we're using a particular implementation of scheme called
STK um here it is and um
I should have got ready ahead of time here okay and we can type stuff into it and the way it works is you ask it a
question it tells you the answer so I say six it says
six um I say plus 6
8 it says 14 um you'll notice in passing that this
is not the way you were taught to write addition problems in grade school um the
reason that scheme uses this notation is that it can use it
uniformly so in math there's infix
notation with the operator in the middle for some things and then there's
oops then there's prefix notation for other things and
then there's postfix [Music]
notation and
then all around the operator or the operand I mean notation for yet other
things um so this is not very uniform and also hardly any of these work very
well if there more than two oper so we standardize on having the
operator first and that means I can say what's the sum of six and 8 and two and
99 and 4,000 and it'll work
okay what do you think four
yeah what do you think ah here's some errors and some zeros
it's actually zero um but
times one um because that's the identity element for the multiplication operator
so it sort of makes sense mathematically to do that um some other operators
um don't like doing that so it's not every function that has variable numes
yeah VAR able numbers of arguments you can't call division with no arguments um
how about if I just say plus not in parenthesis error nope um I know that
looks like it might be an error message but it isn't um this is the way that's
STK represents functions so the value of the symbol
plus sign is a function the same as uh you
know you always learn that you know s is a function um so it's
plus okay um good what if I would like to have an
expression whose value is the plus symbol I can do that as follows um I say
quote is the bottom showing up yes great um quote plus sign uh that I don't know
if you can see clearly back there in the back but it's actually a single quote otherwise known as an
apostrophe um and quote followed by any word the value of that is just that word
so if I say hello I get an
error so I'm asking what's the value of the symbol hello and there isn't a value
but if I say quote hello I get back hello
okay question so far great um we can take the result of
one function and use it as an argument to another function so I can say add
up 3 * 7 and 10 *
10 okay that's called composition of functions you learned about it in seventh or eth grade um
and it turns out to be such a powerful mechanism for organizing computations
that it's basically all we need so you now know uh we're like 15 no
we're five minutes into the class you've now learned about 90% of the scheme
language okay namely parenthesis function argument argument
argument argument however many there are close parenthesis means call this function with these argument values okay
um and what scheme does is first it evaluates the argument Expressions so it
evaluates for example time 37 gets 21 it evaluates time 10 10 gets 100 and then
it calls finally the plus function with those values okay so first evaluate the
arguments then call the function with the actual argument values
that's it that's the language um well almost um first of all not all functions
are functions of numbers um I can say something like first of quote
hello and get H or last of quote
hello get o or but
first quote hello congratulations on not
laughing get l or but last oh hello they wouldn't let
me do this if we were teaching in Texas
um uh we can abbreviate these things by the way but First's BF and so
on okay so those are functions um there's a Constructor function called
word here's my favorite example now and here combine them and it
just sort of butts them up together makes a new word that's the two concatenated um there's also sentence
which you can abbreviate SE and it makes something we haven't
seen before which is a sentence which is a bunch of words in
parentheses okay um now notice this is something scheme is printing out as a
result this sentence if I were to type in parenthesis now here close
parenthesis that would not mean I want the sentence now here it would mean
please call the function named now with the argument named
here okay if I actually want a
sentence I quote it the same as you can quote a
word okay
um first but first last but last applied to sentences carves out pieces that are
words so but first of
um all but the first word
okay and these can be composed also so I can say uh first of but first of
um we got oops oh
sorry programming and Logo to there we go so first of butt first
what does that do well butt first of A Hard Day's Night is Hard Day's Night and
first of hard days night is hard right how about first of first oops
I keep doing it first of first of but first of
um he loves you what am I gonna get L yeah first letter of the first
word of all but the first word oh she loves you okay great
um can you guys listen and hand and pass out handouts at the same
time without reading the
handout just T them
around if you're really smart we can do this in order of the end
time
just going to start this halfway back
last
you go that was only
box all right tell you what could you take these and just pass
them straight back until they get like four rows from the end and then people
should start
taking and same for
you and
okay the first row that doesn't have handouts can start this one when it gets to you straight
back and you don't get very many do
that and
that's
okay the other 10%
language uh we can give names to things so I can
say
for now if
I and here's the area of a circle of radius
5 um I can
Define procedures and that
than there we go oh wow so loud um usually by convention you just go to
another line to put the defin the actual body of the procedure but it's only a
convention a scheme treats a new line the same way it treats a space it's just a separator
um oops so now um I've defined a procedure
by the way notice when you say Define what you get back is um as The Returned
value is the name that you're defining so um up
here I defined pi and it it said pi and here I'm defining square and it says
Square um so what does this mean it means when you call square with an argument like if I say square
of plus 23 what happens
first plus 23 first thing we do is evaluate
the sub Expressions to get the argument values now we're also by the way
evaluating this sub expression whose value is the function we're calling so
we get the value five good um and now in
the body of square which is this expression here wherever we see an
X we put in five and so we get times 55 and that's
25 okay um so that's the rule of uh
evaluation for scheme almost always um there are a few
exceptions uh one of the exceptions is Define itself because when I say
Define pi at the time I say this Pi has no
value so if this used the ordinary procedure calling rule of first evaluate the
argument expressions and then call the function I we get an error on this call to Define Unbound variable
Pi um and the same here um Square X well if I haven't
defined Square yet this doesn't mean anything and this although it looks as
if it means something it actually doesn't until we
substitute some value for this these X's right so Define is what's called a
special form um actually technically the whole expression that you type is called a
special form Define is called a keyword um which is the name of a special form
and what's special about it is that it doesn't do this thing of first evaluate the arguments
Etc um actually it depends which kind of Define and
you'll learn why this is in a week when we look under the rug here under the hood of this but if I say Define hello
to be + 23 uh the value of hello is five right
it's not plus 23 this got evaluated if this we're inside
parentheses then we'd be defining a function and then nothing would be evaluated until we call the function
okay great um there are oh maybe a
dozen um they say in teacher school you're supposed to say any phone that rings in
my class is mine but um I'll let you off the hook this time
[Music]
um oh yeah Special forms there's about a dozen of
them um Define is the first one that you're learning and we'll see a couple more um as this week progresses okay let
me take uh a couple of minutes to talk about administrative things
um what you need in the way of materials for this course you need the handout
that I hope you just got who doesn't have a handout okay anybody who has more than
one hand out there send them that way to the top right your right here they come
great um so you need a handout you need another handout that you're going to get
in a minute um you need a computer account form and I'll talk about that in a
second those are the things we give you and then there's some things you have to buy uh the most important one is the
textbook um you can buy it used if you want if you do make sure it's the second
edition not the first edition um Second Edition that out for a long time so it probably is but check
um in my opinion you're going to want to keep this book forever and sleep with it under your pillow um but you know there
is a used Market because I guess not everybody agrees with me um there's also a course reader it comes in two volumes
a thin volume one and a thick volume two uh the reason it comes in two volumes is
that you have to get a brand new this semester's volume one for
$941 but if you find a used volume two that's okay volume two is the stuff that
doesn't change from semester to semester um you need the volume one because it
has all of your assignments for the entire semester are in here all the labs
all the homeworks all the projects in here um so that's important what's in
the big fat one one thing is my lecture notes so my goal is that you shouldn't
have to write stuff down in here um and that's because I vaguely remember being
a student and I can't think and write at the same time and I want you to be
thinking in here okay so you get my lecture notes you can read along if you
know I seem to be saying something that isn't quite in here or a clarification you can scribble it in the margin but
mostly you should be listening and thinking and not writing um another
important thing that's in here is the scheme reference manual so if you have a question about you know what's the order
of the arguments to such and such uh you can look it up okay
um other really important things in the big volume um
is some sample exams so you can get an idea of what the exams are like there
are way too many exams in this course we give three midterms and a final I keep trying to cut back and
students always insist that we have to do this which sounds kind of masochistic but the reason is the fewer
exams there are the more it matters to your grade if you totally mess up one problem so students like to have a lot
of problem s to sort of smooth out their errors in the midterms um so that means
that the Tas and I are pretty much constantly either writing an exam or grading an exam um which is the only bad
thing about teaching in this class oh that and arguing with students of back grades that's another bad part
um okay uh let me hand out the other handout actually it's only one page this is the
last minute
update so here you go pass those around pass those around
um what's in the last minute update uh mainly is information about uh
which ta is teaching which section um when and where they meet and the all
important which sections have rooms so if you are on the waiting list for this
class or if you're an extension student and want me to sign you into the
class the answer is we have enough spaces for
everyone okay everyone will get in provided that you are willing to meet at
a section time that has openings okay so you have to meet us halfway about this if you absolutely
can't meet any of the section times that have openings you can attempt to make a
trade with someone else um and there's two ways to do that
one is to just sort of show up at the section you're trying to get into and ask the TA if you can just yell out um
hey can anybody take Section such and such that I'm enrolled in but you should enroll in a section even if you don't
like the time enroll in one of the open sections that will get you into the class if you want me to sign a
form because you're an extension student I'm not going to sign your form until a TA signs at first saying that you're in
a lab and discussion section okay um so I want to make sure
that everybody's really in a section it matters a lot um the lab and discussion sections you
probably all figured this out already are linked so if you're in lab section 15 you're in discussion section 115 they
go together um and it's the same ta and the same students and that's good
because you're going to be working in small groups and you really get to know your partners so a week from now your ta
is going to organize you into groups of four and you are really going to get to
know this group of four very well because you're going to collaborate on some projects you're going to
collaborate on some exam questions there will be a couple of group questions where you're whole group getss together
to we got the answer to something I really recommend that you study together um and please do your best to
make sure that nobody in your group gets lost and dispares and drops out okay try
to support your group members why because your entire group gets bonus
points if the lowest scoring person on an exam from your group G gains Five
Points in the next exam okay so if you can take your sort
of weakest link in your group and support that person to really do better
uh you get two bonus points if that person drops out you don't okay so this is a reward for
working together um having said that there are limits to
your working together um you're going to be hearing this from every single instructor this
week right you probably already heard it six times don't cheat
um I think that some of what people tell you about this is nonsense uh for example people will tell
you that you're hurting your fellow students by cheating uh that would be true if this
course were graded on a curve but it's not um grading on a curve is evil
because it makes you compete with each other instead of cooperating um so you are not hurting
anybody else by doing well in the class another thing that I've heard people say that isn't true is that you are going to
harm the reputation of the University of California if you
cheat now come
on every three or four years some football player rapes a Towny at a
fraternity party and that's terrible but the
reputation of the University of California is pretty good
um so that's not why you shouldn't cheat here's why you shouldn't
cheat you guys right now are constructing the person you're going to
be for the rest of your life um human behavior is mostly a
matter of habits people talk as if you make big decisions all the time about what to do but that's not true almost
all the time you just do what you're in the habit of doing if you get in the habit of cutting
Corners this early in your career you know how are you going to
make it through the harder upper division classes and then what are you
going to do when you actually get a job and the person next to you isn't doing the same thing you're doing okay you're
not going to be able to look over somebody's shoulder but you are going to be able to find ways to cut corners and
I don't want to fly in an airplane that was programmed by somebody who cheated in this
class okay so really and furthermore
what's the best thing that can come out of cheating you
uh condemn yourself to a life of doing something you don't know how to do and
don't like doing okay so don't cheat if you do you're really hurting yourself um and
the thing to do instead the way to avoid cheating um in this class I don't
believe we've ever had the kind of conspiracy you read about in the newspapers where somebody breaks into
the professor's office you know and blah blah that doesn't Happ what happens is people panic at the last minute and
cheat the way to avoid that is if you don't understand something don't think I'm going to wait
till next week and see if it gets better don't think I don't want to bother the poor
Professor uh it's what I'm here for come to my office hours come to your ta's
office hours the very minute you don't understand something okay good so don't
cheat um other administrative things if you're in
section 20 and 120 I really apologize for the fact that the lab and discussion
times are half an hour offset from each other um it's a long story um but was
the best we could do um and the csua help sessions that you
were told about right at the beginning are at the very end of this onepage last minute
handout um
okay uh that's it all of your other administrative questions are answered in this
handout so I would prefer not to have administrative questions today you can
ask administrative questions on Friday if the answer is in this handout you owe me a
dollar okay I don't feel that way about course
content questions if you ask the very same question that somebody asked a
minute ago because you didn't understand the answer that's fine okay don't refrain from asking
questions because you think it's a stupid question stupid questions are the best ones because if you have a stupid
question then probably 50 other people in this room have the same
question whereas if you ask uh I'm going to prove how smart I am question then
you know you won't make any friends um
all right let's get back to work
yeah oh uh okay are there last minute handouts to pile them
somewhere on the back okay hands up if you don't have one okay so people who have the big pile
pass it for some of it that way and some of it down here okay we should have just about
enough I I hope uh if not we'll make more
um oh let me write this down one administrative thing that I should have put in the hand out but I'm not sure I
did Jenny is the staff support person for this class among other things and if
you're missing a handout or something um you know you need to reschedule exam
she's the one to see um okay back to
work oh yeah
so
okay here's your vocabulary lesson for today this
thing is called a formal parameter
you don't have to write it down it's in my electron notes just understand it so
the formal parameter is the name for an argument to a function
right um this thing here is the
body okay those things are part of the definition of a
function
this is the actual
argument expression and then a sort of invisible
thing is the actual
argument value which is five okay so there are three things that
can Loosely be called the argument of the function there's X which is its formal parameter there's plus 23 which
is its actual argument expression and there's five which is its actual argument value almost all the time
either it's obvious which one I mean or I kind of mean all of them together and I'll just say the argument or the input
even um when it matters those are the names and we'll try to be clear about
that okay oh yeah about asking questions um they uh because they're
webcasting this and everything they're shining bright lights in my eyes and so um I might not be able to see your hand
in the air and if that's the case wave it around um this is this is your
physiology lesson for today uh your eye sees moving things a lot better than
stationary things um so I really can see your hand better if it's moving uh if that doesn't
work yell um
okay so here's a typical function that you might Define so I can say plural
computer here is plural
book plural Point notice I'm quoting the words that I'm using as
inputs because quote computer is the actual argument expression and computer
is the actual argument value or book or boy okay
um well there's a problem with this it doesn't quite
work that's the wrong answer right so I'm going to fix
it word oh one little comment before I go on I used WD as the formal parameter
why didn't I just use word it's not just because I'm a lazy typist it's because in the body of plural I'm using a
primitive function called word w r d and
it has to have a different name from this okay a name can only mean one thing at a time so that's why you'll see me
use wood for words and scent for sentences as uh as formal
parameters okay so if what what's different about fly it
ends in a y equal question mark equal question
mark is a built-in predicate function a predicate is a function that Returns the
value true or false okay it's not a rule built into
the language that predicates have to end in question mark it's a convention that they almost always do it just helps you
read programs more easily although it actually in one way makes it harder to read programs you have to say if
equal or something so it's like Chinese where the uh tone
matters um so if the last letter of wood is
equal to quote why last of word is a procedure call but
the Y I actually want the letter Y itself so it's quoted so if those are
equal then I'm going to return word all but the last letter of my
argument word and then I S otherwise same as before word would
quote
s so book still works fly
works but
a broken boy you're going to fix that in the
lab okay um if is a special form
yes okay question is There's no distinction between a character and a string with only one one character in it
um that's right these are my crossed fingers here
um um if you read the reference manual you'll see that there is but for our
purposes uh there are neither characters nor strings there are words and there
are sentences okay yeah
hush a string is a bunch of characters in in those other
languages um
yes is there a function that gives you a character in the middle of a word well yeah
um we found the second character Remember by taking first of but first so
you can make compositions of those to do that um there's also um something made
up of that um let's see uh I think this
wait no it works this way
um no whoa that's interesting Maybe I'm Wrong
maybe there isn't one um for Words good
question oh there's item let's try that item for
quote computer yeah there we go
item um oh yeah thank you for reminding me all the stuff about words and
sentences this is why I had my fingers crossed in your question all the stuff about words and sentences is stuff that
we added to scheme here at Berkeley for your benefit in this class um in sort of
ordinary scheme like in the reference manual uh there's no such thing as words and sentences they deal with text in
different ways this way is better um it's easier uh in a few weeks we'll sort of
see what underlies it uh but for now it's much much easier to think about it this way the idea of words and sentences
came from a language called logo anybody ever programmed in logo huh a few people um used to be more
than that um you're going to get to know it very well uh toward the end of the semester when you write a logo
interpreter um but anyway we've imported this idea of words and sentences from
there and it it just makes life easier um okay um moving
on oh yeah let me do
this whoops CD lectures
1.1 yeah
uhuh uh his question is can I write it my own little reader that lets you leave out the apostrophe
you don't want to because sometimes you really do want to
know what's the value of of this as a symbol or what's the value of this
procedure call um so you really want to make it it's not just a stupid syntactic
distinction it's the difference between program and data basically um and it
really matters so I wouldn't think that way if I were you
um okay so here's a little pig latin program who speaks Pig Latin oh my God what do they teach in
school these days all right um Pig Latin um when I was a kid was a secret
language that kids use to keep secrets from their parents I guess these days it's a language that parents use to keep
secrets from their kids um and the way it works is to translate
a word to Pig Latin you take all the leading consonants move them to the end and add ay so piggle whoops
piggle of scheme for example is
imke so we take the SC everything up to the first vowel up
to but not including move it to the end and add a y okay now how does this
program accomplish that let's take a look it says
if PL done question mark of word in this example we are using a lot of helper functions maybe more than you really
need the if I were writing this for my own purposes I'm not sure I would have something called PL done question mark I
might just put this expression uh up in there but um for purposes of teaching
you how this works we have a predicate function called PL done that takes a word and it asks the
question is the first letter of this word of vowel right we take first of word and
then we add ask vowel true or false now how does vowel work that's not built in
but member question mark is built in so we're saying is this letter a member of
AE I oou if so then um it's a
vowel and so I take the word that I was given and I add a y at the
end otherwise here's the fun part I take all but the first
letter and then I stick the first letter after that so if I'm
given scheme I turn it
into CHS moving the s to the end but that's not the answer I want so
what I do is I ask for pig latin of that okay so the entire expression here
is pigle word but first of word first of word and that will compute Pig Latin of
chims which will compute Pig ltin of hsk which will compute Pig Latin of IM which
will say aha now it starts with a vowel I'll stick a y at the end there was a hand up
yes okay the question was instead of member
here can I use equal question mark right that's where you mean um no you can't um
that letter e for example is that letter e equal to this
sentence no it sure isn't for one thing it's a word not a sentence and for another thing it's just e not
e um so no member is what you want okay
yes oh why did I use letter as the
argument down here oh I use letter here because I used
it here letter is the formal parameter to
proced your vowel question mark okay so when we call vowel question
mark I say like for example vowel question mark of s we're going to substitute s for the formal parameter in
this expression okay so that's why scheme doesn't care
what word you use as a formal parameter um as long as it's not the name of a primitive or something that you need uh
you can use any word you want but you use a word that helps you understand so here my argument is a whole word of you
know many letters here the argument is always going to be a single letter so I'm reminding myself of that by the name
that I picked okay
yes ah what if I use the word Rhythm I would be in trouble because this has a
pretty simplistic sense of what a vowel is that's true it's very complicated to figure out whether Y is a vowel or not
so I didn't do it for purposes of demonstration here but let me get to the important point about this um this is
procedure piggle because we only have a couple of minutes this is procedure piggle and here it is calling itself how
can that work this is the idea of recursion which is a function calling
itself recursive programming is a prerequisite for this class if this is
new to you a procedure that calls itself uh maybe you should take cs10
before you take cs61a okay that's the prerequisite for
61a we assume that this is all old hat to you if is a special form it has to be
because if we evaluated this recursive call before we
called if then even when we got to the base case to the word that starts with a
vowel we would still try to do the recursive call over and over and over again if being a special form it has its
own evaluation rule which is it starts by by evaluating its first argument
expression that has to be true or false if it's true we evaluate the second one
and forget about the third one if it's false we evaluate the third one and forget about the second one okay so
that's if is a special form um
and uh let's see we have one minute left who doesn't have a big
handout who doesn't have a little handout oh geez okay anybody who has
extra handout don't get don't go yet very rude anybody who has extra handouts
please pass them down to the front and people who don't have them will pick them up also you guys should be
listening and not leaving this might affect you um if you are enrolled in one of the
sections that has not had a scheduled lab yet that would be sections 20 and
whose lab meets oh sorry most important thing this week only both section
meetings the one that already happened and the one that would ordinarily be a discussion are meeting in the lab so
this afternoon or tomorrow or Friday morning you're meeting in the lab if
you're in sections 20 or 21 then um your ta doesn't have your
account forms because I just printed some up so people in those sections only I just have enough um should come up and
get I'm going to leave them not on the stage because they're going to rotate it but here um an account form if you're in
some other section your ta has your account forms if you're on the waiting
list but you're going to be in section 20 or 21 then hang around and we'll see if it works okay um see you Friday thank
you
