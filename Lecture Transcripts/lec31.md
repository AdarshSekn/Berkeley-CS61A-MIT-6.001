Transcript


afternoon I'm a little slow getting
organized here okay what we're going to be talking about for the rest of the week is things that can go wrong in
computations that happen in parallel and what to do about it so to start out I
have to teach you a little bit of 61c
let's say you say this set bang X 2x
plus 1 here's what that looks like in a
typical machine language there'll be an instruction that says
load and then a register name like
register 8 that's one notation for it X the reason
I picked 8 is in the MIPS architecture the one they use in 61c registers
starting at 8 are used for short term values that are being loaded in the processor just for a moment and you'll
see why that is in just a moment and I'm going to say add immediate immediate
means the thing we're adding isn't in some memory location that's in the instruction the actual value we're
adding is in the instruction so add register 8 1 and then store register a X
ok so that sequence of 3 instructions is what the computer does to add 1 to X and
it goes through that load and store thing because a typical computer there's
the processor over here and the memory over there and they're two separate pieces um so you may have had the
Ariane's for example of getting a computer and then going out and getting more memory for it right you go to the
store and you get a little board that you can plug in that has more memory and you don't have to change the processor
to do that you just add memory because it's a different piece of the machine inside the processor itself there's a
teeny little bit of memory like typically 32 registers and machines on
your desk today 32 is a very small number right the the memory of your
computer is measured in gigabytes billions of bytes and here we have just 32 values the reason for putting a small
bit of memory in the processor is that the registers can be really fast
so there's a trade-off again you'll learn more about this on 61c there's a
trade-off between size and speed for memory so we have a great big memory
that's billions of bytes that by processor standards slow meaning you
know you can only read a billion read or write a billion times a second let's say
and then in the processor itself you have a teeny bit of really really fast
memory that during that one cycle of reading or writing the main memory you
might be looking at those registers six times to carry out an instruction okay
so we take X out of the big slow memory and bring it into register eight in a
small fast memory that's inside the processor add one to the register and then store the result back okay
so this little load and store architecture typical of how machines work um okay so the problem comes up if
we have some form of parallelism in
which there are two different threads doing things at the same time so
that could happen because you have a dual-core processor right which a lot of
you do so there's a dual-core processor or more almost everybody okay great so
in your machine there are these two processors independently carrying out instructions let's call them a and B and
let's say that a is trying to do set
bang X plus X 1 and B is trying to do
set bang X I don't know plus X 3 okay
now these happen to be happening at exactly the same moment so what happens
is these things are not just 1 all at once operation each of them takes three
steps load add store so let's well first
of all what should happen what answer should we get after these two
instructions have been done let's suppose that X has the initial value 100
which is the value B when we're finished 104 right we should do both things ok so
now what happens oh I should explain each processor has its own set of
registers even though they have the same memory okay that's how they're able to work independently so let's say the
sequence of events moving down the chalkboard is this this machine says
load register 8x and then this machine
comes along and says load register 8x and then this machine says
and I register 8:1 and I register 8 1
and finally store register 8 X store
register 8 X okay so here's time moving down the
board we load X which has the value 100
into register 8 so register 8 in processor a now has the value 100 then
we load X into this machines register 8 so it's register 8 also has the value
100 add 1 so that makes it 101 at oops
sorry add 3 so this makes it 103 store
it into X so X now equals 101 and then
store this into X so we get 103 instead of 104 ok buy these things interleaving
in this way essentially one of them didn't have any effect that isn't always
the result but what always does happen is some kind of wrong answer in this
case the possible wrong answers are 101 and 103 depending on which one gets in
there first with the store right it's the order of the stores that really
matters it doesn't matter which load happens first we get into trouble as
long as the second load doesn't come
after the first store so if these things overlap at all then we're going to get a wrong answer
okay questions about this so far yeah is
there ever a problem with them trying to access the memory at the same time so what if the two load instructions happen
absolutely at the same time one of them wins probably the same one all the time
the interface between the processors and memory will be set up in such a way that
somebody wins you know this first we look at processor 1 then we look at
present to it I don't think it's possible for the hardware door really
try and do both loads exactly at the same moment yeah is this a work with
local variables no I'm envisioning that
X is a global variable or it's an element of an array it's some shared information it could be local provided
that the thread separation happens after
that local variables created because typically threads will share whatever is going on at the time that the second
thread is created ok so it doesn't really matter if it's global or local if
each process has its own local X and they're in two different places in
memory then it won't be a problem ok yeah so that's something to emphasize um
this is not going to go wrong very often
ok a computer can typically carry out a billion instructions a second that means
these two sequences of three instructions have to overlap within
three billion of a second okay so almost
all the time one of them will completely finish before the other one starts you might
think that's good that this isn't a very important bug since it hardly ever happens but no actually it's bad because
in computer terms hardly ever means you
might have to wait a day before if the situation arises because we're going to
be running this program over and over and over again typically it's not going to be just one thing X that we said once
and that's the end of it this is going to be inside a loop that you know is doing something a rather a bazillion
times and sooner or later we are going to have this problem and when we do have
the problem your program is not going to
instantly crash it's not going to say oops sorry two things happened
overlapping you lose what's going to happen is that it's going to compute an incorrect value and it's going to
proceed with that incorrect value and maybe twenty minutes later the
inconsistency of an incorrect value will cause some other piece of your program to crash so concurrency bugs like this
are really oh I got louder are really really hard to find in your code it's
much much better just not to have them in the first place so that's why this is
an important topic because especially those those of you who take operating
systems this 162 or databases 186 you
are going to be doing a lot of things where concurrent operations like this come up and you're going to have to be
able to prevent that kind of bug otherwise you're going to spend really
long all-nighters in the lab the night before the project is due tracking down
this bug it only happens once every three million times or something no I don't
mean that a third of a billion times okay so it's important that you get this
idea of concurrency in your head firmly lodged and so when you're writing code
you're just automatically going to say oh wait is this a concurrency problem
right here let me put in a solution at a time and we'll talk starting now about what the solution is
so one solution is just never to do things in parallel go back to the days
of you know you only have one processor in your computer it's not a very good
solution because parallelism is the way computers are going to get faster in the
future it's about that we're going to have faster processors it's that we're going to have more and more processors
inside your desktop so a decade from now you might have a hundred processors in
your in your little box instead of just two or four and also parallel parallel
computation happens on a larger scale than just the Box on your desk so my
favorite example everybody's favorite example is airline reservations okay
have you read the occasion I've had the occurrence that you are making a
reservation for a flight and you click on seat selection and up pops a map of
the airplane and you pick the seat that you want and then it says oops sorry
that seats taken right has that happened to anybody yeah why did it show you that seat is
available if it was taken well it was available at the time the computer drew
the map but somebody else was making a reservation for the same
fight at the same moment and clicked on the seat before you did well that's
pretty bad you don't get the seat you want but it's not nearly as bad as if both of you got that seat right that
would be kind of a disaster so the airlines have to worry not about
concurrency within one computer but concurrency across all their servers all
over the world so you can't just say
let's not have parallelism as a solution to the problem instead what you have to
do is have the idea of a critical section you have to say these three
instructions are uninterruptible okay
once we've done this load nobody else was allowed to look at X until after
this store okay now that's not the same
as just saying let's not have parallelism because if the other processor is adding one to a different
variable Y then they can interleave and that's perfectly okay they just can't
both be using X at the same time so this is what's called a critical section and
what you want to do is in some fashion before you do the load you want to say I
reserved X I have dibs on X and then you do the load the add the store and they
say okay I'm finished with X somebody else can have it now all right yeah
so what does it mean to say I'm reserving X it means that if another
process is executing either this same code or some other piece of code
involving the variable X when it says I reserved X at the beginning the system
the operating system or somebody the hardware or whatever will say no sorry you have to wait and that process will
just wait right here until your process says release X okay
oh yeah the X is still there just nobody's allowed to look at it for 3
billion of a second um okay let's take a
little bit of a look I'm going to say
load 61 a live con current and then I
can show you um how this works so let's
go ahead and set up the exact situation that I was talking about on the board
okay parallel execute is a procedure that takes any number of arguments and
those arguments have to be thunks that is to say procedures with no argument
kind of like the callback procedures we looked at on Monday and it will run them
in parallel the way this worked is parallel execute actually has a little
scheme interpreter inside it that switches very rapidly among the different alternatives so I'm going to
say lambda of nothing sorry set bang X plus x1 close this up then
close the lambda and lambda nothing set
bang X plus x3 close because okay what's
the value of x now look it's 103 we got the same wrong answer that we
anticipated okay so how do we fix this and in the book they provide a high
level mechanism for saying this entire
procedure call should be protected against using X now the way you do that
actually you don't say I'm using X instead I say I'm going to put X back to
100 then I'm going to say define X
protect to be make serializer so make serializer is the constructor
for an abstract data type called serializer and what if serializer does
it takes a procedure as its argument and it
returns a protected procedure okay so
for every variable that might be shared I'm going to have to have a separate serializer so this is exes protector and
there would also be wise protector and diseased protector for those other variables so now I can say parallel
execute X prot of Glenda nothing set
bang X plus x1 goes the plus goes the
set that goes Glenda close the X prot and X pot of lambda nothing set bang X
plus x3 close close close close close
and now if I look at the value of x its what it's supposed to be 104 okay so the
serializer has prevented those two threads from overlapping when they're
both trying to use the same variable X so questions about how a serializer is
used yeah
where did I tell the serializer which variable to protect I didn't I just used
the correct serializer for these procedures so I looked at this
code right here I the programmer I said oh this is a critical section with
respect to X I guess I'd better use X's serializer okay more typically you might
have some abstract data type called a protected value that would have two
pieces to it the value in the serializer so you know maybe I would say call car
of X with the argument lambda nothing set could er X 2 could er X +1 so car
would be the serializer encoder would be the data you could do that but the
serial Iser doesn't no scheme doesn't know I the programmer know that X prot
is the serializer for X that clear yeah
what would look like if I ran a trace on parallel execute it would be messy and
it would use features of scheme that we haven't talked about so I don't recommend it as far as you're concerned
you're supposed to imagine that there's two pieces of hardware doing these two
threads you can have as many threads as you want by the way in parallel execute and they all run in parallel but what it
would really look like is a scheme interpreter or a little bit like scheme one only more complicated because it has
to be able to switch back and forth among threads yeah
ah question is suppose I call X prot on the first Punk for the first thread but
I don't say X prot for the second one well I still get 104 and no it's the
serializer that enforces the fact that only one of them can be running at a
time so if the second one cheats and doesn't use the serializer then it can be running at the same time
okay so they both have to serialize those in fact they both have to use the
same serializer in order to be protected against each other yeah
he's saying since there's no real connection between X prod and X couldn't
I use Y prot that's supposed to belong to Y to protect X yes you could but then
what you're doing is preventing a thread using X and a thread using Y to run in
parallel okay once you do that you might
as well just not allow parallelism period so basically what you have to
imagine is you and your spouse have ATM cards for the same shared bank account
okay now a bazillion other people have ATM
cards for other accounts at the same Bank and people are constantly using
ATMs all over the place so if you and your spouse happen to show up at the
same time to do a transaction it should make one of you wait but if you and I
with two different bank accounts show up at the ATM at the same time it shouldn't make one of us wait okay you want to
have just the right amount of protection not too much not too little we'll get
into the topic more in a second yeah
so if instead of using X praat I had said make Sur realizer here and also
make serializer here then I'd have two different serializers and they would not
mutually exclude each other so now it has to be the same one and that could be
a let you know so it could be local but that kind of defeats the purpose you really want it to have the same scope as
the variable it's protecting right okay
let me move on okay so we actually have
a set of abstractions about
serialization looks like this is my
abstraction diagram
so this is make serializer up here and
this is something we'll talk about in a moment called make mutex and it's
separate these things separate the levels so at the bottom is atomic test
and set so we'll see that in order for
this protection to work you have to be able to load the value of something and
store a new value at the same moment that nothing can get in between the load
in the store okay so you're like exchanging values between the processor
and the memory atomically so test me is you have to be able to look at the thing
that means you have to be able to set it this isn't being used for X it's going to be used for X product up here
ok so atomic test and set is typically provided by hardware in some form we'll
talk a little bit but not very much about how that works in different
situations right now what I want you to see is when I was showing you what the
set bang translates into I said we want to be able to say at the beginning of
this I reserved X and at the end I'm releasing X somebody else can have it
now as two operations the start and end of a critical section that's not what I
showed you is make serializer make serializer the start and end points are
implicit and what I'm saying with the serializer is protect this procedure
call okay so it's serialized is a more abstract mechanism than the
mechanism that says I reserved acts and now I'm releasing acts that mechanism is
called a mutex the word stands for mutual exclusion right because it these
two processes exclude each other from using X so make mutex uses atomic tests
and set we'll see how that works in a bit to create something called a mutex and that gives you critical sections
this level of abstraction is typically provided by your operating system so on
your computer you're running you know looking around the room Mac OS or maybe
you're running Linux or maybe you're running Windows each of those systems has a mutex mechanism in it you can say
allocate limit X and then you can say start of critical section for this mutex
end of critical section you may have
heard and if not you will in literature the name semaphore for this level of
mutual exclusion semaphore is like a mutex it's a little more complicated
because it has the ability to let
exactly three processes use this resource but no more than three so the
first 3 acquire the mutex operations would succeed and then a fourth one
would fail why on earth would you want something like that well you wouldn't in a situation involving reading and not
changing the values of variables but let's say in the lab there's three
printers right next to each other and you want all your different computers to
be able to say okay I want to print the document you don't care which printer it goes to
so the first three people want to print something win and the fourth person has to wait until somebody finishes printing
that's the kind of situation where you would want to semaphore people hear the word semaphore more than
mutex the semaphore was actually invented first I think that was the beginning of thinking about critical
sections by the way everything that I'm
telling you now was well understood by computer scientists in the late 50s I think mid
fifties despite which it's only quite
recently that operating systems are more or less free of concurrency bugs so
those of you who have Windows computers if you're old enough you may remember
getting in the old days the blue screen of death fairly often white fairly often
meaning once a day or so right that's in the pre Windows NT windows systems
mostly the reason for that was concurrency bugs and the same was true
of you know the UNIX kind of systems and and Mac systems and everything until
maybe the 70s or early 80s all these
systems were full of concurrency bugs because the people writing the operating systems were not the computer scientists
who knew about this because in those days remember you couldn't major in computer science like when I was in
college I was a math major even though what I really majored in was programming computers and being a disc jockey but
technically I was a math major and I never heard anything about concurrency until much later except in certain
ad-hoc situations where I would know about certain things that had to be protected okay so operating system gives
you the ability to delimit a critical section with a beginning and an ending and then
typically you would have a protected procedure lets or you might have a
protected object if you're programming in an object-oriented language an object
you'll recall has a collection of methods for all the different things that knows how to do and a high level of
abstraction for serialization might be only one thread at a time can manipulate
this object so all of the methods of the object would be protected by one
serializer okay that's a fairly typical thing to do and that level of
abstraction is provided by a programming language okay none of this is cast in
concrete so you can take atomic tests and set and invent serializers directly
on top of that these three levels don't have to be Hardware operating system
programming language they can be the work can be divided up in some other way but this really is pretty typical of the
way modern systems deal with concurrency okay questions about the picture
okay let's see where are we now
oh yeah the book characteristically
works its way down it starts by showing you as I just did here's the feature we
want we want serializers and then it says okay how can we make serializers we
make them out of mutex and how do you make a mutex you do that of atomic test and set um
it's almost but not quite true that you
need must have some kind of hardware support at that lowest level to provide
the atomic read and write operation it's not quite true you can look up google it
if you're interested a way of doing concurrency control that's entirely
implemented in software with no hardware support except the usual you know add
subtract load or kind of operations but
the algorithm is pretty complicated convincing yourself that it really works
why it has to be complicated in just this way it's even harder and as far as
I know nobody actually uses it in practice it's one of those things but you know you invent for your PhD thesis
and everybody says isn't that nice and they go on doing things the easy way which is to have some hardware support
the hardware support is not necessarily a machine instruction called test and
set as it is in the simulated system
that the book talks about for instance
if we're talking about internet scale parallelism like you're the airline you
know you have these servers all over the place it's not just one server there's a bazillion of them and they have to stay
synchronized um the atomicity at the lowest level turns
out to be provided by networking hardware that makes sure that two
packets coming into your computer can't step on each other at the same time that
just keeping the packets separate is the basis on which we end up providing
atomicity okay so that's very different from looking at one particular location
in memory there are the kinds of low-level support for parallelism - I
don't care that much about the low-level I care about what we build on top of it
except I guess I should say in the old days when I was your age there was
hardware support for parallelism and it was a very primitive kind basically it
was okay turn-off parallelism altogether
firm offered this block of code so you instead of having a critical section
regarding the variable X you just have critical sections period and then
sometimes the things you want to do in a critical section are long that's not so good you don't want to sort of turn off
time sharing the ability of the computer to do different things at once for a
long period of time not even long in computer terms and so what you would do
is you would use that primitive turn off parallelism altogether mechanism to
invent a guaranteed atomic test and set on which you would build mutexes and so
on okay so these days we have better Hardware support but in the early days
of thinking about it they had a much more limited kind of hardware support
and we're still able to get the job done
used to be back then by the way well it's still true actually that operating system programmers get
paid more than all the other programmers because they have to understand this
parallelism business that's starting to change nowadays everybody has to
understand parallelism because application level programmers are creating threads and have to not step on
each other's toes so now everybody has to understand it but it used to be that
only the operating systems people really understood anything about parallelism okay all right so when we have
concurrency the last thing we're going to do today and will continue this Friday is talk about four different ways
that things can go bad and they are
incorrect results that's the worst case
right that's we get 103 and we should have gotten hundred four by the way what
counts as a correct result when two programs want to modify the same
variable and lots of different outcomes are possible how do we decide which
outcomes are okay and which ones aren't answer the result must be consistent
with some sequential order of carrying out the operations so you can do things
in parallel but you have to get the same answer you would have gotten if you
didn't have parallelism if you did this thing and then you did that thing separately now that still might be more
than one possible correct answer so if instead of adding one to X and adding
three to X we say add one to X and the other one says multiply X by two okay
only come over here and do that so one of them is computing + x1
the other one is computing times x2 ok
and X starts out at 100 what if we do
this one first than that okay 101 202 right what if we do this one
first and then that 100 200 201 okay so
these answers are correct the possible
wrong answers in this example are 101
and 200 in which effectively one of them
happens the other one doesn't happen that's that interleaf situation we saw over here okay so there isn't just one
correct answer necessarily there could be several correct answers of several
wrong answers we have to get a correct answer so incorrect results that's the worst thing that can happen it's better
that your computer crash then that it gives you a wrong answer you may not
think that's true I mean what's one wrong answer now and again but the wrong
answer sort of build up on top of each other over time you get longer and longer and longer and you know
eventually you really get in trouble about it whereas if your computer crashes you figure out what the bug is
and you fix it and then everything works well from then on out unless your
computer is running a telephone switching system it's the computer you
talk to when you pick up the phone and get a dial tone for those computers
getting an occasional wrong answer meaning every once in a while connecting you to the wrong telephone is better
than the system shutting down altogether for everybody right but for most computations
incorrect results of the worst thing that can happen next one is inefficiency a particular inefficient a particular
kind of inefficiency the one in which we fail to do in parallel things that could
be done in parallel so that's if you just have one serializer protecting
everything right so not only can't you and your spouse use the ATM at the same microsecond
nobody two people as if there's only one ATM in effect in all the world so that's
not good the third one we're going to talk about is an interesting problem called
deadlock this comes up I'm not going to
give you the details on the two minutes but here's the general idea this comes up when you have two different threads
and they both need to use X&Y thread a
acquires X thread B acquires Y and then
neither one can proceed until the other one finishes that's a deadlock also
sometimes called deadly embrace in the early literature and finally this is too
short a name for it but this is what I call it in the notes unfairness in which
process a always wins okay now a little
bit of unfairness is not a terrible problem if process a wins more often
than process B so what but if process a keeps requesting resources over and over
and over again and process B never gets to run at all that is a problem so we
have to make sure that everybody gets to turn once in a while okay we'll talk more about these things on Friday to you
oh and don't forget dim sum Saturday
UC Berkeley