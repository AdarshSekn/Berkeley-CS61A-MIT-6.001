Transcript


now that we finished learning scheme every week a mind-blowing new idea this
week's mind-blowing new idea is function is data so this is your brain and unless
you're one of the handful of born mathematicians in your brain there's
this big brick wall between the notion of stuff and the notion of actions so
that's why in our languages every human language has nouns and verbs as different categories we talk about
knowing that such-and-such versus know how to do such-and-such and in computer
programming there's this big distinction between data and procedures as to
different kinds of things data is stuff like numbers or character strings or whatever and procedures you know what
procedures are so our job throughout the course of the semester is to try to
break down this wall in your heads but
it really is going to be hard it's something you're going to have to stretch your minds around this wall for
example to take a non computing example this is the reason freshman calculus is
notoriously difficult even for people some people who did well in math and
high school is this sort of big you know hitting the wall about calculus and
calculus students think it's because of details of that you know integration by parts or something but it's not it's
because the integral itself as the thing
is a function of functions so the integral doesn't take some number and
give you at a different number it takes a function like f of X equals 3x squared
and gives you a different function like f prime of x equals
6x right and it's wrapping your mind around this idea that you can have a
function whose argument is another function that makes calculus art it's
also what makes this week's topic art functions as data in the computer programming context so we're going to
sort of inch up on it by starting with a
simpler idea which is generalizing
patterns and remember as we do this I'm
going to show you a very very simple example of it so keeping the backing in mind the reason is we're building up to
procedures as data so up on the top half
of the screen after we define pi there
are four procedures that compute the areas of various geometric figures so if
we have a square of side R if there is R squared if we have a circle of radius R
its area is PI R squared if we have a sphere of radius R its surface area is 4
PI R squared if we have a regular hexagon of radius or side because
they're the same thing in hexagons are its area is 3 root 3 over 2 R squared ok
1 and 1/2 root 3 R squared so we can use these procedures let's stop doing it so
I can say you know circle area 5 and I
get 25 pi which is a little more than 25
times 3 but I don't like the idea of having a
separate procedure for each of those I would like and I notice that there's a
pattern in here what's the pattern of those four area procedures yeah it's all
some number times R squared right because area is two-dimensional R is one
dimensions of crap so here's how I'm
going to do that my original procedures took one argument which was the linear dimension of the
thing my new procedure takes two arguments I've added an argument that's
going to embody what's different from one of these procedures to another so
what's the same is for every shape it's some constant times R squared and what's
different from one figure to another is what the constant is so for a square the
constant is 1 it's just R squared for a circle it's PI R squared for sphere it's
4 PI R squared and so on ok so now I can say area circle 5 and get the same
answer and the same will work for any of these other figures ok so I want to make
sure you get how this is a generalization that the original area
procedure is each one took one argument for the linear dimension the generalized procedure still has that argument for
the linear dimension but now it has another argument that says what's different from one pattern to another ok
any questions about this so far
great okay what makes this a really simple example is that I was able to
capture the differences in just a number right the constant factor so I can
define a circle to just be PI but
sometimes the pattern is a little more
complicated so here I have this is an example taken from the book I have a
procedure that computes the sum of the squares of the numbers from A to B so if
I say some square 3 to 5
I should get 9 plus 16 plus 25 which is
50 okay clear how that works it's a
squared plus 8 plus 1 squared plus 8 plus 2 squared dot dot step 2 d squared
so how does this procedure work says well if there's going to be a recursion
so we have to have a base case the base case is if a is greater than B then
we're not adding any terms at all so therefore the answer is 0 if a is less
than or equal to B then there's at least one term to add namely a so we're going
to add a squared which is this to a
recursive call going from a plus 1 to be
okay similarly we have some cube if I
say some cube from 3 to 5 I get some number that's much too hard for me to
compute in my head namely 216 and that's 3 cubed plus 4 cubed plus 5 cubed okay
yeah what I want you to see about those two procedures is that they're almost
the same namely they both say if a is
greater than B returns zero otherwise add some function of a to a recursive
call for a plus one to D so the only thing that's different here is that in
this case it's the square of a and in this case it's the cube of a okay so I'd
like to generalize this pattern but the
would excuse me the way I have to represent what's different between these
two versions is no longer capturable is just a number
okay these are two different functions so I'm still going to have an extra
argument for what's different but this time instead of a number the argument is
going to have to be a function okay so I'm going to say to find some just plain
old some of some function I'm putting in
capital letters just you can see what's different here and a and B so one new
argument function and then it's going to
say if oops greater than a B don't ask
me why that then return 0 otherwise ad
now I have to take that function and apply it to a right well that's how we
do that to call a function you put it in parentheses along with its arguments so
function of a and then some of function K plus 1 and
be close close close close okay yes
gin the AAP lowercase a this is a
sensible programming language it doesn't pay attention to case of letters sadly
this is no longer true if you look at the latest scheme standard it got
hijacked by Java fans and so they're making identify as case sensitive
but if you have three things in your program called foo and one of them is lowercase fo and one of them is capital
F lowercase o low and the third one is capital F capital o hable oh you're asking for trouble so sensible
programming or just it doesn't matter okay bad habit get out of it they taught
you in high school sorry I'm not making fun of you or
making fun of your high school teacher okay and it isn't even your high school
teachers fault really I'm making fun of the College Board who has the AP curriculum in Java
instead of scheme okay
other questions okay so now I'd like to
use this right there some x-squared from
3 to 5 is this going to work no it's not going to work why not cuz unbound
variable X when I said x XX here remember scheme uses applicative order
that means before it call some it's going to try to multiply X by X but I
don't have an ax I wouldn't help if I said a because there isn't one of those either okay so we have to find a way to
give it a function as an argument rather than a number so right now I'm going to
do that this way I'm going to define a
function Square and now I'm going to say sum Square from 3 to 5 I get the answer
I want it ok please note that there is
no open parenthesis before this word Square you all know right that the
singular parenthesis is not parenthesis parenthesis as is so there's no open
parenthesis before the word Square that's because I'm not invoking the function square I'm just taking square
as a thing and passing it as an argument to some so you see how we're breaking
down this wall because Square started out life over here as an action and now
I'm using it as a thing as data for this other procedure some okay
um yes won't scheme try to evaluate
square yes it will it will evaluate square the value of square is this ugly
thing which is how STK prints out procedures so it's perfectly okay to evaluate square but I'm evaluating it is
not the same thing as invoking it okay what I'm evaluating is the the word squ
a re the value of that word is a function a procedure okay if I say
parentheses square such-and-such then I'm invoking that procedure I'm actually
running it with arguments okay good question other questions okay moving on
the version in the book by the way just backing up to the definition of some
here they add another complexity which
is to allow you to use a function of your choice in going from one value of
the variable to the next so if you want to add up all the squares of odd numbers
between 1 and 10 you could say sum
square function 1 and then the function
of X that's X plus 2 so add 2 function
and then 10 and it would do 1 squared plus 3 squared plus 5 squared plus 7
squared plus 9 squared and then we would try to do 11 but that's bigger than 10
so that would be the base case so that's
just you know an added level of generality that they edit for lecture purposes that try to make things as
simple as possible so this was the simplest way to get a function in as an
argument okay once we have this idea of
function is argument we can use it to generalize many many many interesting
patterns so
so here I have a function evens up at the top of the screen what it does it
takes a sentence of numbers as an argument and it returns the subset of
that sentence that's even numbers so I say evens whoa
okay let's try this again evens quote
three five one four nine eight six seven
and I get four eight six which are the
even numbers out of that sentence so is everybody see what the function does what value it computes good
okay some people aren't coming
if you don't sum then I'm assuming up that's not what you want then we have
thumbs down okay how does numbs added evens work well
it's a recursive procedure so first we have a base case which is if nums is
empty then we return the empty sentence
why do we do that well the range of evens oh yeah I think I forgot to say
this last week the two most important words in the English language are domain
and range the domain of a function is what kinds of things does it take as
arguments the range of a function is what kinds of things does it return as
its result so the domain and range of evens are both sentences so in the case
of an empty sentence I still have to return a sentence and the one that I'll return is the empty sentence okay as
opposed to some other procedure that might have same numbers as its range and
then the base case I might return 0 or 1 or whatever makes sense okay so if we
get down here then the sentence isn't empty so therefore it has a first word
for which in this case is going to be a number and this complicated formula is
just asking is that number even so I take the number I take the remainder on
dividing that number by 2 and ask the question is this equal to zero now as it
turns out I could have just said even question mark first of nums but I like
doing it this way because it's a good example of composition of functions to remind you that the way scheme evaluates
an expression like this is not left to right is not right to left it's inside
so the very first thing that's going to happen is we figure out first of nums
which is in this example 3 and then surrounding that we take the remainder
on dividing 3 by 2 which is 1 and then I
say is that remainder equal to 0 and the result of that is false
ok so for 3 we're not going to do this thing which is the action but for an
even number like when we get to 4 we are going to do this so what is it we want to do if first of nums is either well we
want our result to include first of nums because it's even what else should it
include well it should include all the even numbers of but first of notes so I
had a few people show up in office hours this morning who had the same problem they wanted to say first of Nam's
newline evens uh but first of nums do those two things that's it you can't do
that a function has to return one value so if you're accustomed to thinking
about programming in terms of first through this then do this and do this try not to think that way I think what
is the one value that I want to return and the answer is I want to combine
first of nums on the recursive call into a sentence sentences
the primitive sentence constructor takes any number of arguments they can be words or sentences mixed together and it
sort of strings them out into a sentence so our result sentence is going to include first of nums and it's also
going to include any even numbers that might come after 1st of numbers in the sentence ok and then the third con
Clause is otherwise namely we have an odd number if we have an odd number then
I don't want first of nums to be part of the result ok because we only want even
numbers so I'm just going to call evens on but first of Nam's and whatever that returns that's what
I'm going to return to throwing away first if none okay questions about how
that works yes
sentences as opposed to oh we haven't invented list yet that's Chapter two sorry sentences
sentences that basically um she's reading ahead or she took yesterday or
something lists are a more complicated
data structure sentences okay so the structure is the book the first part of
the book there's chapter one which is all about procedural abstraction it's
about controlling the control flow of control of a program so how do you say
you know here's what I want you to do and what mechanisms do we have to help
you do that and that's what chapter one is about chapter two is a bad data and
we get into data structures and how to build them up and they did it that way because there are some complexities of
that both of them and they only wanted to throw one kind of complexity at you
at a time now in order to make that work the book uses in Chapter one entirely
mathematical examples that's because the book comes from MIT where you know
everybody speaks mathematics even the business majors there aren't any English
majors and for our purposes in Berkeley
I wanted to provide more interesting data from the beginning but without
running into the complexities of lists and sentences a kind of an idiot-proof data type you can't
build the wrong thing by accident with them very easily so once you get flow of
control under control then we'll don't want to talk more about data okay and we'll revisit this question of sentences
and what they are and why okay other questions okay moving on keywords
get life so he words takes a sentence and it returns the subset of that
sentence consisting of words that include the letter e so and got to get
you into my life got into and you and into and my don't have the letter e but
get and life do okay fortunately doesn't
the word a doesn't have an e in it so it doesn't say get a life alright how does
a words work well says if my argument sentence is empty return the empty
sentence then says okay the sentence is
not empty so it has a first word does that first word contain the letter e so
remember question mark of a one letter word and a word will return true if that
letter is in the word and false if that letter is not in the word you can also do member question mark of a word and a
sentence and it does similar sangwich and it's true if the word is in that time is false other way so is the letter
e in that first word if so then I want
to include the first word in my result and I also want to include a recursive
call for the but first if not if there isn't an e in that word then I just want
to return a recursive call for the but first yeah
is se the same thing as the pen I use another list guy se is the constructor
for sentences it is subtly different from the pen for lists because it accepts words as arguments but a general
rule for you guys who learned about list last semester tryna and actually this is
a good piece of advice for everybody who learned anything about programming before the semester as we're doing stuff
try not to do it by mentally converting
what you're learning to what you already know okay and it's for the same reason
the teachers of foreign languages tell you this you know when I was learning French in high school they told me
correctly try not to translate what you're reading into English try to think in French
right because you never get any good at it until you can think in French and the same is true here if you convert into
what you did last semester or convert into what you did in high school you're going to miss the point I think
okay so you know try and stay on the same page with the rest of us all right other
questions yeah okay
oops
okay pronoun takes a sentence as an argument and it returns the words of
that sentence that are pronouns which is to say ones that are in this list which
yes is not really exhausted that leaves that all the possessors are so on how
does it work well if the sentence is empty then return the empty sentence
otherwise the sentence has a first word so asked is that first word one of these
words if so return a sentence that
contains first of scent and also contains the result of a recursive call
for the but first if not if it's not a pronoun then just return pronouns of but
first ascent okay so these three
procedures have a very similar pattern right yes why is a member instead of
equal because first of scent is going to be something like I or only it's not
going to let's say it's AI is AI equal to this sentence no I isn't a sentence
at all and certainly isn't you know this sentence I doesn't have a me or you or II or she or it in it so
it's not equal to that but it is a member of that there are two different relations that answer the question good
okay
so I want to generalize this pattern
so I'm going to take a predicate function as an argument because that's what's different it's what tests do we
make of first ascent and it takes a sentences argument just like the other
ones and I'm going to say cond
empty cent return the empty sentence that's the same in all of them
now what Fred of first of sent if pred
of first of cent is true then sentence
first of cent and a recursive call with
the extra argument read the same and but first of cent else just the recursive
call
okay so compare this with the ones on the top half of the screen and see if
you agree that it captures the pattern mainly the only thing that's different
is this part where we make some
particular test about first of sense everything else is the same so what we
need is to capture that test and again a test isn't is an action it's a thing to
do so it has to be a procedure rather than a number or a character string or a
sentence or get any of those things okay so now I can say keep even question mark
come on okay
the other ones again I'd have to define
you word question mark of word to be remember a question mark quote e word to
make a function just four words and now I should be able to say keep a word
question mark
and get the answer right
okay question yeah
is there any advantage to converses a stack of nested-if just that your code is prettier if you
keep nesting if everything marches further further toward the right margin you know in your line space and the
window gets smaller and smaller that's all and also as soon as you see the word
cond you're thinking okay this is a multi-way choice so it helps the reader understand the structure I think a
little bit but scheme doesn't care okay
yeah ah are there any exceptions to the
thing where we have to define a function and then stick a function to the function I did not pay him to ask that
question
you
let's do something new
what's this well glad you asked that question back
in high school or middle school or whenever it was your algebra teacher was
very sloppy about notation and said things like the function ax plus B right
ax plus B is in the function ax plus B is a number we don't know what number it
is until we have values for a and X and B but but that expression represents a
number real mathematicians would say the
function X maps to let's pronounced maps
to ax plus B there are a lot of
advantages to this notation one of which is that unlike this one it makes clear
what it's supposed to be a function of okay in high school they use more or
less explicitly this convention that letters near the beginning of the alphabet are constants and letters near
the end of the alphabet are variables but suppose we had an expression like x
y plus Z well there are a lot of
functions this could be maybe it's the function y maps to XY plus Z and
somebody is going to tell us the values for X and Z separately
maybe it's the function X comma Y comma Z maps to X y plus C where it's a
function of three arguments maybe it's y
comma X comma Z maps to X y plus Z well
that's the same function X Z Y there now
it's a different function right so
saying what your parameters are of your function the formal parameters helps you
understand what function you're talking about sadly this character does not
appear on your computer keyboard if you're printing it in a paper you can
say if you're using tech you can say
backslash Maps too and it'll print that but that's not how we do it in our
programming languages the way we do it is based on the work of a guy named
Alonzo Church who was a is I guess a mathematician did he die yet Church I
don't know he was alive a few years ago so he may still dig he invented a
formalism for trying to talk about mathematical ideas based on the notion
of functions and there's a long story about this which I'm not going to tell
you right now probably unless we have time at the end but in his
representation of functions he used the Greek letter lambda which looks like that Greek for L
basically to represent the thing that
makes a function so instead of saying X maps to ax plus B he would say lambda X
dot X plus B that was his notation
except that he wouldn't say this because there was nothing but functions in his language so it's a little Messier but
this is the lambda part so a function of X that has this body and we don't have a
lambda on our keyboards either I got my
introduction to computing at the MIT artificial intelligence lab and then the Stanford artificial intelligence lab and
their keyboards do have lambdas because they do all their you know not all but a
lot of their programming or did enlist which is the language developed for artificial intelligence so these lambda
a lot but we have to spell it out I will write it on the board using lambda the
letter but when you're typing it into the computer you have to say la MBDA so
the notation is lambda and then a
sentence basically of formal parameters and then an expression which is the body
of the function so this is the function WD maps to number question mark whoa TWD
yes
and so I said again
tell me when okay the keep function
yeah okay so did you understand for
example how E words works yes okay so keep works the same way compare it cond
if the sentence is empty return the empty sentence okay now if the first
word of the sentence contains the letter e that's what this says and keep I'm generalizing that the same
as I generalize the area function back at the beginning that was the point of that thing about the different kinds of
areas the idea of generalizing a pattern this is the part that I'm generalizing and you capture a generalization by
having an argument for what's different between the instances of this
generalization so what's different between a words and pronouns it's this part right versus this part that's
what's different those things are expressions whose value
is true or false now maybe I have to explain the word pred pretty short for predicate a predicate is a function
whose range is true and false true and
false are called boolean's so a predicate is a function whose ranger's boolean so this expression
produces a true or a false so a function to compute this expression will be a
predicate and what I do in the generalized version is I take whatever predicate I'm given and call it with
first of Santas the argument okay and all the rest of this is exactly the
same as before except that the recursive call has this extra
bread in it does that answer your question okay anymore yeah
so is there a difference between using a lambda and defining a function with
defined there's so much isn't a difference I didn't pay him either
there's so much isn't a difference that in fact when you say define square x
times X X all this is is an abbreviation
for to find square m 2x times X X okay
this is the same kind of define as if I said you know define foo plus 2/3 right
so we evaluate the plus 2/3 the value of foo is 5 right now what's the value of a
lambda expression if I say lambda X
times X X what do I get or do I get I get that that's a
procedure lambda returns a procedure lambda makes a procedure lambda is how
you make a procedure okay so the way you learn last week this way to make a
procedure you now know actually has
hidden inside it a lambda because lambda is the only way to make a procedure okay
so we evaluate this lambda expression but that does not entail evaluating its
body right when we create the square procedure we don't evaluate x XX that
doesn't happen until we call this function right so I could say oh friend
open-paren lambda X times X X of 6 you
get 36 okay so lambda makes a procedure and you can
call that procedure just like any other procedure usually you know type stuff
like this this is a very roundabout way of saying 6 times 6 what you use lambdas
for is to use them as an argument to a
procedure like keep a procedure like keep is called a higher-order procedure
higher order meaning that either it takes a procedure as an argument or
returns a procedure as its value that's what higher order means higher order now
procedures represent functions remember we had that discussion last week a higher order procedure represents a
higher order function higher order function is one that takes functions as
arguments and our returns of function like for example derivative and integral
calculus are higher order functions keith is a higher order function it
doesn't return a function but it takes a function as one of its two arguments ok
and it does that in order to generalize a pattern generalizing patterns is how
we keep our programs from getting really long remember I said last week programming is easy as long as you can
see the whole program at once you know when the program gets too big to look at it all at once it gets hard so the way
we make programming possible is to try to make our program smaller and we do
that by cramming more into the same amount of space and one way to do that is generalizing patterns so that you
don't write almost the same code over and over again instead you write it once
generalized like keep okay see you Wednesday
