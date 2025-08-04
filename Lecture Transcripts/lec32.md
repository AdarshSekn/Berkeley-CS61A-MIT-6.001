Transcript


okay good afternoon continuing work now
not continuing we're liftoff administrative announcement tomorrow's dim sum needed 10:30 outside the
Berkeley BART station or meet at 11:00 at legendary palace if you google
legendary palace Oakland the first hit has the address and everything okay I
put back up this chart of the three layers of abstraction about concurrency
control the wording is a little different when I said last time I'm abstracting away from my abstraction
my representation of the abstract version so up at the top it now says
protect a control abstraction so that's what chapter one was about remembers
control abstractions are the most basic control abstraction is a procedure and
that's what we're protecting with the serial Isis and scheme in this course
but objects are another kind of control abstraction or there could be other things in different programming
paradigms but in any event what you would like a user to see about this is
the ability to control concurrency with respect to whatever form of control
abstraction is in use rather than with
respect to lower-level things like machine language code and the middle
level has the idea of a critical section where we are talking about machine
language code and then the bottom most level is that there has to be some way to read and write the value of a memory
location atomically meaning that nothing else can break in in between the reading
of the writing
so and then right at the end of last time I put up the four different things that can go wrong and that's what I want
to go through in more detail today so incorrect results the key thing for
you to remember is what the definition is of correct and incorrect results
because in the kind of programming we're talking about here there isn't just one
possible correct answer there might be more than one correct answer but a
correct answer is one that is consistent with some sequential order of evaluation
of the different threads okay so that's not saying that you have to do the
thread sequentially it's saying you have to get the same answer you would have gotten if there weren't any parallelism
at all if one of them entirely happened before the other one started so it's
entirely possible that if a happens before B you get a different answer from when you get if behalf of before a
that's okay both of those are correct answers but what's not correct is
something that's neither of those okay
so in order to get to be assured of getting correct results we have to put
in concurrency control which is to say we have to put in some kind of
restriction on when things can happen in parallel um but if we go overboard with
this if we put in too much restriction then instead of incorrect results we're
going to get inefficiency where one of the threads is sitting there idling
twiddling its thumbs when it really could be working in parallel with the other thing and it would be okay yeah
okay so the question is is a result correct if it's the same result you would have gotten sequentially but you
got it through an incorrect process the definition of a correct process is one
that's guaranteed to give you the same result as you would have gotten sequentially it's up to the
implementation how to achieve that and still get you as much parallelism as
you can so it's kind of hard it's
something you have to learn through practice to get the right granularity of concurrency control if we just say
anything that has reference to anything in memory can't be in parallel with
anything that has reference to anything else in memory then you've done away
with the parallel capabilities of your system it's as if you had one processor
instead of a bunch of processors on the other hand if the control is to fine
grained then you might be able to get incorrect results so an example I like
to think about is the one about airline reservations because very often you have
to take two flights there isn't any direct flight from point A to point B and so you have to go by way of Chicago
right it's always Chicago unless it's LA which is even worse and
so you're requesting two different seats on two different flights and the
question is how should we put in
concurrency control for this so an example of something that would be to
course of a parallelism is
lonely except one request at a time for a given flight date okay
obviously you know if I'm trying to get from here to Boston and somebody else is
trying to get from Timbuktu to Kalamazoo there's no reason why we have to get in
each other's way and we're going to be looking at entirely different flights
and a lot of people want to fly on the same day especially if the day is tomorrow so it would be really bad to
have the parallelism dependent just on the flight date so then maybe it's the
flight number on a given flight date so
I'm going to be on flight 724 from here to Chicago on such-and-such a date now
and nobody else is allowed to do seat selection or actually to make a
reservation even because they might run out for that flight on that date in
parallel with me
well that's possibly too fine-grained
and possibly too coarse-grained so for example let's suppose two people are
requesting the same flight on the same date but one of them likes window seats
and one of them likes aisle seats and so we make different seat requests could
those be handled in parallel yeah but if
we use flight number and date as the criterion for parallelism then they
won't be done in parallel the other hand um since I'm going to be on two
different flights another situation that we'd like to avoid is for me to get a
reservation from here to Chicago but not get a reservation from Chicago to Boston
and that would be pretty bad I would be stuck in Chicago what could be worse and
so we really want to restrict parallel
access to both flights at the same time okay that's the sort of thing that might
make us actually want to say well only one person on a given a flight date
because of this need to have two different flight numbers and control
access to both of them simultaneously but the solution that's used for that
problem instead of trying to restrict against everything that happens on that
date is to say I want to serializers or
to mutexes at once one of them for my first flight and one of them for my
second flight and I shouldn't be able to make my reservation unless I got
permission to use both of those protected serializers at the same time
okay well that's a little tricky because
once you're asking for two serializers at once you run the risk of the third
problem which is deadlock actually there's a simple solution to deadlock for the case of flights so let me talk
instead about the examples in the book which is suppose I want to transfer
money from account a to account B in a
single transaction so I need to control
access to the from account and the to account at the same time okay so how am
I going to write that code so let's say that every account has a
serializer associated with it so I'm
going to say something like call from a
cancer Eliezer of to account serializer
of transfer which is a procedure and I'm
going to call that with from account to
account as its arguments okay so
everything from this parenthesis to this one is getting me a version of the
transfer money procedure that's protected with respect to both accounts
so any questions about what this is doing before we go on to what's wrong
with it okay no questions because you
don't understand or no questions because you do understand so got it sort of don't got it
okay some of each let me try again
supposedly were thinking about parallelism at all and I asked you to
write a procedure to transfer money from one account to another I want to transfer hundred dollars from your
account to my account let's say you
would write a procedure called transfer that would take two arguments the from account and the to account and the the
I'm being vague intentionally about what an account is maybe it would be the account number or maybe it would be some
object that represents the balance of the account and the account number and the serializer would all be in there
and so on so I don't care about that but you're going to write transfer from
account in some form to account in some form okay everybody clear on that but
the problem is resolving good okay now I want to worry about doing this in
parallel with other people doing transactions on different accounts and
we looked last time at how things can go wrong if two people are using the same
account at the same time if I'm trying to deposit money and you're trying to deposit money to the same bank account
at the same time one of our deposits might not actually happen unless we make
sure that those two transactions are serialized serial meaning one after the
other not the stuff you read for breakfast but more like a radio or TV serial where
there's an episode in another episode another episode one after the other so
if we if there was just a single account involved we would say my account
serializer of transfer and that procedure call calling the serializer
with the transfer procedure as argument gives us a protected transfer procedure
right remember that from last time so you call the serializer it takes a
procedure as argument and it returns the same procedure only protected now with
respect to other people using the same serializer okay unfortunately for
transferring if we just want to deposit or withdraw money that's fine if we want to transfer money from one account to
another there's not just one account involved as two accounts and we have to
make sure that nobody is simultaneously changing the balance of either of those
accounts okay who's still with me great
okay so one way we could do that is to just have a very broad kind of
serialization where nobody is allowed to do two transactions on any accounts from
our bank at the same time but that would mean that all the ATMs in this banks network minus one would be unusable at
any given moment so we don't want that we wanted to have a specific protection for this bank account except now there
are two bank accounts so what I did is I called in here
I called two accounts serializer on the transfer function that gives me a
version of the transfer function that's protected with respect to other people
using the to account when we're putting money into okay so we're safe as far as
to account is concerned but we're not safe about from account yet so I take the protected procedure that I got from
this serializer and use it as the argument to this serializer so now I
have a transfer procedure that's protected against the to account and is
also protected against the from account okay so this procedure that I've gotten
from these parentheses marked with a tick mark here what that gives me is a
version of the transfer procedure it's protected against both accounts simultaneously so if I win if I get both
of these serializers while the transfer procedure is running nobody else can use
from account and nobody else can use to account yeah does the order of the
serializers matter that's a great question only I'm not sure quite what question you're asking it's going to
matter a lot in a second when I talk about deadlock but as far as the protection aspect is concerned no if we
succeed in getting both serializers then it doesn't matter which order we got
them in okay the important thing is that we have both of them before we do anything substantive okay other
questions okay great so now you have the idea of
protecting two things at once oh you see how that would work in the airline case it would be serializer for my flight
from here to Chicago of serializer of my flight from Chicago to Boston of feet
reservation right got that so if I need to make a reservation on two flights and
it's no good to me to have one without the other I have to get both of them or neither of
them then we have to use both serializers in order to be properly
protected okay now here's the problem
with this what happens if thread a is
trying to transfer money from you to me
and meanwhile it just so happens that thread B is trying to transfer money
from me to you okay you get the picture
you and I are having battling ATM Wars trying to transfer money to each others
yeah and we want to make sure that the
result of this is consistent with them
happening sequentially which is first we transfer money this way then we transfer money that way or the other way around
in either case we transfer the difference between the two amounts from
the bigger amount guy to the smaller amount guy okay well what happens so if
you think about serializers being implemented in terms of mutexes which can control a critical section so
something that we say acquire the mutex run the code release the mutex all right
this when I call this procedure which mutex are we going to acquire
first from a counter to account to
account everybody says and I think you're wrong I think what's going to
happen is this when we make a serializer it says construct a piece of code that says get
my underlying mutex and then do whatever I'm protecting and then release my mutex
now in this case whatever I'm protecting is there is this inner procedure so when
we have both of these serializers on top of each other it's going to be acquire
from acquire to transfer release to
release from okay that's the sequence of
events within a thread okay now let's
look at the sequence of events looking at both threads at once this guy says
acquire the from account which is you
okay I'm being very hand wavy about the notation because the notation doesn't matter what matters is the idea here
so I say acquire you now it just so
happens that at that moment this thread gets to run it says acquire the from
account which is me this succeeds this
succeeds and now we're in trouble because this guy is going to try to say
acquire me which will fail because he's
got it and this guy is going to try to say acquire you which will fail because
he's got it okay so these two threads need two
different concurrency controls and they
acquire them in the other order because from each other because which one is trying to transfer money from me to you
yeah I was trying to transfer money from you to me and if we're unlucky one of them gets
one the other one gets the other and then they're both stuck that's why in
some of the earlier literature deadlock is called deadly embrace you can see what's going on these two threads are
each one waiting for the other one to finish okay questions about what the
problem is here is getting it great okay
[Music] that's a deadlock now how can we solve
this problem there are various ways
sometimes there's a natural ordering and if the different procedures use the
natural order inconsistently everything will be okay so in the case of the
airline with the two different flights I have to take the flight from San
Francisco to Chicago before I take the flight from Chicago to Boston right it
doesn't make any sense to them in the other order so if the software for
making a two flight reservation always first asks for the first flight and
second asks for the second flight then if two people are trying to make
reservations on that pair of flights they're both going to ask for the same flight first at most one of them will
succeed and the one that succeeds can then ask for the second flight and that
will work too okay there isn't going to be a deadlock in that case if everybody
starts with the chronologically first flight okay well that doesn't work for
bank accounts for bank accounts however we can impose an ordering arbitrarily
and the way we do that is you have a bank account number and I have a bank
account number so instead of saying get the from accounts utilizar and then get
the two accounts réaliser we're going to say serializer for whichever bank
account number is smaller and then serializer for whichever bank account
number is bigger and then do the transfer okay so that makes the code a
little bit more complicated you have to find out which one is bigger and if there's through this and if at do that
but it means you don't have a deadlock some cases are way more complicated than
this if you study databases CS 186 you
will find situations where you need half a dozen serializers at once and what's more sometimes you don't know
you need one of them until you've already done some computation with the other ones okay so if you know all the
ones you need ahead of time then it's easy to find a way to order them or at
least it's possible to find a way to order them but if you ask for you know serialize the racks and serialize or Y
and only then you find out that you also need to realize there W ok it's too late
to ask for them in alphabetical order yeah to serialize does not follow
applicative order no they do yeah ok
this is really tricky I'm glad you asked the question because I'm sure there's a hundred other people in the room we
don't get it and we're too timid to ask don't we he's looking at this code here
and he's saying because scheme uses applicative order don't we call to account serializer
first and therefore shouldn't we acquire
this mutex first the answer is yes to the first note of the second even though
it sounds like they're the same question because everything in between these tick
marks parentheses happens before we actually try to do the transfer okay and
because of that we haven't actually acquired any resources during this whole
computation although we've done is construct a procedure which when invoked
will acquire both of these resources okay only when we call this procedure
with these arguments do we start thinking about which mutex do we need first and the answer is to account
serializer when we called it generated
this piece of code okay from a counselor
realizer now says okay let me protect this with respect to the from account by
sticking a choir from at the top and release from at the bottom we haven't executed any of this code yet when we
call this function with these arguments we come in to the top of this code and do things in this order okay so yeah
it's really tricky but this really is the reg order in any event it doesn't
matter I mean I'd like you to understand this but as long as you understand that there is an order and if another thread
tries to do these in the opposite order you're going to get in trouble that's the important thing about deadlock okay
so some deadlock problems are very very simple and we can solve them by finding
or imposing an ordering on the different resources if you ask for a resource if
you need resources number you know three and ten and five you ask for them in the
order of three five ten okay and then everything works because if you get
three somebody else who needs the same combination isn't going to get three and
so you can go ahead and get five and ten without that kind of interference
sometimes it's more complicated for various reasons and so you can't solve the problem in that simple way so how do
you do it well when you study operating systems one of the things you will learn
about is some very very complicated hairy annoying convoluted algorithms for
trying to do analysis of the resource needs of different threads ahead of time
to make sure to try to make sure that deadlocks can't happen that's not what
anybody does in practice this is a trick
that we all learn from the database people who invented it first what you do is this you go ahead and write the code
and easy as possible way and you let that locks happen
footnote remember that a single concurrency hit where two processes need
the same resource at the same time is very very rare because your critical sections are short they take maybe a
microsecond to run so we're talking about two people in the same microsecond
needing the same resource so it's very uncommon in the first place in order for a deadlock to happen you
need two of those coincidences right so
the probability of deadlock in a particular situation is vanishingly small nevertheless since computers do
things very fast and we do things over and over again sooner or later you're going to get a deadlock so we can't just
say let deadlocks happen I wash my hands of it right people used to say that once
upon a time but it doesn't work instead what you do is you start up another
thread in parallel with everything else that you're doing whose sole job is to
poke around the operating-system looking for evidences of a deadlock so you look for oh this
procedure is waiting for this resource that procedure is going for that resource but wait a minute this
procedure has that resource we'll see you you find out that a deadlock is happening from the thread
maintenance databases in your operating system and then what you do is you just kill one of the processes say I'm sorry
you have to start over so let's say we
have a and be stuck in this deadlock over here um and the deadlock preventer
notice is this that there's that they're both waiting for each other and just kills a so that causes a to release your
account and therefore B can finally succeed at acquiring your account and
then a has to start all over again asking for your accounts and then my
account but now process B has finished so we're not going to have that same problem again in order for this to work
you have to be able to back out of a computation so when I said kill the
process it's not that simple you have to notify that process that it
is in a deadlock not that thread because
it's stuck but some other piece of that process which has to figure out if it's
in so why did we need concurrency control in the first place because we're
changing the values of things and there might be an inconsistent state in the
middle when we've partly changed something and not change the other parts okay so what we have to do at this point
is undo any changes to the database that
process a has made and release its
resources and then notify it that it has to start again from this call
by the way another solution that doesn't solve the problem of finding out halfway
through that you need a resource but does solve the other problems and this is something else that's done in practice is instead of having a system
call saying I want to acquire this mutex you give it as argument the list of MU
disease and you say I want to acquire this mutex and that mutex and I'm the attack from the other mutex all at once
and you leave it up to the operating system to worry about deadlocks and reordering of the requests if the
requests all come in as a block then you can do that you can do the analysis of
making sure that I can simultaneously acquire all of these resources sorry um
so um folks this is just scratching the
surface of how to handle deadlock and how to handle concurrency all together
you are going to learn this again more than once so our hope is that when you
get it the second time around with a lot more detail than you're seeing this week you will say oh yeah I remember the big
idea of this from 61a so I can now concentrate on the details of how to
make it work without having to learn what problem am I trying to solve okay that's our hope here okay resource
starvation the last thing on the list um I talked about this a little bit right
the end of last time it's the situation in which several threads want a resource
and somebody wants it over and over again and if that somebody gets it over
and over again so at any given moment there might be a bunch of threads all waiting for the same resource and if the
same one always wins then those other resources those other threads are never
ever going to get to run and that's called resource starvation it's okay if they're not a hundred percent fair if
you know thread/a wins more than half
the time you know that might seem unfair if they were human beings involved but
it's okay from a computer standpoint as long as the red bee gets to win eventually then it's okay but in certain
situations if you do your scheduling badly it might be that somebody way down
the list never gets the resources that it needs so one simple thing that people
do to prevent this is when the operating system is looking for who should get
this resource instead of saying let me start with process one and see if it needs it then two then three and work
down in sort of process number order you remember the process number that got it
last time start with the one after that and we're you know rotate back around so
that the same process doesn't get it twice in a row and everybody gets a turn but around that's called round-robin
scheduling okay so once again I'd like
you to remember what the four things are that can go wrong and have some sense of what they mean I you know I after the
final exam I don't expect you to remember any details about how we do
serializers in scheme and 60 okay that doesn't matter what matters is what is
the problem we're trying to solve what mechanisms do we have to solve it at
different levels of abstraction it's like what's a critical section you're going to hear that term again in other
courses and when the wrong how can we
solve the problem and you know that's really it so what
bounces correct and incorrect results under what circumstances do and don't you have a deadlock have some
understanding about the question of granularity of protection so fine-grained protection might give you
incorrect results coarse-grained protection might give you an efficiency trying to steer your way through that in
simple cases at least and finally just in the back of your mind when you're scheduling an operating systems
allocation of resources make sure you don't starve some process down at the end of the list okay so now I want to
talk about why we need these levels of abstraction in fact why do we need any
kind of support at all for serialization other than just plain old scheme code
like that up on the screen so this is an attempted implementation of make
serializer that doesn't work so first let's look at how it's supposed to work and then we'll see why it doesn't
so mixer realizer is the sort of the serializer class right it's the
procedure that makes an instance of the serializer the instance of the serializer that it's making is created
by this lambda right here which is inside a let and so in use question mark
is an instance variable but persistent state variable for each instance of
serializer in other words every serializer has its own in use variable which starts out
false initially the resource is not in use so the serializer is this lambda
where the cursor is blinking and what does it do it defines whoops it define
something called protected proc and that definition comes down to here and then
finally in this last line you know why this is doing this here we go
finally in this last line we return protected proc so the value returned by
make serializer is not I'm sorry the value returned by a
serializer is not the result of calling a procedure we're not actually going to
do anything to the underlying data it's just a protected version of proc which
was our argument we're going to return that so what is protected proc do well
it's written to take any number of arguments so that's why it's protective
proc dot args so args is a list of all the arguments so the first thing we do
is look to see if this serializer is already in use if it is already in use
then we have to wait a while this is of
course very hand wavy because I don't care about this aspect of it it means let the operating system know that my
thread is yielding up control and somebody else can run for a while now
and then when it's our turn again we call protected proc again this procedure
protected proc with the same arguments so we keep doing that we basically this
is the loop calling protected proc over and over again until finally in use is
false if in use is false then we start doing this stuff we set it to true so nobody
else can get in and we call the
underlying procedure proc with the arguments we have to use apply here because args is a list of the arguments
to proc so you can't just say proc args you have to say proc are going r2 r3 etc
and the way you do that is use apply which does take a list of argument values as you know so we do that call
the result result then since
called the procedure we can now set in use defaults and return the result okay
what's wrong with this code
yeah
how could it have an incorrect result
yeah okay so I would I would explain the
problem little differently he's saying what if two procedures get to get to this point at the same time
well that isn't supposed to happen because up here what's up here we check
to make sure that in use was false so if in use is already true we shouldn't be
doing this setback and they're right after each other as soon as we see that
in use is false we come right down here and the very first thing we do is set it to true but that's not good enough
because somebody could sneak in some other thread could sneak in in between
reading in use and writing in use okay
it's kind of hard to wrap your mind around this way of thinking we're you
know two consecutive instructions that's not close enough to prevent problems it
has to be one atomic operation so we're
going to have to have some kind of supporting mechanism to let us read the
value of in use and set the value of being used simultaneously the book
provides a simulated computer instruction you're supposed to imagine
that it's a machine instruction even though it's a team procedure called test and set bang that takes a memory
location and a new value it puts the new value in the location and it
simultaneously reads the old value and returns it so we can write this by up
here we would say test and set bang and it turns out they don't use variables
they use the car of a pair because the variable isn't exactly the same thing as
a mem locations for reasons that don't matter so I'm going to freeze this moment just
pretend it's a variable so they're going to say test if parenthesis test and set
bang in use true and what that procedure call is supposed to return is the old
value of in use and we can use that in the if now if we lose if somebody else
is already using it haven't we sort of cheated by setting the value to true well yes technically we weren't allowed
to set the value in use unless it was false but there's only two possibilities
either it's false or it's true if it's false then we can do what we want we've
won we're in if it's true and we're setting it to true we haven't done any
harm okay um let's you know what I
clicked so you might worry about what if
at the same moment I'm doing this test on set bang the other thread that has this resource is freeing it and yeah I
really have to worry about that too but I'm not gonna for our purposes it's
enough for you to understand why it is we have to be able to do both of these things at once now I'm talking as if
we're implementing serializers directly in terms of the hardware support but
that's not what the book does what the book does is it implements serializers in terms of a mutex a mutex as seen in
this chapter is an object something that takes messages and carries out methods
and it's messages are acquire and release
so the acquire method tries to acquire the mutex if it succeeds just return
returns whatever it doesn't matter what its return value is if it fails it keeps
trying it says they're looping until it can seed so aquire says see here inside this
resource until I they I'm able to acquire it and then you do the call to
procedure the apply proc args part and then you say you send their mutex the
message release and inside the mutex they'll be an in use variable that it
sets the true or false the advantage of having two levels of abstraction is that
you can write your higher level code without knowing anything about exactly
how your Hardware provides atomicity support you can leave that to the people
who write the operating system okay because there are different ways a test
and set instruction is one way but for reasons you'll learn about in 61 C it's
undesirable to have two memory references in the same instruction two
data memory references in the same instruction and so I want architecture
that I know about the MIPS architecture and 61c what they do is there are two
different instructions one that's called set this value protected ly and the
other that says okay clear the protection flag and what it does is the hardware associates an extra bit one on
off value with each word of memory and if you do this protected set it checks
that bit that one bit see if it's on or off if it's off go ahead and do the set
and turn on and that's all done in hardware if not it just fails and you have to come back and try again later
and clearing the bit just clears bit so
this means you're only doing one memory reference you're doing a set but this
hardware control only lets you do the set if that extra bid is zero so that's a whole
different way of making the hardware work it's not exactly a test and set because you're not reading what the old
value was you're just putting in a new value dang oh no I'm sorry I take it
back I'm wrong it is reading that you're doing so we do the protection directly on the variable X that we're interested
in not a different in use variable so we say read the value of X and set the bit
that says I'm using it and then you do your computation like adding 1 to it or
whatever and then you say protected set and the protected set will fail if
anybody else has tried to read that value meanwhile so it's a way of having
two different instructions that essentially work like a mutex that it's
like a hardware implementation of a mutex where the hardware has this extra
capability to ensure that you don't let another process read the value while
you're doing your computation and then when you write the value that automatically releases the mutex okay
don't worry about the details of that you don't have to know it yet well you have to know is the different kinds of
hardware do this differently and that giving us a level of abstraction in
between what the hardware does and the higher-order control structure that
we're interested in pushes the problem from the programming language down to the operating system to worry about the
particular kind of hardware that you're working on so you can write a program that will work on any hardware okay go
do tomorrow if you come to dim sum otherwise Monday
UC Berkeley