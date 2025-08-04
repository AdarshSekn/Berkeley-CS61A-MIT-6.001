Transcript


okay good afternoon um two administrative things
one of them on the board over there um we are interchanging the lecture topics for
Wednesday and Friday we're going to do the lazy evaluator first analyzing evaluator second um this is an
experiment the reason for it is the Tas all think that uh there's more to talk
about in discussion section about the lazy evaluator so they want you to have that lecture before discussion section
so don't get confused um secondly we're getting in toward the end of the
semester um so it's important not to be late about things at this point because
uh your readers are also students and they have their own end of semester crunch the same as you do uh and it
really makes things a lot harder if things getting late and in particular the grading complaint deadlines are
speeding up so there grading complaint deadlines that are in the first day handout and also in course reader volume
one right at the beginning um and you'll see that there's like three of them almost on top of each other and just a
reminder you're complaining about both missing grades and grades that you think
are incorrect um so don't if you have a missing grade don't wait for it to show
up before you complain because you'll miss the gr complaint deadline and we don't want that if we have a problem
problem about grades uh we'd like to know about it in a timely manner so we
can try to fix it um okay that's it for
administrative things back to map reduce so uh these are the same pictures that
were on the board last time um and again remember that uh F1 is
called F1 because it happens first and because it takes one argument so so the
mapper function takes in a key value pair a single key value pair as its argument
and it returns a list of key value pairs that could be empty or uh could have one
thing in it or could have 20 things in it um the reducer F2 uh comes second
it's a two argument function it takes an accumulated soar value Val and a new
value and combines those um to produce a
new value so far um so the one important difference
that you can easily get tripped up on is that the mapper function gets a complete
key value pair as input the reducer function just
gets a value and the reason for that that is very often we're going to use some
simple function like plus as the reducer and that wouldn't
work if we had key value pairs um so the reducer never knows what key corresponds
to these values and it shouldn't have to know um the reducer
function should be associative for those of you who missed out on high school
that means uh a function B function C should be the same as a function B
function C it's possible to have non-associative reducer functions but you're then you have to start worrying
about exactly what order things happen in and it's best if you don't almost all
the time the reducer will be plus or times or word or sentence or a
list uh I'm sorry or cons not list or con stream um
okay uh all data are in the form of key value pairs we talked about that the
reason again for key value pairs is that sort operation in the middle which looks
at the key and doesn't look at the value to do the Sorting um and so the reduction is on a
per key basis that's why key value pairs matter in the map reduce process um stop
me if I say something you don't understand um oh stop that what do you
mean DHCP okay does that mean this still works yeah oh look at that what a
surprise okay um so we're doing things in parallel
that means each processor runs its own map and each
processor runs its own reduce that's how we get the benefits of parallelism that
we're not not trying to do the entire data set in a single process so that's
just easy to forget in the uh scheme of things
um so how do we know which values from the file go into which
mapper the answer is it really doesn't matter the key value pairs initially at
the Left End of the diagram are in no particular order and you just get random ones and that's okay because your mapper
function F1 is only looking at a single key value pair at a time it doesn't do
anything Global with respect to the entire data set that's the reduction stage that thinks about sort of the big
picture um and each of the reduced processes is completely separate from one another and
because of that instead of a single result as in the simple One processor
case where accustomed to what we get is a stream of key value pairs where each
value is the result of combining all the initial values for that key um oh and
finally the key that in the key value pairs that your map returns doesn't have
to be the same as the key of the incoming data so we'll see in most of
the examples we do where we're looking at text files the key is the file name
and the value is one line of text from that file in what comes in and most of
the time we just ignore the file name uh which is the initial key and we make up
new keys which are the individual words or something like that
um okay and the reason that map that I'm sorry that your mapper function F1 has
to return a list of key value pairs is that um the map stage is also the filter
stage so sometimes you'll return an empty list and also sometimes you'll
split up an incoming line from a file into multiple key value pairs for
example one per word very common thing to do um
right okay oh yeah and the Sorting uh I've
only drawn one big tall box in the picture but the Sorting is done in parallel also it's a bucket sort that is
to say as a mapper function outputs a key value pair um the sort piece of map
Ru sends that key value pair to the right processor for that particular key
so we get all the all the key value pairs for a single key together and that
becomes the input to reduce okay oh that's what I didn't put
in the diagram I knew there was something
F2 goes to all the reducers and Bas of
course okay um
all right so since each reducer gives us
um only part of the result what map reduce returns when you
call the map reduce function is a stream of key value
pairs um and it's um generally speaking a sorted stream
sorted by by key okay that because that's how in the
actual map underlying map R software um it's possible to specify the Sorting
algorithm how you decide which key value pairs go to which processor um but
that's one of the things that we kind of sweep under the rug in our simplified map rce
interface okay questions at this point that's all pretty
abstract now we're going to start running code once we start running code I'm hoping it'll be clear what's going
on and maybe you'll have questions so
SSH to icluster and you'll log in I'm sorry I cluster one is what you can
connect to do eek no CS I
think okay that did you um
right maybe it does matter or maybe I'm not on the net
anymore let's find out it's eeks all right eeks yep and you might get a
message like this so I'll say yes okay great um so you will log in
with your class account and it's the same password on icluster one that it is when you log in in the
lab um
SDK okay
um oh yeah I didn't talk really about the last argument to mapper do so F1 is
your mapper function F2 is your combiner function for the reduction base is the
base case that the that the reduce starts with and then instead of a list
of data as in the simple example on the left um there actually two things that
can be used as that last argument to map reduce one is in quotation marks a uh
file name on the distributed file system of icluster which is a cluster of several machines so that's one thing you
can do um and the other thing you can do is use the result from a previous map
reduce um which is a stream of key value pairs so if you say Define
Fu uh to be map reduce blah blah blah then later on you can say map ruce F1 F2
base Foo okay uh and some of the problems that you're going to be doing in the lab
require you to do that that there's two passes through map ruce before you actually get the answer you wanted in
the first place um okay so let me actually start with
the um very simplest possible example and see if this
works I'd like to just look at what's in a file on the distributed file system so
I'm going to try to use a map reduce that essentially does nothing okay it just passes all the
inputs on so um ah so here's a good pop quiz if I
just want pass all the data through what should I use as
F1 yeah the identity function Lambda XX agree
disagree yep you're all wrong okay everybody who thumbs up is wrong because
F1 has to return a list of key value pairs so in this say it's going to be a
list of length one I'm just going to say list because if you call list with one argument it does what we want
here okay so that's a little tricky thing to remember um what am I going to use for
the combiner I'm going to use cons stream because I want to get a stream
out um I'm going to say the empty stream um this is kind of a half
constam actually in truth is treated specially by mauce it notices that you
said kstream um and it treats it as a special case because the sort of natural way to
do an accumulation is right to left and you can't exactly do that for infinite
streams so it has to go left to right to come out right no J's making faces at me
what oh you think this isn't going to work it
does oh maybe you think it goes all the way to end well we'll see well maybe we
won't see I'm not quite sure how to find out except by having a function that
prints something here the way they do in the book when they introduced streams in the first place I wanted to show you how it works okay so I'm going to put in a
file name um slash
Gutenberg slash
Shakespeare this is actually not the name of a file it's the name of a file directory and there's a file per
Shakespeare play in it um it says Gutenberg by the way because this data
comes from something you want to know about called Project Gutenberg which is an effort to get
um every public domain major work of literature
online um it's a volunteer effort people scan in books um and fix the mistakes
that the OCR made and make text out of it so what you're about to learn I hope
uh the only thing bad you're about to learn is that the disadvantage of our map reduce implementation is that
there's a very large setup time so this is a map reduce that's doing nothing basically there's no computation
involved um when I start it it says
working but by the way okay so that took about half a minute so
that half a minute was almost entirely startup time um now the sad thing
is that uh you can't really
see the data here uh because of these
premises um
oh it looks like doesn't it that um this
is that the of the in the key value pairs the key is a name of a play or
poem or something and the value is a stream of lines of text from the
file so I would like to say um show
stream sorry oh okay
um oh yeah good point uh but I still have to map show
stream mod for these things to get the text so lamb
of D value pair
um no I just map wait I'm sorry map show
stream over get last map reduce output and that's in case you
ranom map produce and it took a long time and you forgot to save the result so let's see what this does right
oh whoops oh yeah okay thank you stream
map show stream over get last oops map
reduce output close close
close all right well now we still have some
huh I wonder why that didn't
work yeah should well anyway it doesn't matter okay so what we're looking at
here um of course oh that's right um so we have a stream of reductions by
play so this thing that says A midsummer's Nights Dream Dot promise
that promise is a stream of all the lines so I probably mean three levels stream map show stream of stream map
of show stream of stream map of showst stream of thing would probably work but
I'm not going to try it I just wanted to let you know that you can get to the files out there and that this is what a
um kind of not really doing anything map ruce call would look like if it would be
list as the F1 and it would be um const
stream as the F2 I could have just said cons and then I would have gotten lists
and then it would all be visible but it would be a lot of lists because one Shakespeare play has like thousands of
lines so I really wouldn't want to go through them all just to prove to you
that that file is out there okay um
all right actually what I really wanted to do let's see if I can do
this of course
not yeah
okay well this is bad I didn't really want to load it um okay we'll see what
happens but what we're doing um yeah no this is bad let's stop
this
how do you stop a
okay there we go govern prer has no
process okay let's try again
okay so here's word count mapper word count mapper takes a key value pair
whose key is um
a name and whose value is the text um so
what I want to do I've taken here a very small file called Beatles song and I'm
going to find out how many times each word appears it's the same thing that I did last time on a single processor but
now we're doing it in map reduce so word count mapper uh looks at KV value of an
incoming key value pair and it Maps over that Lambda of word make key value pair
word one so A1 hard one days one night one all
right um like that and then
we call map reduce word count mapper is the F1 and just plus is the F2 with a base
case of zero so now if I
oops hey what is this so
here I'm just going to do it the easy
way there
okay oh whoops return all right so here we go um map ruce and progress working
blah blah blah and this is a really short file so
it won't it's going to take the same 30 seconds or so that uh the other one took
um so this map reduce interface is a work in progress and oh that's pretty good that was way less than a minute um
that was like a quarter of a minute um it takes a while to start up because it
has to send your environment out to all the worker machines before it really starts doing anything so let's go ahead
and show stream word counts
um so if this doesn't look like a sorted list it's because
um our idea of a word on a line is anything with spaces in between so this
is the word open parenthesis go which comes from the song Anna parenthesis go
to him Clos parenthesis um Sergeant Pepper Lonely Hearts Club
Band repri right this is she's a
no what song is this um She's So Heavy what's the the real
name yeah um okay anyway so here we finally
get to a which occurs 17 times there's one across that's across the universe
Act Naturally um after one after 909 all
there's lots of those there's all you need is love and all my love and um anyway am only one of those that's
interesting uh I am I said must be
anyway okay so that's word counts um and
now uh oh yeah so so here's the example that I did
before on Beatles songs um
okay so find the most commonly used word
um okay so here we go um and while it's working
oops here's mapper and reducer the mapper says um oh it says something very
strange it says make KV pair first of KV key KV pair KV
pair all right so that's a really strange thing to do why are we doing this so we have
for example a key value pair
um that says [Music]
um okay so the album is uh with the
Beatles um is that right wait first of KV key of
KV oh it's on word count never mind you're right thank
you starting over Okay so we've done word counts already we're not looking at
the raw data so we have something like
um um
what was it that there were seven of all yeah okay so we have something like this
and now what we're
doing is we're using that whole thing as the value for a key value pair
whose key is a the first letter of all so that's what this has to do that
sounds like a weird thing to do right why on Earth would we want to do
that well think about the reduction we want to find out what's the
most common word alog together we'd like to do that somewhat
in parallel right we don't want to have just a single reduction because there's a b zillion words um and that would be a
bottleneck so we want all these computers reducing separately but it
doesn't do any good it's a little bit like in uh concurrency control where you have to pick exactly the right
granularity of uh what to put in a critical section there's no critical sections here it's all functional but
there's this same kind of granularity issue we have um somewhere on the order
of 10 computers to work with if we have a process per individual
word all we're going to find out is that the most frequently used word in the
word all is the word all so the parallel reduction wouldn't be
helpful on the other hand if we just merge everything together then we're
only using one of our 10 processors to do the reduction so the compromise is
that I used is to say okay let's divide this into order of 26 sub problems so an
a problem and a b problem and a c problem and so on so we'll find the most common word that starts with a and then
another reduced process we'll find the most common word that starts with b and so on okay so when we do
that um show stream
frequent we get this um the most common word that starts
with open parenthesis is repri oh if they're ties we just get one of them it doesn't
matter the most frequent word that starts with one is one most frequent word that starts
with it is or is there one oh yeah the one after 909 the most frequent word
that starts with nine is Revolution number nine nine um the most frequent word that
starts with a is a so so far you might be forgiven for thinking that this and
this are always the same but the most common word that starts with the letter B isn't the letter B it's the word be
the most common word for C is cry URS three times um crybaby cry is two of
them and I don't know what the third one is um I'll cry instead ha
um the most common word for D is do um Love Me Do
uh right anyway sorry um okay so and so on
up to Z now at this point we have a stream
that's really short even if there's 20,000 English words there wouldn't be
in the names of Beatles songs but let's say we were doing this as you will in lab for the works of Shakespeare and
there are you know in the order of tens of thousands of different words probably in Shakespeare by the time we've done
this parallel step we're down to 26 modulo a couple of punctuation things so
now we can do a single processor reduction um and get the answer but we
haven't yet talked about um how the reducer works we talked about what the
mapper does it makes things that look like this so what does the reducer do and here's
the tricky part remember I said that the reducer doesn't see the key it only sees
the value right but the way I've set things
up here the value of this yellow key value pair is the white key value
pair so the value that the reducer sees is the original key value pair that we
started with so therefore or in the reducer function this is the function F2
find Mac reducer um current and so far are key value
Pairs and we compare the two values if current is greater we pick current
otherwise we pick so far so in the case of ties it's whichever one we saw
first okay so that gave us frequent um and now
I'm going to take the result of that I'm going to stream map KV value
frequence so that gets rid of these letters that I don't really care about
so we're turning the nested key value pairs into just plain ordinary key value
pairs um and then we use f Max reducer to find the most frequently used word
and the base case um value
is this fake key value pair in which the value is zero and that is never going to
happen in any of the ones that really are in the Stream frequent because if a word appears zero times you know we
aren't going to see it at all but that's what we use as our starting value for the reduction uh and it turns out um
that uh the most frequently occurring word is U at 22 times when we did it on
Friday with just the first three albums uh you'll recall the most frequently occurring word was I not you
um and uh so what that says I guess is that the Beatles got less self-centered
as time went on um see you can learn interesting things
by doing this stuff okay [Music]
um okay
so I would like to find the total number of lines of text in all of
Shakespeare okay so
um let's start this running and while it's running um we'll say okay
the the reducer that's straightforward forward that's just plus the um mapper takes a key value
pair returns a single key value
pair in which the key is the word line
and the value is one so for each line of text in Shakespeare we're returning
exactly the same key value pair so all the reduction is being done
in parallel now um so we turned every line of Shakespeare into a single key value pair
um now if I look at um
will if I say actually I can say show stream will and you'll see that it's a
stream of length one because there's only one key so it all got reduced the total number of lines of text in
Shakespeare according to Project Gutenberg is220
51 okay so that's what you're aspiring to if you want to be a important English
writer um okay one of the things you're going to do for us is
modify this example so that it tells us
how many lines are in each Shakespeare play um and this is the result that we
want this is in the lecture notes so you can try out your program to see if you got the right answer by seeing if your
answer agrees with our answer so each Shakespeare play is on the order of two
or 3 th000 lines of text looks like
okay um
so what are you going to take away from this lecture all after all these examples turn into a blur I'm not like
spending a long time on each one because they're in the lecture notes so you can go back and look at it at your leisure
um I'd like you to take away a couple of things one is that without very much
trouble at all we can do useful parallel computation for you know a fairly wide
range of problems and again as I told you last time not every problem lends
itself to this kind of easy data parallelism something things you have to
work a little harder at or a lot harder at um but a lot of things do lend
themselves to data parallelism and we're looking at some examples and for those ones using the map ruce
mechanism um does what abstraction is supposed to do
remember this whole course is about abstraction abstraction basically uh is
a process of enabling you to think in terms of of the problem you're trying to
solve rather than thinking in terms of the limitations of computer hardware
right so in terms of computer hardware below the abstraction barrier of map
ruce we have to think about the fact that computers sometimes fail we have to
think about the fact that these files are actually distributed over several different computers we have to get the
data from the computer that has it to the computer that needs it we have to think about exactly
what basis the Sorting is done uh we have to think about all these different things we have to think about the
construction of streams out of the results um because you know Hadoop the
map ruce implementation that underlies this doesn't know about streams it knows
about just iteration and emitting one value at a time and we have to turn that
process into something that looks like the kind of stream that we've been working with so all of that stuff is
swept kept under the rug of this very very complicated to implement but simple
to use abstraction so that's Point number one point number two is how to
master this key value pair business so that you know whether you're thinking about a key value pair or you're
thinking about a list of key value pairs somebody should make up a good name for that comparable to farest but I haven't
thought of one sorry not an associate no no no that's a
I'm sorry not a list of any old key value pairs a list of map rued key value pairs it's a little different from an
association list but yeah kind of it is that idea
um and um when you're thinking about just a value okay so you have to keep that
straight in your head including screwy cases like this where the value from one
point of view is a key value pair from another point of view what this should remind you of is the implementation of
two-dimensional tables right it's got nothing to do with two value tables but
there's this situation where you look at something from from above it in the data structure it looks like a
value um in a key value pair when you look at it from underneath it looks like
a whole one-dimensional table right remember that this is the same kind of thing if you're looking at it from the
yellow point of view this thing down here is a value but from the white point of view it's a key value
pair okay um so those are the big sort of takeaway points and then just looking
at the details of this seeing how we did it um and that's about it boy I talked fast
today okay questions yes
yeah no in in that example it doesn't reduce in parallel so he's asking about
finding all of the lines in all of Shakespeare uh and in that case since I
use the same key for everything it is going to be just one reduce process so
uh one of the things that you want to do is make that more efficient um which we could do by the same trick I used here
about the first letter and so on that kind of thing okay so thinking about how to make something efficient is you know
part of what you ought to be doing uh this is kind of a deliberately bad but simple example for you to build on is
that a hand up or you're just fidgeting no okay other questions
yeah where do we implement the breaking it up into the the looking at the first letter okay that would
be um
right
here so I'm making a key value pair whose key is the first letter of the key
of the original key value pair right so the key value the the key
of the original key value pair in this example was the word all first of all is
a right not first of all but first applied to all is a so that's the key of
my new key value pair the value of my new key value pair is the entire
original key value pair okay so that's how that works yeah
ah okay no um the question is about the in the original input file data and how
that becomes key value pairs um the file that you're working with so
this you know Gutenberg Shakespeare thing um is not just a bunch of text
it's already been kind of lisp ified so that it has key and value by the time
you see it and that's part of the implementation of map reduce is that it
when you call it with a string as the last argument so it's a file name it
says oh okay this is a file name I'm going to take this file and I'm GNA make a stream of key value pairs whose key is
the file name and whose value is one line at a time of text okay so that again that's another
thing that's sort of swept under the rug here um but you're right to to ask about
that because if you look at the Google Map reduce paper um they have different
formats of keys and values for different situations and that's one of the things
you have to kind of work out
yeah okay so how do we compare in the reducer how do we do the comparison
well we're doing a greater than
of the KV values not of the entire thing so
remember again current and soar are yellow
values which is to say white key value pairs so that's how come we can take key
value of it KV value I mean of it which is this seven so what we're comparing is
this seven with some other number for some other word does that answer your
question um what the reducer sees so if you look at the picture
um this is going to be the letter a and then each of these values is going
to be you know all do 7 and a23 and whatever okay for the different words
that start with a
questions oh try to remember to to try to keep in your mind a distinction
between what's how Map rce works and what's how my particular example works
okay so that business about the first letter that's not built into map ruce I could have done it in better ways if I
were really really really serious about parallelism if I were Google dealing with all the data in the world um I
would notice that assigning each letter of the alphabet to a processor means that the
one that gets Z is not going to work as hard as the one that gets
a right there aren't very many words that start with Z so I would say well maybe that's not such a good way to do
it maybe I should have you know three three processors for the letter A but I should
have one processor that's doing you know uvwxyz
altogether um so that's the kind of thing that you know we're trying to
simplify your life by not being absolutely as parallel as we possibly
can but on the other hand not being not parallel at all either
okay other questions
no questions okay I hope that means that
you're all happy about this so oh yeah one just final word about this whole thing and I said it Friday but can't say
it too often um this map ruce this is a
function okay so we're taking parallelism and doing it in a way that's
fun functional which means there's absolutely no danger of these different
processors stepping on each other's Toes that whole business about critical sections doesn't apply to the user of
map reduce the implementation of map ruce is not the least bit functional it's full
of state what's the state of this machine and that machine and this process and all that stuff there's a lot
going on under the surface that's not functional but it's done in such a way
as to present you with something that is functional and that vastly simplifies
the use of parallelism that's why map ruce you know is such a good tool okay
see you Wednesday
UC Berkeley 