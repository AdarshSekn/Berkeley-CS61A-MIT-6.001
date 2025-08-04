Transcript


good afternoon welcome to cs61a on a cheery
Wednesday um a first of three midterm exams my mom
always used to complain that we shouldn't call them midterms if there's more than one of them um because it's
not the middle of the term but anyway it's a week from today um it will start at 7 o'clock not
710 um and it will be held in 2050 vlsb
I was not able to get this room for our exams but at least we uh apparently
enough of you just barely enough of you dropped the class already so that we fit in one room for the exam which is nice
um question zero one point your name your login your ta's name your section number um and you're going to be asked
to put your login on each page in case your exam gets separated during
grading um the way it works is you take the exam individually and then near the end uh
you take part of the exam again as a group and if you finish the individual exam early you're going to be sticking
around for that so bring a book to read um but during the exam uh it's closed
book this is an experiment this semester um so you're all guinea pigs um you keep
you may bring one page of notes
um I'm pretty sure that will be plenty if there's anything obscure that you're
supposed to do we will provide the necessary information in the exam um so
we'll see how that goes uh right that's it for exams okay
words and sentences I do this picture on the board to show you that there's an overlap between words and sentences and
lists oh two hands up yes either of you go
ahead can you do both sides of the piece of paper yes you may use both sides of the piece of paper
yeah you can have it however you like if you want to use Sixpoint type that's
fine um by the way if you want to collaborate ahead of time on planning a
terrific set of notes to bring in with your group members or whoever that's fine too
yes the exam um we're scheduled for two hours we
usually run a little bit over because it takes a little time to actually collect the individual papers and hand out the
group part so you know don't plan another activity before 9:30 um the individual part will give
you like an hour and 40 minutes or something and then but the way I write
exams the goal is to get um a reasonable
one hour exam and you have two hours in this case not quite two hours because of the group
part um to do it in so I'm hoping that nobody will feel rushed for time in this
exam and to make sure that that's true uh we have our Tas take the exams
the Tas get 12 minutes if it takes them more than 12 minutes we cut a
question um and it's worth talking about this because it it really if you think about
it affects how you approach the exam the reason the Tas can do in 12 minutes
something that should take you an hour is not that the Tas can write Solutions
faster than you can it's that they're better at reading the questions they
have experience knowing what kinds of questions we ask what it is we're trying to test and say look at a question and
figure out very quickly what it's asking them to do therefore you should plan to
spend more time reading than writing during the exam so you know put your hands in your
pockets if necessary while you're making sure that you actually understand what the
question is asking you to do and then pick up the pencil and start doing it um
the actual answering of the questions supposing that you've been doing the homework all along um the answering of
the question should not take you that much time okay um I hope that's how it works out every
once in a while somebody finds everybody finds some particular question impossible because it was badly worded
we try to catch those things but we're not perfect at it so sometimes we do some gr adjustment if necessary only up
not down um if everybody gets an a that's terrific i' be happy with that
um yeah basically um my theory about this you're going to have opportunities
you're going to be hearing about um an an hkn run review session and probably a
TA run review session uh over the weekend um and you can do those things if you want my own personal feeling
about it is that if you don't know the course material by now it's probably too late you know to learn it um
and that therefore you should just you know do the homework regularly read the homework solutions regularly so read
this week's homework solutions when they're posted on Monday um and Tuesday night get a lot of sleep
that's it that's how you study for the exam any other questions about the exam I hate exams
yes that's right starting Monday is new stuff that will be covered in in midterm
two okay so it's up through Friday of this week and the homework that you're probably doing this
weekend okay although you ought to have started on it already
um yeah any other questions about
that okay great
um you know what this just occurred to me but um I think I think we will ask
you to turn in your one page of notes so make a copy so you'll have them
for later because midterm two you get to bring in two pages of notes and so on so
you want to keep a copy of your midterm one notes but I'd like to see them because it'll help me understand what
students think the course is about yeah
sorry what if you don't bring notes that's fine yeah
I'm sorry I can't hear
you no uh anything that fit the question was is there anything you could put in
the notes that's unacceptable I can't imagine what it would be
yeah sorry it's closed book oh when I said yeah to bring a book
to read is after you've turned in your exam and you know don't bring the textbook bring you
know bring the Cider House Rules by John
Irving or something like that um anything
else okay great um question zero your name your login
your ta's name your section number if you don't know your ta's name or section
number uh now would be a good time to find out out by going to section and
asking um arrange where you're going to meet your group you know we're going to sit in this corner of the room or that
corner of the room or whatever it is
um if you're someone who always asks a lot of questions in exams sit near the
aisles try not to do that though okay words and sentences versus
lists so here's this picture that talks about U what's what
and the purpose of it is to make the point that uh the domains of these
functions neither one is a subset of the other so word sentence first but first
Etc work on Words Kar cter and so on
don't work on Words you can't say car of quote hello and get H has to be
first on the other hand and word sentence first but first Etc doesn't
work on any kinds of lists other than lists of Words which is the same thing as
sentences okay so there's this intersection of lists of words where both kinds of procedures will give you
the answer you want now when you're in that intersection you want to follow whatever
data abstraction has been given you so um if a problem says one of the
arguments to the function you're writing is a list of sentences you're going to want to use
kind car and cter to take apart that list of sentences but you're going to want to use first and but first to look
at the individual words in the sentence okay because we didn't say a list of lists of words we said a list of
sentences right so that that's just an example of respecting data abstraction
the same as you know you use numerator and denominator for fractions instead of car and
cter um okay higher order functions for lists
that's the the only really new material that I haven't taught you
um in lab and our homework and our lecture uh you've seen every keep and
accumulate um every computes a function of each
element of a word or sentence each letter or each word and puts them together into a word or sentence keep
takes a word or sentence and returns a subset either a smaller word or a
smaller sentence that um for which some predicate that you give it returns true
so it selects a subset and accumulate um takes a combiner function
that takes two things and puts them together and so accumulate kind of works
on both because the combiner that you use can be appropriate for words and
sentences or it can be appropriate for lists um so there's really only one of
those that you have to worry about but every in keep there are list
equivalents called map and filter um
so
oops
okay so here's a case of a list of sentences where I used map on the list
of sentences but the selector function I used took one sentence like John lenon
and returned first of it so I got back a
work um so that's just an example of using
map and I think it's obvious how the rest of this goes um if you're dealing with lists of
lists map might give you a list of lists as results where you really just wanted
individual words a list you wanted a sentence as the answer um and in that
case uh you might want to accumulate with a
pen uh or just apply a pen to the result to flattening I think the book talks
about flattening a list of lists
um we did so much last time that I don't
have enough new to say this time pretty amazing
um do we do sorry I'm a little disorganized
today come on here we are
just sequences and calculator all right that'll be Friday okay uh let me talk
actually about the thing at the top of the screen here um which is again about the difference between lists and
sentences so the first thing up there is a procedure to reverse the order of the
words in a sentence and The crucial part is that we
say sentence reverse all but the first word and then put the first first word at the
end of that okay and this works to reverse a
sentence um but if you try to reverse a
list by [Music] doing the same thing only cons instead
of sentence and cter instead of but first and car instead of first it
doesn't work so let me show you it not working
huh you don't
say oops wrong
place better okay so now if I say
reverse this is the cons version we're looking
at I get this wrong answer and maybe you did that in the lab
maybe you've already seen something that looks like this and it's what you get
when you call Cons with something other than a list as the second
argument um so cons is very good for sticking a
new element at the front of a list but it doesn't work for sticking a new element at the end of the
list so that's an asymmetry in lists that has to do with the fact that in each pair of the spine of a list the car
is an element and the cter isn't an element it's a subl list it's part of the list another spine pair um and so
this is what you get if you put the elements in the cters which is what this program tries to
do um so in order to write a real reverse um well there are a bunch of
ways you could do it probably the most straightforward way uh would be
this did you do this in lab this week yeah so
oops
so it's the same up to this point now I'm going to say
append o seek it's
G
okay whoa let's try that again
um I don't know why that happened actually
but yeah um so reverse of oh I see right
here ah
okay
there we go so in order to make this work I use Depend and also here's one of the times
where it's actually a little bit useful to use list I called list with a
single word as its argument so this says make a
list of length one containing this thing and that's because what a pend is going
to do is take the elements of reverse of the cter and combine them with the element
of this one element list I just made to make a new list okay so pend the arguments have to
be lists and the result is a list of the elements of the arguments so that's um that's the way
that we would do reverse or a way anyway that we could do reverse there are other ways um it turns out for example Le by
the way that reverse is one of the few things that gets easier to read if you
write it iteratively rather than recursively so to generate an itative process with the tail call and an extra
argument to helper function just like I did last week so if you're interested
you can pursue um writing an iterative
reverse okay um
hm this is great nothing to
say oh yeah I do have something to say I
guess
so unlike every the output from map can be itself
a list of lists so map itself does not do any flattening of its
result it just takes it conses whatever your function is of car
of the list with a recursive call to map for the cter of the
list okay so that's a little bit different from every that flattens things out for
you into a sentence um
yes okay the question is in the file I loaded there are two things called reverse so how do I know which one I got
the answer is I got the second one the same as if you find a bug in some
program you wrote and so you type in a new version the new version replaces the old version right so it's the same thing
it defined the first reverse and then it said okay here's a different definition for reverse and now that's the new
one okay ordinarily you wouldn't do this and I don't want you to learn this as a programming technique right um it's just
the lecturing technique
sorry yeah use the last one but guys don't Focus your attention on what is
scheme do in stupid complicated edge cases that you shouldn't allow to happen
right basically if you have two definitions for the same thing in the same file it's because you're
confused and it almost doesn't matter what scheme does because it's unlikely to be what you
meant okay so just don't let it happen
yes could you rewrite a pen yes absolutely using cons Ken cter of course you could
yeah I'm not sure I understand the question
um are you saying you want to write you want to change the meaning of
a pen
I think actually there's a definition for a pend using cons get used to calling it cons in the
book um yeah go
ahead I'm sorry say it again
ah okay the question is um in the map example that's right here on the screen
if my list of lists includes just a word what would happen um well we can do
that
um
what
what oh
what I hate computers I really
do in this silly terminal program I have to type control shift copy to copy
something anyway here's what happens um it applies but first to the word and it gets
ELP so the general answer is it depends on the function that you
use as the first argument to map so every element of the list that you give
as the second argument must be in the domain of the first function of that
yeah first argument so in this case the first argument was but first and its domain is
words and sentences so I can have a list of words and sentences if I used um
plus well no square root map square root over a list it had
better be a list of numbers and nothing else okay if I say map car it had better
be a list of lists because it's going to try to take car of all of them okay so it's up to
the that function I there was there a hand up here no oh
yes right the question is in the example without help where I have a list of
sentences why do I choose to see it as a list of sentences rather than just as a list of lists and use cter say map cter
over those things I could do that it really depends on the context so if somebody asks you to write
a program they're going to specify the data structures that you're working
with so um I could say you're given a list of
rational numbers and you'd like to know the greatest denominator so as the first
step of that you're going to find all the denominators and you would do that not
by saying map cter over the list of fractions but map denominator in order
to be following the abstraction even though cter would do the same thing and it would work okay so you just you know
if you're designing the data structure then you get to choose but you should be consistent you shouldn't sometimes use
cter and other times use budir on the same structure okay that's just a you know style
Point okay any other questions before I move on to the next exciting topic and say yes thank
you if you replace map with every well let's try it and see technically it's uh
illegal because the domain of every is words and sentences and not lists of
sentences but it might work let's see what happens
that's what happens so every um didn't
complain it applied but first to each element of the list but instead of using cons as the
combiner it uses sentence as the combiner so it has a flattening effect
so yeah you might want to do that um that's a situation where you're really going to feel torn you're going to say
boy every would do just what I want but I know that it's a data abstraction
violation to call every on a list of lists so what am I going to do and the
right answer is you're going to say
apply
append so we call map the result is a list of lists which isn't what you want
and and you call a pend so applies a function that takes a function and a list of arguments and
calls that function with all those arguments so it's like app pending all the pieces of the list of lists that map
gave you so this is the uh data abstraction
respectful way to do it instead of using every right
yeah why do you have to say apply a pen because
the result from map is one list of
lists if you apply a pen to one argument it doesn't do
anything okay you want to call a pen with the first argument being loves you
and the second argument being want to tell you and so on so you want to call a pend with three
arguments and that's what apply does it takes this list of arguments calls the function with those things as
arguments okay yes can you append something with an
empty list sure but it doesn't GNA it's not going to help you
any can you plan if you append whatever you get from map with the empty list you
will get back whatever you get from map the list of lists because it takes the elements of
the list of lists which are lists and makes a list out of those elements
so pending with the empty list doesn't help um a lot of these things by the way
you should be playing with stuff like this just you know every once in a while fire up scheme and ask yourself
questions like this I wonder what happens if I try such and such and see so you know one of the nice things about
studying computer science as opposed to maybe math is that often you don't have
to ask the teacher whether you got the right answer you can just ask the computer
that helps
yes how would you write reverse just using cons and not using a Pander list
um well one way is I could write a helper
function that's basically a pend um and the other way is uh I can write
an iterative process it's tail recursive procedure it
would be a helper function that takes two arguments which are lists and we call them in and
out and in each recursive tail call it transfers one element from in to
out and if you think about how that works you end up with the elements in reverse order when in is empty out is
the thing you want so that's why reverse is one of the few uh problems that's a
good candidate for using an iterative method because doing iterations just
sort of naturally reverses thing so often you'll try to do something iteratively and it'll come out backwards
of what you meant but in reverse that is a
benefit okay so you can do that it's a fun exercise
okay now for something completely different since we have
time this is Hurst
evue this is soda
Hall
and then there's a little air gap here but there isn't down
here so right here is a door why am I telling
you this you're in the 61a lab on the second
floor you're hungry time for lunch so you come over here you take the
elevator up to the third floor and you walk down the hill to
lunch that's silly stay on the second floor go all
the way to the end of the caror go through the doors that you see and welcome to etra Hall where there's an
exit right here that you can just go straight to lunch from and similarly when you come back
from lunch you can come in this way not from dinner dinner you have to go up to three um so so you know they have they
have cameras near all the elevators you may have noticed up like security cameras and you all think that's um to
avoid theft and stuff but really it's how we tell who smart enough to be a CS major people who go up to the third
floor in the elevator and then walk back downhill doesn't do it
okay any
questions all right we're gonna end early today see you
Friday\