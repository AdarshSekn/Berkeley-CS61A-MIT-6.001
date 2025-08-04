Transcript


hi good afternoon um sorry I'm late drawing my beautiful picture here um let
me just finish this
up okay um today and Monday I'm going to be
talking about map reduce which is um a software
algorithm uh invented at Google uh that is now very widely used for handling
large collections of data out in the world by large I mean very large internet sized collections of data
um So the plan is today I'm going to show you not using map reduce but sort
of doing on a single computer what all the steps are in your map ruce and then Monday we're
going to look at the real thing um and what we have um the implementation of
this algorithm that we're using is called Hadoop it's an open-source version that originated at
Yahoo but a lot of people have worked on it and um some of uh your predecessors
as students have created a scheme interface to Hadoop Hadoop itself was
done in Java and you'll be seeing that in 61b or C um but here we're going to
show you the functional scheme version so first take a look at this picture
um which is about something that we do all the time um just in plain old single
computer functional programming by the way
um we are in a way back in the realm of functional programming although the actual map ruce is not purely functional
it does things um with sequential programming and mutation um and in
particular one of the things we're mutating is files on a a distributed
disk file system so we're given an input file and we produce an output file so in
that sense this is not functional because that's a kind of permanent product
of running napu but let's start just with a very very simple thing that
you've done a million times before um accumulate some function and some base
value um the result of map some other function
on the data so let's see if I can start up a terminal
here yeah so suppose I say
accumulate plus map
count
um okay so the first piece of that it's just this
if I copy that and then
paste we get for each word I've got to get you into my life how many letters
that word has and then we say Okay add those all up and the sum is
21 okay so that's a simple example of take some
data manipulate each value each individual value in some way that's the
map part and then do some kind of accumulation of the
result okay
um and that's um that turns out to be useful not only in little toy problems
like the one I just did but in great big problems um where you're trying to
let's say compute page ranks um or something you're you've got
all the data from all the internet sted on your disc because you're Google um
and you want to take each web page and compute some function of that web page
and then combine the results uh so as to get some useful
information okay uh but when the amount of data is huge we can't really do it in
the functional way uh in which we have all the data in a great big list in the
computer's memory and then map produces another great big list in the computer's
memory and then we accumulate the results from that that just won't work on you know industrial siiz data so you
already know part of the answer to that namely streams right streams are what
you use if you have huge amounts of data even infinite amounts of data although last time I checked the internet is not
yet infinite um but it's pretty close um so uh we're going to use
streams in our map reduce interface um
and the other idea that's important uh that we're going to use is the notion of
a key value pair so you've seen this before in um Association
lists right for tables so you have a table that's organized by keys and you
want to be able to find the value associated with the key so it turns out
that um map reduce is most useful if what
you're dealing with is key value pairs so in the simple version there's just
one map that goes through all all of your data one at a time so you know minimum
Theta in time right supposing it takes constant time to process one datum and
there's n of them it's going to be Theta end time um so now you have to imagine
that we have uh a number of computers uh in your case I think the
number of computers is going to be 12 or something like that when you do it in the lab more or less um but
in Industry it would be more like a thousand or 10,000
computers um and each one of them gets some key value pairs these key value
pairs are not in any particular order um so the way they're distributed among
processors is that separate from map produce we also have a distributed file
system so you can have something that you think of as one file that actually has part of it on this
computer and part of it on that computer and part of it on that computer so basically um to a first approximation
each computer handles the data that are already on its local dis um sometimes it's more complicated
because you have a computer that doesn't happen to have any of this file on its local disk so it asks one of its
neighbors to send it some data um so
the each of these Maps takes the same mapping function the
function I'm calling F1 here and F1 there uh it's the same idea it's the
function that's doing the mapping it's called F1 for two reasons uh it's a pneumonic name it's not just a you know
default name um it's F1 for one thing because it comes first you do the
mapping before you do the accumulation right Reduce by the way is just another
name for accumulate you'll find them both out in the world so first you do the mapping so that's F1 is the mapper
function um not to be confused with map itself which you know what that is
um and then uh later on you do the accumulation using F2 which comes second
the other pneumonic significance is that F1 is a function of one argument
right when you call map you have to give it a function of one argument as its argument and F2 is a function of two
arguments because that's how accumulate works right you take the value so far on
one new element and you combine them in some way because it's a combining operation that you're doing so that's a
two argument function um so we take F1 and we apply
it uh to one key value pair at a time
um and the result of that what the your mapper function has to return is not a
key value pair but a list of key value pairs um and that's
because a single input key value pair might give rise to one output key value
pair or more than one or zero because
remember when we were working with higher order functions back in week two um and later week five I guess there are
three of them right besides map and accumulate there's filter in the map
redu protocol the map stage can also do filtering it can take an input key value
pair and reject it so nothing comes out so what map returns for each element of
the input is a list of key value pairs possibly empty the reason there might be
more than one is is let's say um the value of some input key value pair is a
sentence uh you might because of the problem you're trying to solve need a key value pair per word of that sentence
in your output so however many words there are in this sentence that's how many key
value pairs will be in your list so that's different from um the single
processor situation where one input value gives rise to one output
value here it gives rise to a list of outputs um and
then uh this is a part that people sometimes find confusing map reduce really should be called map sort
reduce um because there's a stage that comes next that isn't in the name which
is sorting the key value pairs uh to bring together all the ones
that have the same key so here we have individual key value Pairs and after the sort we have one key
having more than one or maybe one or maybe zero but no zero ones get eliminated so at least one but maybe
more than one value attached to that key
um the confusing thing about this sorting is that there isn't to computer
that sits there doing a sort like insertion sort or selection sort or merge sort or any of those sorting
algorithms um instead what happens is um there's a
function that you tell map ruce that Associates a particular key with a
particular computer so when a key value pair comes
in um you compute f of that key which is usually something pretty simple like it
could be the first letter or the number of letters or something um and then that
tells you which computer to use for the reduction of that key so you're kind of throwing values at the reduce process
one at a time as they come out from the map stage so the Sorting happens kind of
in between everything else and in the same time as everything else
um so then what you do if you look at the right part of that diagram is you take the key values
collection and you take the key and just put it on the output so it's so map
reduce itself handles the key part and then each of the values associated with
that key goes into the reduce process so you're not reducing all the
values in the world you're reducing the values that have a particular key that's important because if you were
reducing all the values in the world um you couldn't do that in parallel
necessarily um that would end up being a bottleneck to the parallelization of
this process so each key gets reduced separately and so what we end up with is
not one value like the number 21 that got up there but rather um a stream of
key value Pairs and in the output from a duct from the reduced stage each key just has one value associated with
it um sometimes that stream of key value pairs is exactly what you
wanted sometimes you're going to have to do a further reduction to get down to
one single Global value but instead of having you know a million items of dat
to reduce over uh you've got it down to let's say 26 if you did if the key were
the first letter and reducing 26 things that you can do on a single computer in
not very much time okay so it should be
called map sort reduce okay questions about
that so far who's feeling
happy not
happy it's not too bad except for the hands that aren't up at all okay so um
we should now try to look at some actual
examples let's
um this this what I want
no that's what I
want okay so the first thing we have is um
yeah
yeah um the question is about what happens after the sorting and and um yes
in our map ruce implementation uh what you have is a key
with a list of values associated with it in the real map produce which is a
little different from this um the values don't turn up all at once
they turn up one at a time and each reduced process waits for a new value to come in
and when a new value comes in it computes a new accumulated value um
until finally it you know all the data have finished
um so in the real map ruce they don't actually make a list of all of them they just come in one at a time but in our
version yes okay so um starting point highlighted up there
we have an abstract data type called key value pair with a Constructor make KV pair and
selectors KV key and KV value KV for key value if that isn't
obvious okay um and now from this point on what
you're seeing is only to try to give you idea it's not
you know the actual parallel map reduce at all um there's this function called
group reduce that takes the F2 and the base
value and buckets which is a list of lists of key
value pairs
um and what it does let's pull this up up
here uh oops so we map over the
buckets Lambda subset make KV pair um so yeah each subset I'm sorry what what
buckets is is a list of key value lists
like what comes out of the sort so it's all of those things in that
column of key value value value combined and so what we do is is we do
sequentially what would really be done in parallel which is we take one
bucket that's a key and a value that's really a list of values so that one
bucket is called subset in here and we make a key value pair which we
take um oh I'm sorry I was wrong
huh what we have in buckets is a list of key value pairs in which
all the key value pairs with the same key are next to each other so each one
only has a single value so we take KV key of car of subset which is going to
be the same as KV key of all the rest of them so that's copying the common key
into the key of the result and then the value of the result is going to be
accumul at map KV value subset so map KV value
subset gives us just a list of values and that's what we accumulate so we're we're simulating the
fact that the key does not go through the reducer fact the reducer doesn't
know what the key is it's just looking at a bunch of values and it combines
those into a single value so that's the job of group reduce uh we also have in this implementation
uh sort into buckets sort into buckets say sort by
key so we get all the why are you doing this stop that thank you um so we get
all the KV pairs with the same key next to each other and then group is going to
find all the adjacent KV keys that have the same key and form a list of those so
we start with just a list of KV values we end up with a list of lists of KV
Bears okay um and I'm not going to show you group which is completely
straightforward you should be able to write that even though it's long sort by key um I'm not going to go into the
details either oh except for this thing called super before
um in order to sort you need a way to say this comes
before that or this is the same as that or this comes after that right in the
real map reduce the real map reduce takes a bazillion arguments um because you can fine-tune
it to make it more efficient for your particular problem we tried to simplify
away most of that uh flexibility um and so to do that we have
one comparison function that we always use and basically the comparison
function is if we're comparing two numbers then use a numeric
comparison if not use an alphabetic comparison okay that's the that's the
rule that's what all this
says Okay um here's another abstract data type
called a file um this simulates files in the file system
and a file consists of its name and the stuff in it and we're taking this stuff
in it as lines of text uh each line of text in a file will
be represented by a sentence okay all of the data in the
cluster that you're going to experiment with M produ on next week um we have a
bunch of data provided for you including um all the Shakespeare plays and all the
works of Charles Dickens um and uh all the names of beetle
songs um we're working on it's kind of a stalled project somebody may want to
help out with this later um taking a snapshot of Wikipedia and making that
readable by your programs uh but we're not there yet anyway so a file on the
disc consists of its file name which is a symbol and lines which is a list of
sentences okay
um so file to line list says take that file on the disk and turn it into a list
of key value pairs where the file name is the key for all of them and the
values are the lines of text so let's say we have all of Shakespeare's plays
that's one file per play so you'll have a file called you know Julius Caesar and
you know the evil that men do live after them the good is often te with their
bones new line so let it be with Caesar boom I come to bury Caesar not to praise
Him boom you know Etc okay um that one actually probably comes first friends
Roman countrymen let me that's a this was like 10th grade so a long
time ago um anyway so file to line list is going
to give us Julius Caesar friends Romans countrymen Julius Caesar lend me your
ears Julius Caesar I come to Barry Caesar not to praise Him Julius Caesar
for the evil Etc okay
um never mind match we'll come to that later okay and here we have some sample data okay so these are some fictitious
61a students and their midterm scores
um and then we have um file one file two file three um where
what comes first is the name of an album and that's the file name and what comes after that is names of songs and that's
the data one song name per value
um I don't have all of them I only have three okay
so suppose I say append mt1 mt2
mt3 I get this so it's all C A- something thing is
the key and some midterm score is the value and by doing this dis append I've
lost the information about which midterm is which but that's okay for my purposes
so now I'm going to actually do
um this and let's see if I
can oops all
right all right let's just try this okay that's a little that's good
enough all right so this whole thing is
a list of buckets and bucket if we start
here um goes to here that's the data for midterm
no that's the data for cs61a XB who only took two of the three
midterms and here's the data for XC who took all three here's XD who only took
one midterm here's XF XK Etc
okay um so sort into buckets has sorted this data by
um student
and now let's see what group produce does so I group produced using plus as
the accumulator and so what we now have is a list of key value
pairs uh one key value pair per student only one exactly one key value pair per
student in which the key is the login and the value is the sum of the midterm
scores so XB his his scores were 40 and 32 that added up to 72 XC got 27 + 25 +
28 uh which turns out to be 80 and so on okay questions so
far yeah uh is this how your scores are
calculated um well any up your scores yes map ruce no there aren't enough of
you yeah so a bucket is a bunch of key value
pairs that have the same key Okay so we've sorted the key value
pairs so that all the ones with the same key go together and then
um so then uh what was the name of the program that puts them in buckets let's see
um yeah group group takes a bucket like that and
makes it um
no no that's the result from group is is a a bucket per thing and that's what goes into the group reducer
procedure takes a list of key value pairs that all have the same key so um
the important part is that this group reduce models a bunch of reduces
happening on different computers okay so we only have one computer but that's what is going to
happen in actual map reduce so oops I'm up here
oh
yeah okay so what I did here is I took um a song title crybaby cry not chosen
randomly um and and imagine that coming
in at the Left End of the diagram and now what map does and this is a map
that's happening in parallel for all the different be albums is um make a KV
pair that has the word cry or baby or cry as the
key and one as the value why on Earth would we want a bunch of key value pairs
that have one as the value because that was a rhetorical
question because uh we are now going to accumulate those with plus and that's
going to tell us how many times the word cry appears how many times the word baby
appears so
so baby occurs once cry occurs twice okay
well okay let's look at file it's a line list of file one and see what that
actually does it gives us please please me the
album name I saw her standing there and then please please me
misery um and that's all I can read so
we'll and then please please me Anna go it's a parenthesis go to him actually um
Please Please Me chains Please Please Me boys please please me ask me why and so
on okay so key value pairs with the key is the album name and the value is a song
name so uh what good is
that
um so I'm going to take file to line list so key value pairs like you just
saw for three albums appended together and I'm going to call
this procedure word counts and we get
this um and notice uh this is an alphabetical order and that's because
the Sorting of keys onto reducers uh was in this example done
alphabetically okay um so
it's a long list um so the word love appears four
times tied with a um it's not actually the most popular
word which is going to turn out to be I with seven occurrences what oh me all
right me with eight occurrences so and you only has seven so
I guess that shows that the Beatles are more self-centered than is their image
um so let's actually back up here and look at procedure word counts and see
what it does so it takes files which is that
appended list of files and then uh we map um have you
seen flat map before
yes no who has hasn't seen flat map before okay we'll talk about it for the
moment pretend it just says map so what we're mapping is this
function which takes in a key value pair as it's input um and it Returns the result of a
map an inner map which is this one that Maps over the
values so for each song name um
um no I'm sorry it Maps over the values the value is a song name KB value of KB
pair is one song name so this function is mapping over the words of a song name
and for each word we say make kvp word one
so you know Love Me Do would turn into love1 me. one do. one throwing away the
album names we don't care which album a song is on for this purpose so we make a
bunch of ones and then we do sort into buckets so that all of the occurrences
of a are next to each other and all of the occurrences of me are next to each other and so on and then finally we uh
grew produced by addition and that's how we got this list of word
frequencies um and now
I can use that information
oops to find out the most commonly used
word um and that's done
with an accumulate done on a single computer
of uh the results of this
process so on a single computer we compare results I was able to do it on a
single computer because this is a very small amount of data um if it was the works of
Shakespeare then uh there might be a lot of words I
mean the elements of this list is still going to be only one per word of the
English language not one per occurrence of a word in Shakespeare so it's not as
much as you might be thinking but how many words are in the English
language 50,000 I'm guessing 100,000 something
like that a lot of words you probably know some tens of thousands of words
um and there's more in the dictionary that you don't know I mean that I don't know
either okay how are we doing on time
brilliantly
um oh yeah okay pattern matching is what's next and last let me let me back up and just kind of review where we
are um in these problems that I've been doing in the programs are all in my lecture notes and the reader and it will
pay you to go over them more carefully than I can do in an hour
um but we tease out explicitly three
separate steps so there's a map over all the
data and then there is sorted into buckets that does that middle step and
then there's group reduce and it's not just plain old reduce because we're not
getting one overall result we're getting one result per
key okay so that's what a map reduce really is it's a group reduce in
parallel of a sort in parallel of a map in
parallel okay let me pause for questions
okay nobody's going to come rushing up at the end of class to ask me questions right okay
um so let me show you match um
Okay match um is a procedure that takes two arguments uh the first one is called
a pattern and the second one is a sentence a pattern is a sentence but um
some of the words in the sentence might be asterisk and each asterisk means any
zero or more words so star I star her star means I'm
looking for a sentence that has the word I and the word her in that order but
maybe some other stuff and the result of this match is
true so and I love her it's also true
PS I Love You returns false
okay is that
yeah now each each asteris can match any number of words um so if you think about how this
match procedure actually works which I'm completely skipping over for now but it's worth you looking at because of
that fact that each asterisk can match a variable number of words and we don't know ahead of time how many um this
actually is an exponential time computation but luckily uh the way this
is going to work is that although we're going to call match a lot of times each match is dealing with a short sentence
so it doesn't matter that is it's exponential time over n equals 5 so that's okay
[Music] um so using match I have this procedure
GP GP is the name of a Unix utility program that you should know about if you don't it says search for a pattern
in the lines of a file um and so I'm looking for Star I star
her star in all these Beetle songs that I have uh and the
result is no this is right
um so the result is a set of key value pairs where the
key is the album name and the value is the song and for these three albums the
only ones that matched are and I love her and I saw her standing there uh which are the examples I showed you
before and all the other Beatle songs on these albums didn't not match this pattern okay so you can see that this is
actually pretty useful um the ability to look at a lot of data and
select values lines of text for us that include you know certain things and
certain combinations um we're uh we being Dan Garcia and I
are are writing a proposal to the NSF to get a lot of money to help disseminate
uh cs10 which is the beauty and joy of computing um so everybody tells us that
proposals have to have good acronyms so I used grep the Unix grep
yesterday to search for English words that have the letters BJ consecutively
in them um and so our proposal is called frabjous
CS um okay so that's the last example I'm going to show you um I hope you get
the idea of how some of this can be useful I'd like you also to get the idea about this trick of
um using a value of one out of map for everything and then using plus to count
things that's something that is a you know comes out of of the Google paper the Google paper that introduced the map
ruce algorithm is in the reader um you should read it it's interesting uh let
me in the three remaining minutes tell you that
um problems for parallel computation uh come to a first
approximation in two flavors easy and hard um and the easy ones are the ones
in which the data decompose in an obvious way so you're doing a lot of
computations but on each data in isolation um map ruce is great for easy
parallel problems um parallel algorithms is a
topic of a lot of research right now and um the researchers aren't thinking about
the easy problems they're thinking about the hard problems and how to make those manageable so people who are really
parallelism researchers say oh M ruce trivial um but it's the starting point
for everybody in studying how this works because when the Google guys invented map ruce they looked at all the programs
that they were running every day and found that some huge percent like two-thirds of them um were expressable
in terms of map reduce and I should have said this at the beginning but here's why that's
important um let's let's say you have a great big problem and you're trying to
solve it on 10,000 computers so you've got a great big Warehouse someplace that
has racks and racks of PCS hooked up in them okay and even with all this
parallelism this program is going to take all day to finish right because the internet is
huge um what's going to happen during that
day with 10,000
computers you guys aren't this admins one of them is GNA
die right you know your computer dies
every less than 10,000 Days probably and one computer for 10,000 days is like
10,000 computers for one day in terms of the probability of failure which is very very very high so it used to be the bad
old days at Google that every programmer had to build into every
program a lot of code for what to do when a computer fails how to find out
that a computer has failed and how to redistribute its work among the other computers and that was so so hard that
you had to be a genius to do two plus two at Google scale and they could only
hire genius programmers map ruce varries all that under an abstraction layer
so the map reduce program itself worries about how do we divide the problems
among the computers what do we do when a computer fails all of that stuff is written once and for all and that means
that ordinary people like me most of you um can do parallel
processing on a large but not complete set of problems okay Monday we'll look
at the real thing have a good weekend
UC Berkeley