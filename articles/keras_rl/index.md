<div class="content-wrap">

Keras play catch, a single file Reinforcement Learning example
==============================================================

Written by <span class="author">[Eder
Santana](mailto:edersantana@ufl.edu)</span>

</div>

<div id="content">

<div class="content-wrap">

Get started with reinforcement learning in less that 200 lines of code
with Keras (Theano or Tensorflow, it’s your choice).

<span class="more"></span>

![Keras play catch](/articles/keras_rl/catch.gif)

So you are a Machine (Supervised) Learning practitioner that was also
sold to the hype of making your labels weaker and to the possibility of
getting neural networks to play your favorite games. You want to do
Reinforcement Learning (<span class="caps">RL</span>). But you find it
hard to read all those full featured libraries just to get a feeling of
what is actually going on.

Here we got your back, we took the game engine complexities out of the
way and show a minimal Reinforcement Learning example with less than 200
lines of code. And yes, the example does use Keras, your favorite deep
learning library!

Before I give you a link to the code make sure you read Nervana’s blog
post [Demystifying Deep Reinforcement
Learning](http://www.nervanasys.com/demystifying-deep-reinforcement-learning/).
There you will learn about Q-learning, which is one of the many ways of
doing <span class="caps">RL</span>. Also, at this point you already know
that neural nets love mini-batches and there you will see what is
Experience Replay and how to use it to get you them batches. Even in
problems where an agent only sees one sample of the environment state at
a time.

So here is the [link for our
code](https://gist.github.com/EderSantana/c7222daa328f0e885093). In that
code Keras plays the catch game, where it should catch a single pixel
“fruit” using a tree pixels “basket”. The fruit falls one pixel per step
and the Keras network gets a reward of +1 if it catches the fruit and -1
otherwise. The networks see the entire [10x10 pixels
grid](https://gist.github.com/EderSantana/c7222daa328f0e885093#file-qlearn-py-L34-L40)
as input and outputs [three
values](https://gist.github.com/EderSantana/c7222daa328f0e885093#file-qlearn-py-L122),
each value corresponds to an action (move left, stay, move right). Since
these values represent the expected accumulated future reward, we just
go greedy and pick the [action corresponding to the largest
value](https://gist.github.com/EderSantana/c7222daa328f0e885093#file-qlearn-py-L147-L148).

One thing to note though, is that this network is not quite like you in
exotic restaurants, it doesn’t take the very same action exploiting what
it already knows all the times, once in a while we force system to take
a [random
action](https://gist.github.com/EderSantana/c7222daa328f0e885093#file-qlearn-py-L144-L145).
This would be the equivalent of you learning that life goes much beyond
just Penang Curry with fried Tempeh by trial and error.

In the link you will also find scripts that plays the game with no
random actions and generate the pictures for the animation above.

Enjoy!

<span class="caps">FAQ</span>
-----------------------------

**1) How does this Q-learning thing even work?**

C’mon read the blog post I just mentioned above… Anyways, think like
this. The fruit is almost hitting the ground and your model is just one
pixel away from a “catching” position. The model will face similar cases
many many times. If it decides to stay or move left, it will be punished
(imagine a bunch of rotten fruits smelling in the ground because it was
lazy). Thus, it learns to assign a small Q-value (sounds much better
than just “output of neural net”, han?) to those two actions whenever it
sees that picture as input. But, since catching the fruit also gives a
juicy +1 reward, the model will learn to assign a larger Q-value to the
“move left” action in that case. This is what minimizing the [reward -
Q-valu
error](https://gist.github.com/EderSantana/c7222daa328f0e885093#file-qlearn-py-L98-L106) does.

One step before that, there will be no reward in the next step.

I liked how the previous phrase sounded, so I decided to give it its own
paragraph. But, although in that case there is no juicy reward right
after, the model can be trained using the maximum Q-value of the future
state in the next step. Think about it. If you’re in the kitchen you
know that you can just open the fridge to get food. But now you’re in
your bedroom writing bad jokes and feel hungry. But you have this vague
memory that going to the kitchen could help with that. You just go to
the kitchen and there you figure how to help yourself. You have to learn
all that by living the game. I know, being Markovian is hard! But then
the rest is just propagating these reward expectations further and
further into the past, assigning high values for good choices and low
values for bad choices (don’t forget that sometimes you hit those random
choices in college so you learn the parts of life they don’t talk about
in school). For everything else, if you believe in Stochastic Gradient
Descent than it is easy to see this actually making sense… I hope…

**2) How different is that from AlphaGo?**

Not much… But instead of learning Q-values, AlphaGo thought it was
smarter to use <span class="caps">REINFORCE</span> and learn to output
actions probabilities directly. After that, she played several games
against itself, so many that it could later learn the probability of
winning from each position. Using all that information, during play time
she uses a search technique to look for possible actions that would take
her to positions with higher probability of winning. But she told me to
mention here that she doesn’t search as many possibilities in the future
as her older cousin DeepBlue did. She also said that she can play pretty
well using just one GPU, the other 99 were running high resolution
Netflix series so she can catch up with human culture.

That being said, you should be able to modify this script in 2 or 3 days
to get a reimplementation or AlphaGo and SkyNet should be 4 weeks away?

<span class="caps">JK</span>

**3) Your code sucks why don’t you write something better?**

[I’m trying…](https://github.com/EderSantana/X/blob/master/examples/catcher.py)

**4) Did you learn that by yourself?**

The bad parts, yes. The good things were thought me by my friends Evan
Kriminger and Matthew Emigh.

</div>

</div>

<div class="content-wrap">

<div class="nav">

[« Full blog](/)

</div>

These are personal words. Here you may find references to unconventional
ideas. Please, read it at your own risk or don’t read it at all. If you
are looking for my conventional science publications, please visit [this
website](http://cnel.ufl.edu/people/people.php?name=eder).

© 2016 Eder Santana — powered
by [Wintersmith](https://github.com/jnordberg/wintersmith)

</div>
