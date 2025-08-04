n Monday, I think I said an amazing new idea every week and the amazing new idea for this week is the one about procedure as data.
And since you just got introduced to that idea, it's possible that you don't get right away what an amazing idea it is.
Let me tell you that you could build a programming language consisting of lambda, the thing for generating procedures and the ability to call procedures and nothing else.
And that language will be universal in the sense that anything that any computer language can do, that language can do.
You don't have to have, for example, arithmetic built in. You can make that out of just lambda and procedure calls. You don't have to have any special forms except lambda.
In particular, I think this week's extra for experts is about figuring out how to do without define and still be able to write recursive procedures.
How do you make a recursive procedure without being able to give it a name with define just with lambda? That's the extra for experts this week.
So it really is a very, very powerful idea and what we used it for as in this keep example is generalizing patterns of control.
So lots and lots of times you have a problem in what you want to do some kind of filtering of data.
I have a collection of data and I want to keep all the ones for which such and such is true and discard all the ones for which such and such is false.
And that pattern is captured by this keep procedure.
All of the control mechanisms that you typically get in programming languages like for loops and while loops and all of those things, you can build using procedures as data because a procedure is a representation in the computer of an action.
So if you think about the language you learned in high school, you're saying for i equals 1 to 10 do this.
The do this is a procedure or can be represented as a procedure.
So we can have a four procedure that takes a start value and an end value and lambda of i do such and such and creates that control mechanism.
So any mechanism that you want for specifying the flow of control, sort of the sequence of events, what's going on inside the computer can be made out of procedures as data.
In this keep example, one way to look at it is as a specification of the sequence of events, but a better way to look at it is to forget about the sequence of events in the computer and just think about the problem you're solving as being solved all at once.
So I have a collection of data, I want to restrict it to things that satisfy this condition, boom, keep does that for me.
So you don't have to think about does this element satisfy the condition, okay, does this element satisfy the condition.
You can imagine that happening all in parallel and in some systems, in the not very far distant future, it might all happen in parallel.
You might have a list of a thousand things and you might have a thousand processors in that box on your desk and each processor might be looking at a different element of your data deciding whether to keep it or discard it from the result.
So that's the power of having procedures as data.
I wanted to generalize this notion about what should be data in the language by talking about the idea that's up on the chalkboard there about first class data types.
The data type is first class in a language if things of that type can be the value of a variable.
So can I say define such and such to be that kind of thing? Can I do that for procedures? Yeah, I can say define square to be lambda x times xx.
Okay, so in this expression I am defining the variable square to have as its value a procedure.
In fact this happens so often that as you know there's an abbreviation for it where you'd say define parenthesis square of x and what that abbreviates is assigning a procedure to a variable.
A procedure can be the argument to a procedure for any first class data type can be an argument to a procedure.
So as we've seen in the keep example we can use a predicate function as an argument to keep.
A procedure can be the value returned by a procedure. I haven't shown you that yet but I'm about to.
First class data type can be a member of an aggregate. An aggregate is something like an array where you take a bunch of different elements and you make one thing out of them.
So far the only aggregate data type that we have is sentences and a procedure can't be a word in a sentence but next chapter we're going to see the more general mechanism of lists and you can have procedures be elements of lists.
There are procedures of first class in that way too and something that isn't in my lecture notes but is sometimes included in the definition is kind of the opposite of can be the value of a variable namely can be anonymous.
So I have a procedure that doesn't have a name so I can say you know lambda x word x x of quote foo and get foo foo.
So I made this procedure that combines the word with itself. I didn't give it a name and I could just call it.
In every language numbers are first class.
Can you use lambda to define a procedure with more than two arguments? Yeah. The reason that this x right here is in parentheses this one is that it could be x y z or x y z w or whatever names you want and how many however many you want.
Sorry the question was can you use lambda to make a procedure with more than two arguments so yeah you can't.
So numbers are always first class. Character strings are first class in some languages but not all. Notably not in C.
Data aggregates are rarely first class. Instead some languages give you a data type that's called a pointer to an aggregate and those are first class but it's subtly different from having the actual aggregate being first class.
And hardly any language gives you procedures as first class data although I'm pleased to say that that's changing. So Python up and coming language of the future has lambda Java to the standard right now application programming language in the world.
It doesn't have lambda but it has something called anonymous classes which you can use kind of as if it were lambda by standing on your head so it's in elegant but it's there.
So the same people who kind of poo poo the list family of languages as being ivory towerish are starting to adopt the key central idea of list namely lambda in you know languages out in the world because it's so very useful people are starting to catch on to that.
In scheme one of the design principles and one of the things I'd like you to get out of this course at the by the time we're finished is a better idea of why is there more than one programming language.
So what makes people come up with different languages in different situations and different languages have different design principles and one of the design principles of scheme is everything first class if it's in the language at all it should be manipulable in all those ways.
The scheme does pretty well at that will actually meet one exception down the road but again that that's not the design principle that many other languages use many other languages use the principle of everything should be very efficiently compilable.
That's not a terrible idea for language you know understand that some languages use the principle that everything should look natural.
I would argue with that one a little bit because people's idea of natural is so determined by programming languages of the past that it's a way of saying let's not have any progress programming languages.
Different design principles for different purposes we're going to play later in the semester with logo is a programming language designed for children and we're going to look at how that fact led to logo looking very different from scheme even though they're both sort of cousins in the list family.
Moving on I promised to show you how a procedure can be returned by a procedure so here's the classic first example of that I'm going to say define make adder of numbs notice there's an implicit lambda in here I'm saying define make adder to be a procedure that has num as a formal parameter.
And now the body of this procedure is going to be a lambda expression.
So make adder says take a numbers argument the domain of make adder is numbers and return a procedure the range of make adder is procedures the return procedure takes another numbers and argument and adds num to it.
So now I can say define plus three notice no parentheses around plus three so there's no implicit lambda here I'm going to say make adder three.
Now what's plus three do well if I say plus three eight 11.
Define plus five make adder five plus five plus five of seven plus five of plus three of two.
Okay so plus five and plus three let me make the screen bigger so you can see all that so plus five and plus three are procedures by virtue of the fact that when I called make adder in the process of defining them make adder return to procedure.
I turned one procedure for the call make adder three and a different procedure for the call make adder five.
So I don't have to give it an aim I can say this would be kind of silly I don't know why you would do this except just to show you that I can make adder nine of seven.
I didn't have to say okay call this plus nine I could just take the procedure that adds nine to its argument apply that to seven I get 16.
So this is the first simple example of a procedure that returns a procedure.
So I'm going to show you one of my very favorite procedures in the whole world.
It's this one define compose f and g. So you remember what composition of functions is from algebra class right.
The composition of f and g is the function that maps x to f of g of x.
So I'm going to say that in scheme language the function that maps x into f of g of x.
So compose first with bud first.
So compose works entirely in the space of functions it's two arguments or functions it's returned value as a function.
So I can say since compose first but first gives me the second word of a sentence I can say define second to be compose first but first.
So define twice of f to be compose f f.
So I can say did I define square I think so twice square of three what am I going to get 81 I'm getting the square of the square of three.
So twice square is something that takes its argument to the fourth power.
So this is really really cool this gives a very concise notation for building up more complicated functions as compositions of other functions without ever having to talk about the actual domain and range of the functions being composed.
So there's no x when I say compose first but first.
It really doesn't tell you what the domain of first and but first is now in order for it to work of course it has to be that the domain of of f includes the range of g.
Otherwise it doesn't make sense to compose them right.
But you can try and you'll get some kind of error message when you actually run it.
So it's not that you can completely not think about domain and range but you don't have to have those little variables like x floating around.
You can just say second is the composition of first and but first dot really nice.
Anybody ever programmed in Pascal?
A couple of people. Too bad.
Pascal is a pretty useless language but it's interesting to talk about for our purposes here because in Pascal.
You can use a function as an argument to a function but you can't have a function as the return value for a function.
That seems like a pretty arbitrary restriction and it is.
And the reason for it is we're going to see a little bit in this course and you'll see in detail in 61c why it's relatively easy to allow functions as arguments and relatively hard for a compiler to allow functions as return values.
So it was just sort of an efficiency decision that they made.
All right.
Let's see that.
Yeah.
Are compiled scheme programs big? Is that what you're asking?
Oh, I see.
Yeah.
The source code in that scheme program will be smaller than in another language.
There.
Yes. And there are a lot of reasons for it.
This thing that we're talking about is just one of them. Probably the most important differences that we don't declare types of variables.
Later on we'll be talking about that in a week or so.
Two weeks, I guess.
Talking about some of the ways in which this language difference from other ones that make programs easier to write.
It matters because to a first approximation.
Oh, he wanted to know about sort of differences between in size between scheme programs or scheme data and other languages.
And I'm making the claim that you can write shorter programs and scheme that do the same thing.
And it matters because to a first approximation.
The number of debug lines of code.
Produced by a programmer in a day.
Is language independent.
You can be using a very tourist language or a very spread out language and you'll still get.
And it's a shockingly small number like two or three.
And that's because of the word debug.
You can write 100 lines of code a day that don't work.
But once you get it working, it averages out to a pretty small number.
So therefore, the more you can fit in a line of code, the better in terms of getting the job done quickly.
And that's why one of the ways that list family languages have been used industrially is as rapid prototyping languages.
So you want to write a program.
You have a customer that you're writing it for.
The customer gave you a spec, but of course, customers never know what they really want.
So you implement what the customer asked for and the customer says, no, no.
I don't want that. I want this other thing.
And you go through four or five iterations of that.
Before the customer finally gets around to everything's perfect except it runs too slowly.
So those first five iterations are best done in a language that lets you write throw away code quickly.
So sometimes people will write the first five versions and list.
And then when they get to, oh, it runs too slow, write it in C or something.
Try to optimize it from a time standpoint.
Okay. Let's move on.
What's up on the screen here is a procedure for, I'm sorry, the world's most boring problem.
I picked it because it's a question that has two answers, namely the roots of a quadratic equation.
So if I want the roots of x squared minus five x plus six equals zero,
I'll say roots of one x squared minus five x plus six.
And what I get back is a sentence with the values three and two.
Because those are the roots of that equation.
I picked one that would come out nicely.
So since a function can only return one value,
I can't return the three and then separately later somehow return the two.
What I have to do is make a sentence right here that combines the two values.
So what are the two values? You remember that from my school?
It's minus B plus the square root of B squared minus four AC over two A.
And minus B minus the square root of B squared minus four AC over two A.
So the only difference is this plus sign versus this minus sign.
So that's a lot of redundant typing.
And it's also a lot of redundant computation because it takes a non-zero amount of time to compute a square root.
So it would be nice if we could just compute the square root once.
So what we want to do is compute square root of B squared minus four AC and give that a name.
I can do that this way.
So I'm doing roots ABC.
And I have this helper function, an internal definition, roots one,
that has a formal parameter D. It's not just because it's the fourth letter of the alphabet.
The D stands for discriminant, which, if you remember back as far as high school,
is what they call this square root of B squared minus four AC.
And then I call roots one with square root of B squared minus four AC as the actual argument expression.
And then inside roots one, I say minus B plus D over two A and minus B minus D over two A and combine those into a sentence.
Questions about how that works?
Yeah, he's saying it's only, it calculates it once rather than twice.
Only because scheme uses a flickative order. That's right.
If it were normal order, we would end up calculating it twice.
Although we'll see later in the semester there's a fix for that.
But yeah, but luckily scheme does use a flickative order.
So this solves the computing at twice problem.
But it does so at the cost of having to define this helper roots one,
which I'm never going to use for anything else.
And also separating the name D up here from its value down here.
So it's a little hard to read.
So I'm going to solve those problems one at a time.
I'm going to solve the first problem by making it even a little harder to read, actually.
But instead of saying define roots one, I'm just going to have an anonymous lambda expression.
This is the same thing that was the body of roots one.
Let me see if I can get them both on the screen at the same time.
No, I can't.
I guess I can.
So here was the definition of roots one.
And now down here is the lambda expression starting with this second open parenthesis.
That's the same function as roots one.
And then I call it, that's this open parenthesis in white on black here,
with square root of b squared minus 4ac as its actual argument expression.
So there's no more name roots one.
It's an anonymous function.
But even though it's elegant in a certain sense, it's really ugly to read.
So we have an abbreviation.
What we're going to do is exactly this in the meaning of what we're doing.
But we're going to rearrange this to put this D, whoops, this D right here.
And this square root of b squared minus 4ac next to each other.
The abbreviation is called let.
So this is what a let looks like.
And it is let.
Here we go.
Binding's body.
The body is just like the body of a procedure.
It's an expression that we're going to evaluate that will give us the value of the whole let expression.
What's bindings?
Well, bindings is open parenthesis.
And then a binding.
And then optionally another binding.
As many as you want.
And then close parenthesis.
Well, what's a binding?
A binding is open parent, name, and then value expression.
Okay?
So when we put all that together, we're going to see this is the other case besides con where we have funny parentheses that don't mean call a procedure.
This one does mean call a procedure.
Namely, this is a call to the square root procedure from here to here.
Okay, those are plain old function call parentheses.
This one right here, having trouble just picking up one character.
But this open parent is the start of a binding.
And that binding extends all the way to here.
Okay?
So that's one binding.
And then outside that are the two, is the pair of parentheses that encloses the whole set of bindings.
In this case, it's a set of length one.
It's not a procedure call.
We're not calling a procedure named D here, for example.
Okay?
So the parentheses has a different meaning.
I mean, yeah, we're taking an action because of it.
So we're not calling a procedure.
Yeah.
Good question.
Can the bindings be dependent on each other?
So let's look at a case, actually, with multiple bindings.
So while I'm making this let, besides having D, I'm going to have a variable called minus B.
Whose value is the negative of B, and a variable called 2A, whose value is A times 2.
And then the body can just use all of those variables to make a very, very short expression.
So he wants to know, if I've defined D to be the square root of B squared minus 4 Ac,
can I use D in defining the next variable?
What do you think?
Who thinks yes?
Who thinks no?
You guys have seen lead before.
Or you're smart.
One or the other.
The answer is no.
And here's why.
I'm saying let D be this minus B be that, and 2A be that, and then the body.
Now I'm going to unabriviate that.
I'm going to show you what it looks like using a lambda.
In fact, I'm going to do it in two colors.
So I'm going to start by saying lambda of D minus B and 2A.
These are not really valid scheme symbol names, but SDK is a little forgiving about symbol names.
Lambda of that, and then the body of the lambda is sentence with plus and minus.
So that's the anonymous function that is hidden inside the lat.
And what I do with that function is I call it with the arguments square root of such and such,
and then the negative of B, and then times 2A.
So whoever asks the question, do you see that what I have is a procedure call as the outer expression that's calling a procedure that I just sort of custom built.
So when I compute this expression here, the one where I have minus B, if there were a D here instead of B,
does D have a value when I'm computing this expression?
Who says yes? He says no.
Okay, somebody who says no, why not?
Two words.
In scheme, doesn't by the way most programming languages, all of these expressions get evaluated.
All four, the lambda expression, the square root expression, the minus expression, and the times expression.
All of them get evaluated before we call this procedure.
But it's only inside this yellow procedure that these variables have any meaning.
Out here, there is no D. There's no minus B, there's no 2A. Those variables exist only in here.
So we can't use this value in computing this value.
It is a useful thing to want to do. Use this value in computing that value.
And so it turns out we don't really make a lot of use of it in this class.
But if you're interested, there's a thing called let star, the terrible name.
So A, three, B, plus A, five.
Okay, that's good enough.
So this is like a let. It's the same format of bindings, binding, name value.
Here I'm using this name in computing this value.
And the reason I get to do that in let star is that let star is actually translated to let one binding A, three.
And then the body of that let is let B, whatever I said, plus A, five, and then times A, B.
So it nests however many lets are necessary.
So since this second let is part of the body of the first let, the variable A does exist here.
So we can use it in giving a value to B. So that's let star.
Yeah.
Yeah, he's asking what if I wanted to do a let star using lambda instead of let.
And yeah, I would turn this using the same idea I did here.
And then this into a procedure call of an anonymous procedure.
And the body of that anonymous procedure would be a procedure call of an anonymous procedure.
There'd be a lambda inside an invocation inside a lambda inside an invocation.
You have a question?
Can you make a recursive procedure inside a let?
Very good question. I'm proud of you for recognizing that it's a problem.
The reason it's a problem for people who aren't up to speed on this is,
in order to make a recursive procedure, it needs access to its own name.
So if I say let foo be lambda of such and such, in that lambda, because that lambda is out here,
the one that's providing the value for foo, there's no binding for foo.
So I can't call foo inside itself.
And so no, you can't use let to make recursive functions.
There's yet another variant of let that's called let rec, L-E-T-R-E-C,
stands for let recursive.
And what it's an abbreviation for is so complicated that in the first four versions
of the scheme reference manual, they got it wrong.
The v wizards of scheme didn't quite get it right.
But it is right now, you can look it up if you want to.
So where are we?
So what are the things that you have to understand about let other than just what the notation is?
One is this is not like assignment statements in that programming language you learned in high school,
because we're not making permanent bindings.
It's not like saying, you know, x equals 5.
The variables, the let variables, the d and the minus b and the 2a,
are only usable inside the body of the let.
We go on to do something else after the let, they're not there anymore.
Because there are arguments to this procedure, the actual values got substituted into this body right here,
but they didn't get substituted into anything else.
So don't think of it as being like assignment statements you grew up with.
It just has a limited range.
Secondly is the thing that you can't use one value to define the next,
unless you use let star or nested lets.
There will come a time when you actually see that as useful,
when you'll be glad that the let bindings aren't in effect while you're computing the values.
Because you'll have some recursion or something and you'll want to use old values of all three variables
in computing the new value of all three variables.
So sometimes let really is what you want, sometimes let stars what you want,
and sometimes even let records what you want.
Okay, question.
Wow, everybody understand?
I'm not asking questions because I get everything.
I'm not asking questions.
And so lost, I don't know what to ask or somewhere in between.
A lot of thumbs down, okay.
Where'd you get lost at let or at first class data?
Okay, remember the substitution model evaluation?
He's asking about sort of the binding mechanism in the lat.
Remember the substitution model and remember what it is that let abbreviate.
So we compute these things are actual argument expressions.
They're all found next to each other kind of up here along with the values that are along with the formal parameters that they go with.
So it's a matching up a formal parameter with actual argument expression.
So what does scheme do?
First thing it does is it computes the value of all the sub expressions.
So we have an actual argument expression that's square root of b squared minus 4ac.
And we compute that expression and we get 27 or whatever we get, okay.
And we do that for all of the argument expressions.
Then we substitute those values for the formal parameters in the body.
So wherever there's a d in here, we're going to put 27.
And wherever there's a minus b, we're going to put whatever the negative of b is and so on, okay.
So now what we have is this expression only it doesn't have any variables in it anymore except for the global variables that are names of primitives like sentence and slash and plus and minus.
And then we just devaluate that expression which is full of arithmetic functions and numbers and nothing else.
Why do I need let's start to think from let, is that what you're asking?
I substitute them into the body, yeah.
Oh, if I say let a three, I'm not sure I'm answering your question.
Let me know. If I say let a three, we're going to substitute, well, first of all, we compute this expression.
It happens to be a very simple expression, so value is three, okay.
Now every place there's an a, namely here and here, I substitute three.
So now what I'm left with is this inner let, which is the body of the outer let.
So I'm going to evaluate that.
This now says let be the plus three five.
It doesn't say any more.
So plus three five, that's eight.
So I'm going to substitute eight for B in the body of the inner let.
So I get times three eight.
Okay.
Maybe I, if that, that yes sounded like I haven't answered your question yet.
Okay. Sure. Are there questions? Yes.
The difference between using, okay.
Okay. So let.
So the way I did.
Oh, if I had just said define D to be square root of B square minus four, I say.
Yeah. I could have done that too as internal definitions, and that would work.
No.
Internal definitions are complicated to understand.
When we get to chapter four, you will learn that internal definitions aren't really definitions at all.
They are an abbreviation for a let rack.
So it really all comes down to the same mechanism.
Global definitions, things that you type at the scheme prompt.
Those are permanent. They leave stuff around.
Global variables are generally frowned upon in the programming world.
Because that's how you get in this situation where a change in one part of the program ends up affecting another part of the program that you weren't thinking about.
So you want to keep all your variables local.
And this is a way to do that.
So when you're the formal parameter of a procedure exists only inside the body of that procedure.
And whatever notation you use ends up coming down to the same thing.
Okay. But yeah, you could do it with internal defines.
Okay. Yes.
Does let need a body? Yes, there is a body.
In this bottom left, this part is the bindings part.
Yes, the body of the lead inside the lead is times AB.
And yes, lead has to have a body.
And let's start as the order of the bindings matter.
Yes. Because you can use A in coming up with the value of V but not B in coming up with the value of A.
And that's clear if you think about what it expands into.
One of these leads is inside the other.
Yeah.
Sorry.
If you use lead instead of lead star then this expression plus A5 won't use this binding for A.
Instead, either it'll use some global value of A or it'll give you an unbound variable error message.
You guys, don't obsess too much over lead.
You can, you know, go read all this stuff in the book and get to understand it.
And you should understand it.
But lead is just one particular case of the general idea here.
And I'd like to bring lead back into that general idea, which is the ability to use procedures as data.
Let's us build any control mechanism we want.
Okay. So keep was an example of that.
Every which you're writing for homework is an example of that.
I talked about how you could write four as an example of that.
And let itself is also an example of the same thing.
That having procedures as a data type in the language lets us make any old kind of thing we want.
You guys, I'm sorry, I hate to be, what's the word I want?
Tendentious.
But you're being really rude and it does kind of make me feel jittery.
So please wait until the class is over before you pick up your stuff.
We are almost over.
That's quite yet.
If there's another question, I'll answer it.
Yes.
Yeah, explain again why I can't use recursion with the lead.
So it's really the same thing as why in a regular lead, we couldn't use this a to define b.
Do you understand that part?
Because these expressions out here are evaluated before we have bindings for that.
Suppose one of these is a lambda expression.
So I'd like to define a factorial function.
I'm going to say let fact be lambda vn and then if blah blah blah.
And in here some place it'll be fact of n minus 1.
And then I'll say, you know, fact of 5.
Well, this is not in the body of the lead.
The body of the lead is just fact of 5.
So this whole lambda expression does provide a value for this fact here, but not for this one.
Because this gets evaluated before I've made this binding.
So it's really the same as the a and b problem except it's a and a.
Okay?
It's a good question.
All right.
See you next time.
Oh, next time.
Sorry.
The next two lectures are a videotape presentation by Alan Kay about user interface design.
Don't decide not to bother coming because it's a videotape.
They're the best two lectures in the course.
All right.