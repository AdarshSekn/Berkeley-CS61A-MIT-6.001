Transcript


okay uh last time a couple of things I didn't quite squeeze into to saying um I
left you with this picture of um the unimportance of constant
factors um even a constant factor of several million um by the time the
amount of time gets to be significant anyway even that kind of constant factor is down in the noise but I should tell
you there's an exception um and that is if you happen to be in the video game business because those
guys are always absolutely pushing the limits of whatever this year's Hardware can do so they really do worry about
constant factors but for the rest of us no um the other thing was I showed you
this frightening formula um that talks about one function
basically being bounded by another function that f is uh for large enough
values of X always less than or equal to some constant Factor times
G um but I didn't get to talking about the big Theta notation um which is
actually the one that we use mostly that we're most interested in because um Big
O notation says f is bounded by G but it
doesn't say how closely so so um take the function um FX =
3 and the function g ofx equals x to the
X power okay well f is Big O of G but that
doesn't really tell you very much because um f is so much less than G uh
you really want to know about you know how long is it going to take not how
long isn't it going to take so the Theta notation says f is in big Theta of G if
f is Big O of G and G is Big O of f um which sounds at first glance like
it might be impossible because you know F can't be less than G and G less than F but the reason that this is possible is
this constant Factor so essentially what big Theta says is the that
um if you draw a
picture of G so it looks like
this um and you multiply it by something and you multiply it by something else
and somewhere in here lies F so it you know f might vary
up and down a little but basically f is within this envelope pretty close to G
and that's what we really want to know is Big Theta confusingly very often in the literature
they will say Big O when they actually mean big Theta just to confuse you um
but you're not going to do that okay and the other thing I didn't
say about time complexity last time is that there are certain family
of time complexities that come up a lot in computer science um and you're going
to learn again in 61b more than you want to know about this but I'd like to give you a little bit of a sense of what they
are um
so one of the common problems for computers is you have some huge
collection of data and you want to find something in it okay so I have the phone book and I
want to find somebody's phone number I have um the human
genome and I want to find some strings of A's and T's and whatever the other two are
um I have the worldwide web and I want to
find whatever key keywords you're searching for right that's a search those are all search
problems um and so the most obvious way to do searching is
you have all this data and you look at the first thing and say is this what we want nope look at the next thing is this
what we want no Etc and that takes linear time right basically on average
you have to go halfway down the whole data set to find the thing you're looking for um
clever ways take time uh proportional to the log of n which is a huge Advantage
like you know the log of a thousand is three right to the base 10 or well
anyway um so it's a big difference um and typically the way those work is you
get the data in some good order first so when you're looking something up in the phone book you guys don't look things up
in the phone book do you you look things up in the internet who's seen a phone book great let's say
let's say there's a power failure and you want to call up pg& to
complain about it and you can't look up their number on the internet so you drag
out the phone book from the closet and you want to look for pg& you don't start at page one and start scanning down for
pg& right you say okay I'm smarter than this uh P that's about halfway through
the alphabet so I'm going to open it up halfway right so in doing that you're taking advantage of the fact that the
phone book is not in a random order it's an alphabetical order and so you can get your searching down to log in so that's
the sort of pretty clever searching technique and then if you're really clever um you can actually search for
things in constant time uh using an even better data structure called a hashtable
that you'll learn about next semester so all of these things are this sort of searching family of running
times um and then these guys are for
sorting which is the other canonical common problem things to do with a
computer is to put some data in order um and we looked last time at insertion
sort which took Theta of n^2
time um and all the obvious ways to sort Take n s time um
the clever ways to sort take in log in time um those are the ones that work by sort
of cutting the whole data structure in half and sorting the two halves but each
of those you haves you cut in half Etc so that's where the log in comes from um
and it is uh theoretically impossible to do better than n log in
for the the kind of sorting that works by comparing two values see which one is
smaller than which and log in is the minimum you can do better than in log in
in special cases of which my um favorite example is let's say we have
um the name and address of everybody in Berkeley uh which is what 100,000 people
and we'd like to sort them by ZIP code
okay um well the right way to do that is not any of these comparison based sorts
it's you set up a dozen uh great big buckets on the floor because that's how
many zip codes there are in the city of Berkeley well roughly um a dozen and um
you just take an address and throw it in the right bucket and you can do that in linear time in 100,000 people so you get
to do that because um the information on
which you're sorting is only a piece of the complete address if you wanted to get everybody's actual address you know
so that there's as many addresses as people then you would have to do one of these things okay so those are the first
two um
there are um surprisingly few uh but there are some problems that
take n cubed time the canonical example
is multiplying matrices Square matrices let's say um so an N byn Matrix um if
you remember how to do that um there's N squared elements in the answer and each of those
is a sum of N products right everything in this row multiplied by everything in
that column so that's n cubed multiplications that you have to do um
to matrix multiplication there is a an extremely clever complicated way to do
matrix multiplication that is Theta of n to the 2.7 something it's not e it's some ugly
number um but you know basically it's
NQ and then here's the important Point there's a huge gap somebody's going to tell me I'm
wrong with some example or other but to a first approximation you never see n to the fourth problems or n to the fifth
problems um after this we get
to exponential time problems
and factorial time problems and the occasional end to the end time
problems um how many math haters in the
room a few you understand right that two to the nend is way way way way way bigger than
incubed like grows much much faster even the math haters know that I hope
these problems are called
intractable meaning um yeah theoretically we can write a program to do these things but
in practice um for significant size data sets the program would never finish
running um so you know linear time algorithm means
double the input size um double the running time quadratic
means double the input size quadruple the running time but two
to the N means just add one to the problem size go from like Nal a million
to n equals a million + one and that doubles the running time so that means
you don't get to a million you get to like n equals 50 and if you can just just barely do that n equals 51 is going
to be way too long right and by the time you get to n equals 100 forget it you'll be dead before you get an answer um so
for for non-toy siiz problems these
um these kinds of running times really do mean in practice that we can't do it
and um for problems like this one of the
things that you do is say well can I come up with an approximate solution to the problem that is good enough and can
be computed in a reasonable amount of time so all of that stuff is uh the analysis of algorithms that you'll learn
about later on um and that's all I have to say about time efficiency um I want
to go on now and talk about space
efficiency yeah
ah okay question was um would I would you ever deliberately design an
algorithm to be intractable say for cryptography um and the answer is it's
not good enough for your algorithm to be intractable if there's a better algorithm your enemy is going to use it
instead of your intractable one um so no
Bally um okay space efficiency uh this is the thing in the
book having to do with um iteration versus recursion and tail
calling all that um and I want to start by saying that this matter is much less
than it did back when they wrote the book um back then computer
memories um were measured in um
kilobytes as opposed to gigabytes or terabytes um and you really did have to
pay careful attention to how big your program space requirements were um it
still matters a little bit these days not because you're going to run out of
memory you really are not unless you're an astronomer or you work for the
federal government um on the budget but
um what does happen is as your programs memory requirements get bigger
indirectly that slows the program down because what happens is you're competing your process is competing with
other programs on the computer and your operating system is moving things in and
out of memory um and the higher the memory load the
more time you lose to your program not being in memory when you need it to be
um so for that reason people worry about space efficiency still somewhat um
okay so the other piece of background to this topic is um when I was your
age I bet you never think you're ever going to say that to anybody right um
when I was your age um lisp the the language of which scheme is
a dialect um had kind of a bad reputation um for doing everything
through procedure calling uh instead of
having uh specific iterative mechanisms like for loops and while loops like that
language you learned in high school um because procedure calling was viewed
as being very expensive um and therefore lisp was viewed as
being unsuitable for practical problems and
um the big sort of top level Point here
is is that you can write a program using procedure calling using
recursion as the means of expression the form in which you write the
program and it still can come out with
um the same efficiency that you would have gotten from a wired in iterative
construct provided that your algorithm is basically iterative in the first place as if you would have written it
iteratively you know in some language with for Loops uh we can get iterative
performance even though you didn't write it that way in scheme
um so up here we have um two different
versions of procedure count what count does
tells you how many words are in the sentence or how many letters are in a word um and we have here two different
implementations and the first one they're both recursive procedures so here's a recursive called to count in
count and this second version of count has a helper function iter and here's
the recursive call to iter so so there's a recursive call both ways nevertheless even though these are
both recursive procedures that is the form in which you write the program is recursive for both of them the process
generated by these two programs is very different and the first one generates a
recursive process the second one generates an iterative process so uh to
understand all that um you have to remember remember that um
inside the computer uh there are a lot of little people right and every time you make a
procedure call you're hiring a little person to solve the problem and uh there are lots of little
people that know how to do the same procedure uh and when you call one you
give it different input values to work with in its arguments um and so they're
doing slightly different jobs but all running the same algorithm so so in the first
version works like this um I'm going
to so as not to take so much time or board space instead of counting I Want
to Hold Your Hand I'm going to count she loves you so um I'm gonna hire um Charlotte
okay that's Charlotte's task and charlet says is the sentence
empty no it's not so I have to do plus
one and then count of but first of this which is
loves you right so
Charlotte hires um Carl to do
that Carl says is loves you empty no it's not um oh meanwhile Charlotte is sitting
there waiting right Charlotte's twiddling her thumbs waiting for Carl to do the job so Carl says loves you is an
empty so I'm GNA do add one to um count
of but first of that which is the sentence
youu and Carl hires
Kathy to do count of you right Charlotte's waiting Carl's
waiting Kathy says is youu empty no it's not so I'm going to hire um
Charles oh wait I have to do I'm sorry I have to do plus
one count that's a parenthesis of empty
sentence and hires Charles to do count of the empty
sentence okay everybody with me so far
great Charles says is that empty yes it is I return zero here Kathy here's my
zero now Kathy says add one to that
zero it gets one and so
Kathy tends one to Carl Carl in order to do count of loves
you says plus one to the one from Kathy says okay count of loves you is two
Charlotte is doing plus one whatever I get from Carl that's a two add one to it
three Charlotte returns three to Alonzo who prints it
out um at the scheme proms okay
so as we're doing this really no work is being done on the
way into this recursion it's only when we get down to
the empty sentence that we start with zero and start adding one adding one adding one adding one on the way out and
so each of these little people has to wait for the next one in line to return
a value right now each of these little
people um has to remember what scent is
and you know where I came from and everything and all of that information takes up room in the computer's memory
so when they're all waiting when we have four little people all waiting for each other um that's four chunks of computer
memory uh in use for this computation Okay so
this isn't a question about the running time it's a question about the memory use which is linear in the size of the
problem yes let me get to it proceses and then
I'll answer that okay um okay now let's do it the other
way um yeah
yeah Charles has zero words actually so he's doing the empty sentence but no
once the computation is finished we're not using the memory anymore if that's what you're asking
okay each little person has pockets in which they keep information
so Charles has a pocket in which is an empty sentence and Kathy has a pocket in
which is this one-word sentence and so on right
um now you're right in this simple example it doesn't matter so much what the sentence is once they've made the
recursive call all they really care about is waiting for the answer right and then who asked me
that's the the important thing that they have to remember is who asked me for this answer right Charles has to remember to
give the answer to Kathy and Kathy has to remember to give the answer to Carl and Carl has to remember to give the answer to Charlotte and Charlotte has to
remember to give the answer to Alonzo okay so that's what's taking the memory that's important does that answer your
question
oh oh I see okay oh she's asking about the difference
between a a one-word sentence and a word these parentheses right
here um mean that we're looking at it sentence they're just not the same thing at all so
no okay um all right let's do the iterative
process Carol is given the task count
she loves it right so what Carol
does um is
this itent zero so Carol hires Irving
to do
iter no I'm ahead of myself
it of She Loves
You zero Irving says is the sentence empty
no it's not so I'm going to [Music] hire
Isabelle to do
iter loves you
one Isabelle says um is it empty no it's not so I'm going to hire if
Abad to do iter U
two kabad says is this empty no it's not so I have to hire
Irene to do it empty sentence
three Irene says is this empty yes yes it is the answer is three and this is
the answer okay in this case we're doing the work on the way in rather than on the
way out and because of that because when Irene is finished the whole
computation is finished that is to say because the
recursive call to iter is the very last thing that the call above it has to do
Carol can say to Irving please do iter she loves you zero
and by the way when you're finished don't give the answer to me give it to
Alonzo Irving when he hires Isabelle can
say please do it of loves you one and by the way when you're finished don't give
the answer to me give it to Alonzo um and then carolly and Irving
you know go off to Hawaii um Isabel hire zabad says by the
way when you're done give your answer to Alonzo Isabelle goes off to the Bahamas um aabad hires
Irene same thing all right so because all the work is done prior to the
recursive call the recursive call is the very last piece of work to do um
there's no need for us to remember who's waiting for intermediate
answers okay and so we don't need to use more and more memory as the size of the
problem goes up we just need one little chunk of memory
yeah you're not adding three and zero together no um you
added one to zero in between Irving and Isabelle okay
so the the work in case that isn't clear I should point out right here is where
the work is being done and remember scheme uses applicative word evaluation which means
the argument expressions are evaluated before the procedure call is done right
so that adding of one happens before the recursive call to iter
okay a scheme interpreter or compiler is capable of detecting this
situation if the recursive call is the last thing that has to be
done then um scheme will
say I'm going to treat this just as if you had said for or while or go to or
however it is you do it you know in those other systems Okay so so you wrote
a recursive procedure call but I'm not going to actually compile a procedure call at
all I'm just going to compile change the value of scent change the value of I'm
sorry change the value of words change the value of result go back to the top remember I said when we learned about
recursion don't think go back and you shouldn't think go back but it's okay for scheme to think go back when it's in
the kind of situation where it can that's because scheme doesn't make mistakes about it and you do
yeah yes um the question was is the scheme doing something different than it
would have done otherwise yes it says oh look this is a tail call um so I'm not
going to do a recursive evaluation I'm just gonna you know change the values of
things and go back do it again yeah
oh I'm sorry the question is when you load it into The Interpreter how does it know which count you're calling um you
wouldn't load this file into The Interpreter with two definitions of count in it there's only one definition of count if you did do this whichever
one you did second is the one that's
there okay why did I make iter an internal definition instead of a separate procedure because um
nobody's going to use this itter except count it only makes sense for counting right
um and so for one thing it's just cleaner because um it keeps the
definition with the use and also if I had wanted to make it
separate um in order not to get in trouble with something else called itter for some other little procedure I would
have had to call it count iter or something and that would have taken six extra keystrokes
twice um so it's just easier but it's not like it's not crucial it's not a
requirement for tailal elimination
yeah ah no he's saying isn't it going to be less efficient because you're defining it over and over again we will
talk much later about how an interpreter works but for now just take my word for it no yes here
next wouldn't you put the functional above the definition no
um internal defines come before the actual body of the
procedure so externally you could Define them in either order as long as they were both defined before you called it
yeah
is there a downside to internal definitions um yes um not an efficiency one but a
debugging one um you can't easily
trace an internal defined procedure you can't say Trace iter at the scheme
prompt because there is no iter at the scheme prompt it's only inside that procedure so it's easier a little bit to
debug if you don't yeah
yeah
yeah yeah so he's saying this call to count the recursive call to count is
inside the expression plus one count of but first
of sent and so after we get back from count we have to still add one to the result this call to iter when we get
back from it here there's nothing left to do yeah now it's not just in case
anybody was thinking of making this mistake it's not because this call to iter is on a line by
itself lines don't don't count a line a new line is the same as a
space um it's got nothing to do with the um notation it has to do with what work
still has to be done in fact here's something I'm surprised nobody's asked yet um this call to iter is inside a
larger expression namely this if
right um so how can it be a tail call if it's inside an if
who can tell me the answer to that yeah because if is a special form and in
particular if's evaluation rule is
um it looks at its first argument and then depending on whether it's true or
false it evaluates either the second or third argument and that's the end so yeah it's the special forness that makes
this work um okay let me
um make sure I haven't forgotten to say anything uh oh there's lots I've forgotten to say but not about this um
so is it okay if we move on good I hope so better be because I'm
moving on
um okay okay
um for the benefit of those three math haers um Pascal's
triangle Etc um each number here is the
sum of the two numbers above it okay BC triangle is useful for a
bunch of things but I'm not going to tell you that because either you already know or you don't care um but I am going to show you this
procedure Pascal up at the top of the screen um oh I'm sorry except for the
numbers at the ends of each row which are always one so Pascal takes Aon number and a
column number counted from zero in both cases if column is equal to zero that
means we're looking at the left edge of the triangle the answer is one if column
is equal to row that means we're looking at the right edge of the triangle and the answer is one
otherwise add these two numbers from the previous row okay so this procedure very
straightforwardly um says what I just said to you at the board about how to compute Pascal's
triangle and so if I do the particular example that I circled up on the board
that's um row five column two counting from zero and
sure enough the answer is 10 it's not five time
two is like
just to prove it there
um oh this is
interesting um that took quite a while didn't it why
because this is a Theta 2 to the n
algorithm to get this number I have to do these two numbers to get the four I have to do two
numbers and to get the six I have to do two numbers so that's four numbers on this row eight numbers on this row 16
numbers in this row Etc yes is there any way we can do this
iteratively no uh well not not with anything like this algorithm because
because there are two recursive calls here and they can't both be the last thing that has to be done
right so um no but we can make this run
faster oops
um running this complicated program here with the this does it looks at
first glance like it ought to be very inefficient because it has this helper function Pascal
row so Pascal row six produces all the numbers on row
six okay and um to get a single element of
Pascal's triangle up at the top of the screen there I compute the row the entire row and then I pick the an the
the column of value from that row so that sounds like it ought to be
inefficient because in order to compute this value here what I really need is
kind of a diamond shape of numbers that looks like this and there's some more numbers down
to the sides that I don't need it would be a more evident that it would be more
of a difference further down um so I'm actually Computing twice as
many numbers as I need to roughly speaking so it ought to take twice as
long but in
fact it takes no time
okay um why is that well
because that doubling of computation is Computing some of the
numbers more than once so in order to get the 10 I need this four and the
six in order to get the four I need this one and this
three in order to get the six I need need this three and this other three and
that just gets worse and worse and worse so we're Computing the same values of this function over and over again and
that's where most of the time is going in the simple version whereas by Computing the entire row one once and
then the entire row two and then the entire row three we compute more numbers
than we need but we only compute each number once um and it's turn turns out
to be the difference between exponential time and quadratic
time okay so the moral of the story and this is much more important than any of that stuff about space efficiency and
tail calling um the moral of the story
is you have to think hard about what's making your program
inefficient and how to achieve a better order of growth and it's the order of
growth that you want this code is much more complicated so the constant Factor if you look at this versus the original
version the constant factor is going to be greater but that is so swamped by the
fact that it's quadratic versus um exponential time that it
doesn't matter next point for those of you who didn't hate high school math you
might remember
this formula which is a formula for computing
one of the elements of Pascal's triangle um without looking at the row
above it you just take which row you're in which column you're in take the
factorial of these three numbers how long does it take to compute factorial Theta of what n how long does
it take to compute three different factorials theeta of what n okay
so this if you know this formula you can do it even better than n squar you can
do it in linear time right so the moral of the story is
an ounce of mathematics is worth a pound of computer science okay now let me answer your
question from before that I promised to answer about um should you prefer
iterative because it's more efficient um my answer to that is no and that's
because um let's go back to these two examples um when I read this whoop that
wasn't what I meant when I read this
procedure I have no trouble at all understanding what it's doing it seems perfectly straightforward and obvious to
me when I read this procedure I have to think about it a little harder plus you're more likely to
make mistakes so this is one of these things where I said um first get the program to
work and then worry about getting it to work efficiently you know um if I were you at this stage
in your life I would write things recursively you know recursive process rather than
iterative process um almost all the time because you'll get it right the first
time instead of not getting it right the first time which matters a lot if that first time is on a
midterm um and also remember that it's only
space efficiency we're talking about both of these versions of Count take linear
time right so in terms of how fast it is it's not going to be a noticeable difference one way or the other so go
with recursion but you should know what iteration is all about see you Monday
