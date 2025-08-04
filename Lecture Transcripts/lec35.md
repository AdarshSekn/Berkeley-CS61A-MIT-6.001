Transcript


okay um our topic today is um software
reliability um or software engineering or the social implications
of computing and we're looking at a case study which is um the most famous
computer software disaster the most studied uh disaster ever um although not
the worst actually um but the worst that we really
understand very well and that's the theak 25 so help me out who actually read the
paper oh good all right so I can pass quickly over the background
um the Thea 25 was a um a therapeutic x-ray machine that's different from the
diagnostic ones that you've all had applied to you probably by now um it's
much higher radiation intended to burn out a cancer
um so this machine had six occasions when it
accidentally delivered a huge overdose of radiation um four of the patients
involved died the other two were very very severely injured
um because of software bugs and
um if you're me the first thing that comes to mind when you hear that story is well let not write software like that
um but that's not a good answer because the th 25 also saved hundreds of lives
of cancer patients for whom it didn't uh overdose accidentally um so it would be
even worse not to do it than what happened um but what happened was bad
enough yeah
no there were only six known cases of Overdose um yeah most of the time it
worked great um and the Machine that it replaced the previous model worked
without failures um so the company had a long
history of successfully building these machines um but this particular model
was not not successful in that way and
um I hope you got the point from the article and I really want to emphasize that this is not a story about bad guys
who you know callously put prophets ahead of lives there are plenty of
stories like that um the canonical story like that is the Ford Pinto um who knows
the pinto story ah very few of you okay this is before you were born um the pinto is
this little car made by Ford and it had the problem that if you
rear ended it there was a very good chance of the gas tank
exploding um but what's interesting about this story is that Ford Engineers figured out
that they had this problem before they were any actual explosions the Ford Engineers went to
the Ford Management and said look should recall these cars and fix this management said no it would cost too
much okay uh so they got sued um for you know hundreds of millions of dollars um
and uh you know lost the case deservedly um so that's a story with bad
guys but the theak 25 story has no bad guys um everybody involved really wanted
to save lives that's what they were there to do um and so this is instead of
being a kind of morality play story this is a story about how hard it is um to
build software large scale software that works
um why is that um we understand a lot about the
process of engineering and Engineering software
you know if you look at it sufficiently abstractly is just like engineering
anything but actually it's very different um because the other Engineers
work with material things and those things have known limits so um Hardware
you know rusts out or wears out or you know the battery stops being able to
take a charge and stuff like that um and software doesn't have that kind of
degradation to it and it also doesn't have the limitations that you have when you're physically building things
footnote um Hardware people are getting to the point where they can build things
on the level of complexity of software because they do their building in software so now they're building
electronic circuits where a switching element can be a single molecule and once you're at that scale
uh you can build very very very complicated Hardware uh that's has the
same possibility of failure as the very very very complicated software does but
with software there's no limit to how big a thing you can build because it doesn't take any physical space doesn't
use any you know iron or steel or selenium or whatever
um and so the sky is the limit and that's why even though software doesn't
degrade it's still has more problems rather than fewer problems than Hardware
so if you think about bridge building um you can probably count on
your fingers how many Bridge failures there have been in recorded
history right um you know yeah there's the Tacoma arrows now who can name
another one right um and that's because there's only so
many ways to build Bridges and the bridge Engineers learned them and they designed
conservatively um and so things by and large work
um it's pretty amazing that computers actually work pretty well um when the
first Intel Pentium came out um I don't know if you know this story there was a bug in floating Point
division so certain problems you get slightly wrong answers
um and this happened because um they put the machine through rigorous testing and
rigorous analysis and it was completely right and it passed and right before
they started building them some engineer uh figured out a kind of shortcut a way
to speed things up in the division algorithm and unfortunately that way to speed things up didn't actually work um
so it was a last minute change that made the hardware not work but we just expect
software not to work it's different from Bridges right I mean when you you know use a computer every so often you get
the blue screen of death or the spinning beach ball of death or whatever it is depending on your operating system but
there always is one and you just say oh well that's how computers are reboot
right um Bridges aren't like that
you know Rockets aren't like that airplanes aren't like that you can't reboot an airplane um people expect them
to work every time [Music] um
so why um because software is hard because there's no limit to how
complicated it can get that's sort of the big first thing to understand is um
we build these massively complicated programs way more comp licated than anything Hardware people can do uh so
that's where we run into trouble um oh yeah I'm supposed to tell you the
Star Wars story um who knows what the Strategic
Defense Initiative is oh lot of you good um this is like
back when Reagan was President so what around the time you were being born more or less um they said we are going to
protect the United States with an invisible shield um of satellites in space that
will detect and shoot down any missiles that might be aiming at
us um and this software this this these
satellites are going to have you know weapons of mass destruction in them that can be used to
shoot down these missiles um and they're going to be entire
autonomous well um the program that they were going to
write to control these satellites was about 10 times bigger than any program that anyone had ever written
before so a bunch of computer scientists said this is going to be a disaster
right um and you know we can't let this happen and so they did things like testified before Congress about what a
bad idea this was um and that was the beginning of an
organization called computer Professionals for social responsibility um which was modeled
after a group called Physicians for social responsibility which was a an anti-war group that their focus was on
War as a public health hazard which of course it is
um but cpsr Focus um was on
um computer systems as a public health hazard basically and
um there was a lot of reason for them to be terrified because this was back in
the days when there was the US and the Soviet Union were the two big Powers pointing missiles at each other and each
side had enough nuclear weapons to blow up the world a hundred times over or
something um it really ridiculous um
and there were it turned out later we found out dozens of occasions on which
World War II almost started because some computer thought we
were under attack or they were under attack they had their dozens too you know um we know more about our dozens um
and in every case um the supposed attack
turned out to be um a flock of geese or just some random airplane you
know or just playing a radar Hardware malfunction and the reason we didn't
have World War III in each of those cases was that a human being had was the protocol for starting
World War III required a decision by human beings so the computer would raise
an alarm and then some human being would look at it and the human beings thank God said oh yeah I never I've seen this
situation before it's a flock of geese and not push the button um but now they
were going to have these satellites push their own buttons um so that was the first time that the
issue of software complexity really came to public attention as you know something that really really
mattered um well
not many of you are going to end up working on software projects that are
explicitly life and death right you're not going to be working on therapeutic x-ray machines I
hope you're not going to be working on automated weapon systems
um so you might think that this doesn't apply to you but you know in my notes it
says there's a continuum from theak at one end that's obviously life or death
and video games at the other end that are obviously not life or death and then there's stuff in the middle like
operating systems um at one point the tanks in Iraq the US tanks in Iraq were
running Windows this was a long time ago they were running like Windows 2,000 or
something you know um so that was life or death and it wasn't you know the
people who wrote that oper anyway um today this is a change from my notes
things keep changing um there's nothing no job you can do about which you can
say um thinking about the safety of of this program doesn't matter let's say
you're writing a video game today that video game is almost certainly web
enabled right and that means that um other people on other computers
whom you don't really know are going to do things that affect the running of your
computer and um so your software even if
it's game software has to be written in a way that's going to uh
not do any damage to your system even in the face of deliberate enemy attacks
right I don't mean by enemy like enemies of the US I mean you know some teenager
in Finland who wants to break into your computer
um so everything software reliability of everything now matters because of the
net um okay so what went wrong in the theak
and this is the meat of that article that I asked you to read and there was so many different kinds of things that
went wrong and here are the ones that I found
um no Atomic test and set so this is the thing we were just learning about a week
ago um that the software was multi-threaded or there were external
events that would cause it to jump to do something else and
um critical sections were not protected now as you know when you have that kind
of bug most of the time it works because most of the time you don't have these
two conflicting things happen at exactly the same time and that's why most of the time the
theak worked right because this kind of concurrency bug didn't happen except
once in a while um
Hardware interlocks removed that was a cautionary tale uh if you remember um
the previous model thak was really running essentially the same
software but it had a little Hardware widget a a limit
switch mounted on this turntable that controlled the aiming of the
X-ray um that would make sure mechanically that certain combinations
of uh settings couldn't happen the software was also checking
for that error so somebody said you know we can save a couple of bucks per
Machine by leaving off this Hardware because the software is doing the job for us um so a very important lesson of
that is redundancy and I want to really underline that because in 61a we always tell you don't do error
checks assume that your input is correct and and we do that because we want to
simplify as much as possible the examples in this first course um but I'd
like you to know that in the real world you should put in error checks even when you think that some particular kind of
error can't possibly happen check for it anyway
um and um by the way when an error check
does detect an impossible error uh you have to tell some human
being about it right so they found out afterwards that those little mechanical limit switches on the old model theak
were saving lives you know month in and month out saving lives
um by silently preventing uh overexposure but it didn't ring any
bells or you know print a message on the console or anything like that it just
silently fixed you know took care of the problem without fixing it um so make
sure you have a an audit trail of everything that happens um so
that when a problem does come up human beings find out about it and can
diagnose it and fix it um there were a lot of user interface
problems so user interface was the subject of that alen K video that we saw um until
relatively recently people didn't think of user interfaces as part of computer science
at all you know computer science is about
algorithms and how we deal with users that's you know somebody else's Department
um so what did they do wrong uh one example example that actually was still
the case in a lot of software that we used until pretty recently um is there's
the little arrow keys on your keyboard to move the cursor around um it turns
out it those things don't sort of hard wearily move the cursor around your
screen those keys generate a sequence of characters that get sent to software
which interpret the characters as meaning move move up and send back a
message to your screen to your display controller saying move up or down or
left or right um well in The theak Operators would fill
out blanks in a form the way you do in web pages and they would you know get
partway through the form and then notice a mistake they had made higher up and they would hit up Arrow up Arrow up
Arrow up arrow and the little cursor would move up and then they would overwrite what used to be up in that
line and think that they were changing a previous entry what they were really doing was putting the string up Arrow up
Arrow up Arrow up Arrow up arrow in this field down here because that's how the software was written so the moral is
that what happens on the screen should correctly reflect what's happening inside the
program that was one user interface mistake that they made
um defaults so if the operator is filling out that
form and just hit return enter on an item without saying anything uh the
software would assume some default value pretty common even today um and
most of the time that's okay but not when we're talking about therapeutic
x-ray doses um in that kind of system we've learned you don't have a default you make the
operator enter a value um and finally too many error messages
if youve used Windows you know about this problem um if every time you do something a
little window pops up saying you know warning blah blah blah blah blah
eventually you stop reading those things you just click yes you know okay okay um
and that's what happened with the theak it gave a lot of error messages for
situations that weren't really errors and The Operators came to understand this so an error message would pop up
they would just not even read it and then a different error message would come up that really was something
important and they wouldn't notice they were just in the habit of getting return
um documentation this is probably the biggest problem you
ask any software company is trying to get people to write documentation and
have it right have documentation that's readable so you know how
um I keep thinking about Windows but it's not just Microsoft it's everybody
um a dialogue pops up and it says um
how many gble fliters per inch would you
like and there's a little question mark button so you say oh good I can get help
so you click help and a window pops up that says this screen wants you to enter
how many gble fitzers per inch you want and that's the help message
um there were situations like that in the theak too where the documentation just didn't help people
understand uh what was going on and
finally and this is sort of the human interest part of the story here in the
article um when these cases first came to light nobody believed it right the
company that built these machines said you know people use this machine all the
time and it you know always works something went wrong this
particular time it must be that the operator made a mistake um anybody ever heard that
recently this failure was due to operator error people still say it all the time
look in the news whenever you see some disaster involving computers some PR
person is going to say this failure was called caused by human error
um well sometimes times they were just wrong it was a computer error it was
just an error that didn't happen very often other times technically they were
right technically the human operator did something that he or she shouldn't have
done but the software was designed in such a way that it encouraged that kind
of operator error by having bad defaults or by not behaving in the way that it
looked like it was behaving the things that I was talking about in the user interface so
um one of the takeaway messages is anytime anytime you hear somebody say
operator error um you should be very very very skeptical because what that means is
that some billion dollar company is trying to scapegoat some $10 an hour
worker uh for a problem in their system um
so why was the company so defensive partly it's just human
nature you know I say you just killed somebody you don't say oh H okay I'm
sorry um saying it wasn't me right um so that's part of the problem
that has to be overcome in other part of the problem is um lawyers anybody going
to be a lawyer when they grow up here really no okay you can close your ears
for the next couple of minutes um it's much much harder for
anybody to say yes I take responsibility for this
situation if the next thing that happens is they're going to be sued
um how many of you drive a car right in your mail when you got your car
insurance you got a little pocket guide for what to do in case of an
accident and the very first thing it says is do not admit
responsibility right um well okay that's a good way to not get sued but it's not
a good way to encourage responsible behavior so that's a problem um
and then after they finally the company finally said that they did have a
problem they fixed it they found a bug and they fixed it and they sent out
revised software glad that's taken care of and then they had more
failures right so there were half a dozen independent problems they were
found one by one you know
um so that's problematic too
so how do we fix this I I have an article that um is assigned reading in
my social implications of computers class uh that's from well it's about a company that does
software Consulting for NASA were building some software for the space shuttle at the time this article
came out and you know in that context the software has to work the first time
right um it's no good to have a space shuttle take off and then discover a bug
by the shuttle exploding that's bad um so this company undertook to have
software that worked the first time and the article talked about how they did it and there are some very interesting
things one was um they
treat writing software as a 9-to-5 job 5
o'clock you have to go home you're not allowed to work all night you know none of these sort of hackathon like sessions
um those things are a lot of fun but they're not a way to get Reliable Software written so you come in in the
morning having gotten a good night's sleep and you work you're eight hours and then you go home
and you relax and you have a good night's sleep um and they said that was one of the most important elements of
their success at writing software that works um another one is and this is kind
of you know painful to think about nobody's allowed to write any code until
they have a detailed specification and I mean
detailed um practically every line in the software is is document the documentation ended
up being way way bigger than the software and they did all that first um
and whenever you make a change in the software you have to fill out a form in
which you say what page in the spec authorizes you
to make this change in the software um and somebody else reviews
that to make sure that you know your understanding is the same as theirs
um and then finally the the what I think is probably the most important piece is
that they built a climate in the company
of not blaming people people took responsibility as a
group and they worked very responsibly and they understood the importance of what they were doing but if something
went wrong the question they asked was not whose fault is this the question was
what went wrong with the process because the process had a lot of redundancy in it so nothing was supposed to get into
the code that hadn't been checked by several people you know and um you know vetted
with respect to the spec and all of that so if a bug gets discovered they want to
know how did that bug get past every piece of
the system and it's our responsibility collectively to improve the process and
that did happen they did find some bugs you know late in the debugging stage
before delivering the software and then they would go back and they would change the way they write software in response
to how did this bug come in so that's some of the background for um what you
have to do do to write software that works um so more
technically redundancy is one thing like that little mechanical widget limit switch um you can have redundancy in
software too you don't just check for something once every time it comes up you check to make sure that you're
looking at the kind of thing you think you're looking at um there's the notion
of failing softly uh that is to say we'd like the
software uh not to have any bugs at all that's our goal but let's say something
does go wrong um you know there's some huge static surge through the system and the
computer make some random wrong answer we want to ensure that if this system
fails it fails with the xray off not with the X-ray on so that's failing
softly um leave an audit Trail so
um this is a lesson that people have learned uh all the time your computer discs get full right you haven't done
anything you think well how can my dis be full I had space yesterday I don't today what's going on and what's going
on is that all of those dozens of little background procedures with
unpronouncable names in your system are writing records of every single thing that they do onto your disc
um and every so often you're supposed to go and delete the old records um and maybe the problem is that
like mine your computer is sleeping at 3: in the morning at the time when it was supposed to do the deleting uh so
your dis filled up um but that record is a just in case thing just in case
something goes wrong you can look at those records and ordinarily nobody ever looks at them because they're way too
much information but when something goes wrong then you do look at them so that's the idea of an audit Trail
um and this is this notion of software engineering which is the attitude of
saying um building software should be just like Building Bridges right that's what
software engineering is about
um I always have fights with people about the teaching of uh computer
programming to high school kids because people want to instill good
software engineering attitudes in kids and I say no don't do that um because then they won't want to be computer
programmers uh let them have fun and make mistakes and when we get when they get to College that's when we'll teach
them how to be software Engineers so here we are doing that
um so there are three stages at which you can solve problems the design stage
um um and then verifying you've written a program but you haven't run it yet and
then debugging so design um modularization so
one of the stories about what object-oriented programming is about I think I told you when we did oop that you're going to hear different stories
about this my story was about a metaphor about a simulation of something with multiple
agents um and this programming technique being well matched to that metaphor but
another story is about information hiding it's about um if each object has
its own local storage that's hidden and the other objects can't see it that
vastly limits the opportunity for one part of the program to step on something
that another part of the program cares about so um that's Mo
modularization um then next one is understanding concurrency so that stuff we did before about critical sections
and serializers and all of that um uh the goal of us doing it just as
briefly as we did is not that you're now ready to go into the world of work and
not make that kind of mistake but you're going to have more practice with it later and when you hit concurrency
issues in Upper division classes um you'll say oh yeah I remember that idea
from 61a so I know what a critical section is I know what problem we're trying to solve here
um and there's the notion of analyzing invariance here in my notes
um there's a homework problem we didn't make a big fuss about this but the um in
the section on Fast exponentiation the Theta of log n time exponentiation ation
algorithm and there was a homework question asking you to write it iteratively um and they gave a
hint saying that you have an extra input a to your helper function such that a *
B to the N is invariant right what they meant by that
was basically as um B and as b gets
bigger and or n gets smaller a shifts also so as to make it come out the same
next time through the loop as last time through the loop um so that's an invariant and you can design programs
around things like that you can say you can put assertions in your code that say
according to my understanding of the situation X+ Y is less than 27 here and
uh in your debugging you can actually have your program check you can make that assertion
executable so if X Plus y isn't 27 uh it
gives an error message um
okay so how do we verify that a program works you've written a program some
human being has written a program and handed it off to a computer we'd like the computer to help us certify that
this program is correct so the first thing you have to
understand is that that can't be done why
not yeah no it's not because programs are really complex have you done the halting
problem yet that homework exercise the wonder about suppose
there's a program that checks whether another program
halts okay yeah the checking program might be wrong
yeah that could be but it's worse than that it's theoretically impossible even if we do everything as best we possibly
can um if I hand you a program and it's input data and I say
I'd like you to write a program that will check whether this program finishes
never mind whether it gets the right answer just whether it eventually terminates for this input and your
program should always terminate right so it's easy to write a program that just sort of simulates the other program and
if that program terminates this one will too and if not not but we want a program that always comes up with an answer yes
or no does this program terminate on this input it can't be done it's no
computer ever will be able to do that um this was the first big interesting
result in theoretical computer science worked out by Alan Turing um the guy who
won World War II um he did he won World War II all by himself um by um decoding the German
Enigma Cipher so that the Allies knew what the bad guys were up to before they
did it um he also founded theoretical computer
science and one of the results is you can never ever prove that a program is
correct so when somebody comes up to you and says I've proven my program correct
you say oh yeah what about the halting theorem um but what you can
do is you can prove certain restricted
things about the correctness of certain classes of programs and there's been a lot of work done on program proofs um
and they have some very impressive results even though we know for sure that they're not
every possible bug found we can still find lots of bugs and certify that certain kinds of bugs are not present so
the the program proof people what they like to do is they'll write a program
Checker and then they'll take some big piece of public domain code like Firefox
is traditional um and they run their verifier their proof their program
checker on Firefox and sure enough they come up with 20,000 bugs and then they dig through the
Firefox bugzilla database and they say well uh okay uh 16,000 of the 20,000
somebody had already found but we have 4,000 new bugs that nobody had found before that our program found and that's
how you know you have a good program Checker um you'd think since people have
been doing this for like one or two decades that Firefox would be totally bug free by now but it isn't um not just
because of the halting theorem um the other thing that you can
do is in your compiler you can write your compiler to give warnings so sometimes you'll get a message saying
warning uh variable Fu initialized but never
used right or declared but never used um
and you know maybe that's just because you felt like it um or maybe you used to
have a use for it but you don't anymore but maybe it's because you mistyped what
was supposed to be the reference to that variable um so you get that kind of compiler
analysis that helps and then finally for debugging there's a lot of um
information that people have come up with about good debugging techniques debugging is still partly an
art um and also one of the best ways to debug your program is to have somebody
else debug it and the reason for that is you know what you
meant if what you wrote down in the program isn't what you meant you're very
likely to read what you meant instead of what you wrote so that's why it's good to get
somebody else to look at your code um but also we have this idea of blast blackbox and glass boox debugging so
given a procedure um one way to debug it is
without reading the code of the procedure just look at its input output
behavior that it's designed to have and try to figure out sort of corner
cases where the spec isn't quite clear about what should happen or you could
have thought of it this way or that way things like that or things at the very limits of um of the domain of your
program so that's blackbox debugging see how it does on cases that you think
ought to be hard and then there glass box debugging where you actually look at the code line by line and say let me
make a test case that exercises this line let me make a test case that exercises that line and so on um you're
supposed to do both of them you're supposed to do both blackbox and glass box debugging as the best way to catch
bugs um don't break the old code with a new fix um who's had that problem in their
project right something used to work and you broke something and I mean you fixed
something and then something else that you had already fix started not working again
um usually this comes from not understanding your program so that what you're doing is sticking Band-Aids on
things um but sometimes it's because of an unclarity in the specification of the
domain of the problem but anyway you should watch out for that by um anytime
you try out something in your program uh put that test case in a file
so that the next bug fix you do you can rerun all the tests that you've ever done right without having to reinvent
them to make sure you aren't Breaking All Things there's an interesting debugging technique in which introduce
bugs on purpose um so you just pick some random line in your program and make it do the
wrong thing and the point of that is to see whether the code Downstream from
there catches the problem so if this line is generating bad data do you get
the error message that you should get or does your program blow up divide by zero
or something um so that's called regression testing and the most important thing I'm
ever going to say to you so pay attention debug by subtraction not by
addition so if you have a bug that means it's because there's some code in your
program that's wrong and you need to find that wrong code and take it out as opposed to put
in some extra code that detects this case that isn't working and does a clui
workaround okay and the reason for that is after you found your first 10 bugs and put
Band-Aids over them you're going to find that you have Band-Aids on top of Band-Aids and um you can't understand
your own code believe me I've been there so it's a little bit like my advice to
you about midterm exams or final exams remember I said plan to spend more time reading than writing on the exam and you
said sit there and read the question and make sure you know what the question is asking it's just like that when you're
debugging a program and something isn't working in your program if necessary sit on your hands
to prevent yourself from changing the code of your program before you
understand why you have that bug okay and then remove whatever is
wrong um even if it's 4 in the morning and the project is doing an hour um okay
what didn't I say anything else any comments or
questions
yeah crappy code um oh boy um it's gotten better I have
to say the original answer to that question when they built windows on top of Doss is that the bottom most layer of
the system was just totally not built for concurrency and then they threw this
Cloe together on top of that and it it couldn't work with Windows NT they did a
complete rewrite and they got they hired a guy who actually knew how to write operating systems um and put them to
work and so the blue screen rate went down a lot at that point if I don't know if you go back that far but NT was way
way better than anything that came before um it does get better over time even at
Microsoft but there's one side of answers about
how especially evil Microsoft is and and it would be fun to talk about that but I
think it's more important to talk about the sense in which Microsoft is like anybody else who's trying to sell
something in the marketplace people don't go out and buy
the next version of your software because you say we fixed a th000
bugs that's not going to be good enough to get them into the store or clicking on the internet they buy the next
version of your software because it says you can have a desktop picture that
swirls around as you move your mouse right right that sells
software and so basically there's no incentive um for companies to fix bugs
and that's especially true if your company is a monopoly if your only competition is
yourself you know um then there's really no incentive for you to fix bugs it's
just coming up with something flash that'll impress people so that's basically why um so be a good consumer
of software and ask about how many bugs did you fix since the last
version question yeah
between software engineering and computer science
um well computer science is kind of a big
tent um part of what computer scientists do is properly called science that would
be the theoretical computer scientists who sort of figure out how systems work and how to analyze how systems work um
part of what we do is the engineering of software it's building software so
software engineering as a name is a kind of move there was a political movement
within the computer science Community to pay more attention to software reliability
um now they like programming languages that time went hand behind your back
because they think that's how to prevent bugs so you know there's a there's a much longer story than I can tell you in
a minute but um software engineering I would say is a piece of computer science
is that fair okay see you Monday
UC Berkeley 