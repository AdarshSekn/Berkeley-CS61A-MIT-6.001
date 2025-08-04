Transcript


okay good afternoon um W I was expecting a bigger turnout
because of the point for the course evaluation so anybody who's in webbland watching in real time time to get up out
of bed get dressed hustle over here fill out of course evaluation okay
um good internet conference mt3 solutions online all that administrative
stuff over there you can read um today we're talking about the analyzing
evaluator and the okay stop playing with the mobia strip you guys pay attention
um the analyzing evaluator is a variant on the metac circular evaluator and
basically uh what it is is a compiler um for scheme programs but
instead of compiling scheme programs into machine language it compiles scheme into scheme which will seem a little
weird um but you'll see that it actually is useful so on the board here is the
factorial function that you know and love and up on the screen is MCE EV Val
uh the EV Val part of the metac circular evaluator and I would like you to
imagine that you are uh the scheme interpreter and somebody calls fact
five so what do you have to do you look at that expression and you
say is it self evaluating no variable no quoted no assignment no definition no if
no Lambda no begin no cond no is it an
application is it a procedure call in other words why yes it is that is to say it's a list that isn't a special
form so uh we call MC
after making an environment in which num is bound to five and in MC apply it um
calls MC eval on the body of the procedure the body of the procedure is
what's up on the board there it's the if so let's come back up and see how we evaluate that if
expression is it s evaluating no is it a variable no is it quoted no is it an
assignment no is it a definition no is it an if yes it
is cool so we go to eval if eval if
basically says first evaluate the first argument which is the equal num zero so
we're looking at equal num zero and we say is it self- evaluating no is it a
variable no is it quoted no is it an assignment no definition no if no Lambda
no begin no con no application yes it
is so um this time we're calling A Primitive and I'm skipping a lot of
steps about you know evaluating sub expressions and everything I'm just trying to hit the high points here um
because so we have have to evaluate equal sign now equal sign is pretty easy to evaluate is it self- evaluating no is
it a variable yes so we look up its value and it turns out to be the uh
numeric equality test procedure uh then we look for Num and we
say is it self evaluating no is it a variable yes we look it up its value is
five and then we have zero you say is that self- evaluating oh yes it is so
its value is zero so now we can call equal with the arguments five and zero
are those equal no they're not so we get the value false so we say look at that and we say
is it's true or false it's not true so we skip over that one and we go to the
bottom line the one that starts times num and we say is it salie valuating no
variable no quoted no assignment no definition no if no Lambda no begin no
con no application yes so now we have to evaluate the sub
Expressions well let's evaluate that asterisk is it self- evaluating no is it
a variable yes so so we look it up its value is the multiplication procedure
how about num is it self- evaluating no is it a variable yes so we look it up
its value is five now how about that next thing the parenthesis fact Etc is
it self- evaluating no variable no quoted no assignment no definition no if
no Lambda no begin no cond no application yeah
yes it's an application so we have to evaluate its sub expressions and then we
can evaluate its body in a new environment so let's evaluate fact is it
self-evaluating no is it a variable yes so we look it up it's the factorial
procedure and now we have to evaluate minus num One S evaluating no variable
no quot application yes so we have to evaluate minus num we evaluate the
pieces of that minus sign self evaluating no variable yes so we look it
up it's the subtraction procedure now we have to evaluate num self evaluating no
variable yes so we look it up and it's four how about one is it self-
evaluating yes so its value is one um so now we call minus with the argument
values five and one it gives us the answer four so now now we're calling the
factorial procedure with an argument of four so um we call MC apply with the
procedure and a list containing four
um and uh apply makes a new environment
with fat with num bound to four and then it says evaluate the body of the
factorial procedure which is that if
is it self- evaluating no variable no quoted no assignment no definition no if
yes so we eval if we have to eval equal num zero are you bored
yet I am um so the point is by the time we
actually get down to factorial of zero and that's equal to one and then factorial of 1 equal two and so on by
the time we actually figured that all out we looked at this if statement five times right six times
from five to zero um and each time through we say
well that first argument that's a procedure call second argument is self-evaluating the third argument is a
procedure call now within those procedure calls there's a variable lookup and a variable look up and then
there's a procedure call and another procedure call we sort of figure out the
shape of this expression the pieces of the expression six
times um and each time it involves going through this big long cond with a bazillion Clauses checking each time to
see if this thing is self-evaluating and is it a variable and is it a quote and so on um so we would like to avoid that
and the way we'd like to avoid it is to what we'd really like is to evaluate
the body of of a procedure only once instead of every time you call the procedure we can't quite do that because
how we evaluate it depends on the value of num so if num is zero then we have to
return a one and if num isn't zero we have to do this other thing so we can't say just evaluate it once and for all
but what we can do is separate the evaluation into the part that's just
based on what I'm calling the shape of this procedure you know it's a it's a list with subl lists and in there are
symbols and so on and we figure out that if it's a list that starts with if that makes it an if special form do all that
stuff only once and the name for that is going to be analysis we analyze this
expression and then um later on we do only the part of the
evaluation that requires knowing the value of num or saying that another way we do only the
part of evaluation that requires having an
environment so what I'm going to do is essentially this we're never we're
not actually going to use the piece of code that I'm about to write but I think seeing it will help you understand I'm
going to say Define
evaluate expression an environment now here's where we take
advantage of the fact that we're using scheme which has first class procedures as our implementation language because
I'm going to call
analyze of just the expression so analyze does the analysis
part the part that we can do without knowing the value of num in other words without an environment
the result of calling analyze is going to be a
procedure not a metac circular procedure but an STK
procedure that embodies what it is we have to do once we have an environment
so in order to do the evaluation I can find my yellow chalk
which I conveniently left two boards away and say call all that
procedure with the environment as an
argument okay so the reason we're not really going to do it like this is uh first of
all if we made an analyze procedure and just immediately called it that uh
eliminates the purpose of this analysis which is to remember the result of the
analysis so we're going to have to store that result from Analyze someplace so that
every time we call this procedure it'll be available to us and the other thing is they happen at different
times so it's rare although it does happen that uh namely when you type in
an expression at the scheme prompt then we are going to do that we're going to evaluate we're going to analyze the
expression and immediately call the analysis procedure because the Expressions you type at the scheme
prompt we don't have to remember the analysis you it's just a one shot you type it you
get a value you move on it's the ones that are the bodies of procedures that
we have to really remember okay so analyze takes a metac
circular expression as its argument and it's going to return an STK
procedure which we can then at our Leisure call once we know the environment all right so let me
um huh uh no wrong
one there we go that's my problem analyze.
scum so here's the thing that I just wrote on the board MC Val just calls analyze and then calls the result of
that procedure uh let's look at analyze exp this is the thing that has the form
of what used to be eval but now it doesn't take an
environment as an argument anymore because what it's going to
return is an STK procedure that takes an environment as an argument so let's
start with an easy case what if it's self- evaluating if the expression is self-
evaluating we call analyze self- evaluating which is right down here at the bottom of the
screen and what it returns is this is an STK Lambda remember Lambda of
environment ignore the environment and return EXP
so um here we are taking advantage of scheme's lexical scope because this exp
is the argument to analyze self- evaluating when we call the analysis
procedure the thing that's created by this Lambda it's not going to be from inside analyze
self-evaluating but nevertheless this Lambda whoops
this ah n looking for n oops no I'm not
I don't know what I'm doing wrong but anyway doesn't matter um this Lambda
expression remembers the environment in which it was created namely the call to analyze self
evaluating and so it remembers the value of x so if we're looking at that one for
example we would do analyze self evaluating of one and this looks like a step backwards
things are getting more complicated instead of just returning one we're returning Lambda of environment one
basically ignoring the environment that were given so you have to remember the
distinction between STK environments which are implicit in this so when you
see that symbol X that symbol is looked up by SDK in an SDK environment this n
here here this argument is a metac circular environment as far as STK is
concerned it's just a list structure but it's the kind of environment that the evaluator
creates okay um analyze
quoted uhuh analyze quoted does something a
little bit interesting uh it has this let expression
so why does it do that why doesn't it just say
Define analyze quoted
X to be Lambda of
n um text of quotation which means
CER um EXP so this would look like the thing that
we did just above it for analyze self- evaluating um what is this let by
us and it isn't very much that it buys us in this case but looking at the simple cases will prepare you for the
more interesting cases that are coming up what this let buys you is that we
only have to pull out the catter of the expression once
if we did it the way I wrote behind me on the board here every time we eval this quoted
expression we would have to take cater of it we would have quote Fu and we
would pull out the foo from the quote Fu this way we pull out the foo from the
quote Fu just once and the analysis procedure is effectively Lambda of well
down here up there Lambda of n Fu
okay um so this Q Val that's not a metac
circular variable it's an STK variable um so everything in STK is
faster than doing things in the metac circular evaluator because we don't have to evaluate we don't have to interpret
STK uh the way we interpret metac circular scheme um it's done for
[Music] us so the let takes the CER out of execution time
and puts it into analysis time and Analysis time only happens once and
execution time happens potentially many times so that's a slight Advantage which
is going to turn into a bigger Advantage when we're doing more complicated things any questions
yet I understand this is new and the examp examples don't look very interesting so far
right anybody any confusions I should clear
up okay moving
on okay oops right here's something a little
more interesting analyze assignment so the expression we're looking at is set
bang variable value expression okay so as in the case of
quote we have this let the let happens when you call analyze assignment not
when you are actually running the assignment so this let only happens once
and we have two things VAR is assignment variable of X which is CER of x car ofex
is the word set bang catex is the variable that we're assigning a new
value to the the metac circular variable that is getting a new value and now
comes the interesting part right
here assignment value is cator so it's the third piece of the set bang
expression but we're not just saying let VPR be assignment value X we're saying
let vprb analyze assignment value
X okay so if you say set Bang
Fu big long complicated expression that big long complicated
expression gets analyzed as part of analyzing the set
bang and therefore we only have to analyze it once when we actually call
the analysis procedure which is this Lambda of n thing we're going to set
variable value the same as in the regular metac circular evaluator
VAR that's the variable name to vpro of
En so call vpro with the current environment which will be different each time so imagine
that this set bang is part of a procedure body and we call the procedure over and over again so we're this set
bang over and over again with different values for things so calling vpro with
the environment will give us a different value each time right um and then we set
this variable to that value in the current environment okay so I want again the the
really whoops going the wrong way the really important part of this is this
call to analyze right here so analyzing an expression involves analyzing all the sub Expressions so
you'll see in a moment when we look at if that when we analyze this particular if right here we're going to analyze
also equal num zero we're going to analyze one not very hard we're going to analyze times num fact minus num one
which includes analyzing asterisk and num and the call to fact and the looking
up of fact and the minus and so on all of that stuff is part of the analysis of
the if
okay all right let's look at analyze if it's coming up pretty quickly
here here it is um so given an if expression we pull
out the three pieces the predicate the consequent the alternative and we
analyze all of them so that's what I just said we analyze equal num Zer we
analyze one we analyze times num fact minus num
one okay once we've done that we can make
the analysis procedure the the thing that's returned by analyze
if and remember what the one in the metac circular evaluator looks like um
there are three calls to MC ofal it says if true MCE Val of if predictive if n
then MCE Val of um if consequent blah blah blah else MCE Val of if alternative
blah blah blah instead of that we say if true P ofin so we've already analyzed
the equal num zero and we just call its analysis procedure with an expression that has a value for Num and then we
call either COC or AO but not both
okay now somebody should have a question by now there should be questions unless you're all completely
lost
yeah does it mean that every time you would be calling eval before you use analyze instead no
[Music] um you only do the analyze
once for this expression yes yes that's right every place pretty
much every place in the metac circular valuator code that used to say MC Val is
now going to um have an analyze and then depending
on circumstances uh it might or might not run the analysis procedure or some
analysis procedure yeah okay why does it say true question
mark um that's really something that was already in the vanilla metac circular value valuator and the reason is they're
leaving open the possibility that we might in some variant
evaluator use a different representation for true or false than SDK does for
instance we could have a scheme variant in which number sign T is true and
anything other than number sign T is false so kind of the opposite of what scheme does we would Implement that by
changing true question mark okay that's why
yeah ah okay so this defeats you think the special forness of if yeah he's
saying well remember if is a special form has to be a special form because um
in the case of a recursive procedure like this we want to make sure uh that we don't keep calling fact
for Num equals 0 num equals ne1 m equals -2 on forever
but analyzing this expression doesn't involve calling fact
it just involves registering the fact that this is a procedure
call and that comes running the procedure we have to look up fact in the
environment and and and call that procedure so it's okay to analyze both branches even though it wouldn't be okay
to run them good question thank you for asking that okay I have five minutes left before we do course evaluation so
let me proceed to the really crucial part of this which is right here what
happens when we see a Lambda expression well we pull out the formal
parameters from the Lambda call that vs and then we take the body of the
expression and remember the body of a Lambda can be more than one expression if you're doing nonfunctional
programming so we have this thing analyze sequence which does does just what you think it does it takes a list
of Expressions analyzes all of them and returns a list of analysis
procedures okay um do I mean that no it returns an one analysis procedure that
consists of recursively are evaluating each piece of the list so analyze
sequence makes an analysis procedure for the body and then we call make procedure
in the regular metac circular evaluator this would be make procedure uh Lambda parameters of exp
Lambda body of exp n but this time what we
remember in our abstract data type procedure is the analyze
body this is where the speed saving comes from because when you create a procedure
that's when we analyze its body and what we store we don't store the text of the
procedure at all all we store in our data structure is the analyzed procedure
body get it and so it's when we say Define fact that we
do the analysis when we say fact five that analysis has already been done
now we do have to analyze the expression fact five itself that you type at the command line but the actual procedure
body including the recursive cost effect that's already been analyzed and that
really speeds up the process of doing a recursive call so that's something that
you're going to play with um I guess in the lab no you're not um but you can
play with it um in the lab if you feel like it at your
leisure um so try hard not to get confused about
the difference between an STK procedure which we haven't changed at all and a metac circular procedure which is the
thing that this is all about that's the first sort of summary point and the second summary point I said at the
beginning that what we're doing is writing a compiler um mostly when you think of
compilers they compile into machine language but that's not always true these days so if you write a Java
program uh often the Java compiler doesn't compile into machine language it
compiles into this intermediate thing called Java virtual machine jvm code and
the point of that is that the jvm code is runable on everybody's computer not just
yours well this is kind of like that it's compiling metac circular scheme
Expressions into to svm scheme virtual machine code otherwise known as STK
procedures okay so compiling scheme into scheme really does um give us a speed
payoff and I'm actually not lying when I say that this is like what a compiler
does this is a compiler for scheme um now because we're compiling
scheme into scheme if leaves out a lot of the stupid boring details in grown-up
compilers which you'll get more than you want to know uh when you take 164 um
which you should do anyway it's mostly interesting despite the stupid boring details of machine language so this is
the your introduction to the concept of
compilers okay hkn people great so what's going to happen
these guys are going to give you evaluation forms to fill out one for me and one for your ta is that right yeah
only once on the form that's for me you're going to take one of these poits
and you're going to write on it post it your
name Frank ubar and your login your class login
cs61 A- XY whatever it is you're going to write
these extremely legibly capital letters would be fine if that makes it more legible if your name
is very long I only need a substring of it what we enter in is the login and the
name is just it tells me do you want to enter the score for this person and we check to make sure it's the right person
so the reason for poits is that the course evaluation you're going to do is
anonymous so you don't put your name or anything on the course evaluation form you stick
a Post-It on it because you want a point for doing this these guys after they
collect your forms are going to pull off all the poits and give them to me but
they're going to keep the form so I don't get to see your form uh before the end of the semester and I never get to
see your form with your name attached okay but I do get your name so that I can give you the point okay oh and
you're going to have two forms to fill out one for me one for the TA only put on one posted on one form okay
UC Berkeley