---
layout: post
title: "Destructively Constructive: Compulsively Debugging My Way to and from Insanity"
comments: true
date: 2019-05-20
---

<!-- BODY -->
So a set of students in my lab are currently working on a deep learning model, and given the software climate that means that they are also starting to learn python. I started showing them a small model I built, much less complicated than their own model, so I could give them a fresh example to analyze and compare against their own plans.

## Wow, so organized...
Quickly this devolved into a conversation about the structure of my own code. Given my gross disorganization and lack of ability to stay on topic or focused in my personal life, their reaction to my code was a bit surprising. I hadn't really thought of myself as being particularly organized or savvy.

Fuck that, of course I did. I just thought it was nice that other people thought so.

Still, it's very true that in most other ventures I'm fairly disorganized disheveled, and messy (despite my delightfully debonaire appearance). This got me thinking about *WHY* exactly I put so much effort into organizing my code, and looking up new frameworks in python when I have no real external motivation to do so. There are three major answers:
1. When I have a bug I call even my whole existence into question
2. Learning new frameworks lets me kill time while looking like I'm still moving my project forward
3. Marketing

That last point requires a little more explanation.

Everyone out there, be it those who are making or those who are using software, will pitch it as the next best framework for keeping themselves organized or for being some drastic improvement to their productivity, life, gut health, etc. But seriously, you will not have trouble finding reviews about even the most mundane tools out there, and when you meet the people reviewing these tools in person, you might even start to agree with them that you were not truly living before you used the `click` module for making a nice CLI.

To be honest, it's really more of points 1 and 2 that heighten my coding compulsions.

## Debugging my anxiety
Something I've come to accept over the past few years is that the more mistakes I make, the more I'll make mistakes that I won't learn from. Let's unpack that: I like to make sure that whenever I write something I assume that everything is going to fail, and that when I am even slightly confused, that's the point in my code I'm going to go back to in 2 weeks after I've already ran it, analyzed the results, and reported it to my PI.

The main reason I like to use nice frameworks, make every action into a modular unit that I can move around in any which way and test individually, is that I know at some point I will fuck up. When that happens, I'll be able to tear my pretty little script to shreds and change it up completely within a few minutes. Plus it always calms me down to know that I can read and understand what I've written ages ago, and even re-use it in a new program if need be.

## Show me some code, homeboy
Alright at this point I've talked a big game. Prepared to be underwhelmed by my coding practices for the next 5-10 minutes as I tell you how I organize my work into:
* Main scripts with points of entry
* Utilities
* Side experiments
* Testing functions (at least for code that's really complicated)

### Main scripts with `click`
Since my last hackathon I've been using [`click`](https://click.palletsprojects.com/en/7.x/) to manage changing arguments to the same general program.

With `click`, you can just add command-line arguments to a function using their decorators:

`main.py`
```python
import click
@click.command()
@click.option(
    "--arg1",
    default=2,
    type=int,
    help="A dumb argument")
@click.option(
    "--fun-arg1",
    default="cheese",
    type=click.Choice(["crackers","cheese"]),
    help="A nice snack")
def main(**opts):
    for (arg,value) in opts.items():
        print("{} is set to {}".format(arg,value))

if __name__ == '__main__':
    main()
```

In the main script of my little commandline program, I'll put in a skeleton like this to start. I like using `click` this way since it passes in everything as a nice set of key-word arguments that I can neatly store in a dictionary `opts`. This way I can add flags or changes without a whole bunch of new logic: if I don't want something to run or I want to add something new, just add another argument, add in a flag or something to skip based on that argument, and then call my program with the new feature. I can change my code without changing it in multiple places, and I get a nicely formatted help message out of it too:
```
william@comptastic:~/Documents$ python main.py --help
Usage: test.py [OPTIONS]

Options:
  --arg1 INTEGER                A dumb argument
  --fun-arg1 [crackers|cheese]  A nice snack
  --help                        Show this message and exit.

```
### Utilities
This is actually a way I organize my code that could be better, but at least it's something to start with when I'm just starting a project and I have no idea how complex it will be. It's actually pretty boring, basically just a bunch of functions with docstrings:

`utilities.py`
```python
def doStuff(a,b):
    """
    Add two numbers

    Args:
        a (int): The first number
        b (int): The second number

    Returns:
        int: The return statement, the sum of a and b
    """
    return a+b
```
#### Docstrings???
I guess the interesting thing here is that a lot of different tools recognize these docstrings, python itself will store them in the `.__doc__` attribute of functions and if someone calls `help` on the function there will actually be help there if you define docstrings.

`doctest`, which I don't personally use for testing, ships with modern python versions and lets you literally copy tests you run in the python REPL and paste them, with their results, into the docstring. You can then actually run all these docstring tests.

I choose this format because I find it fairly clear, it's based off of the [google-style docstrings](https://www.sphinx-doc.org/en/1.5/ext/example_google.html) that are recognized by [`sphinx`](https://www.sphinx-doc.org/en/1.5/index.html), which is a nice tool for generating documentation from your code (although since I'm by no means generating large-scale software at this point, I've never actually built documentation using the tool).


#### Why I'm doing it this way
But other than docstrings, most of my workflow is just grouping like-functions together and then importing them into my main program:

```python
import utilities


def main():
    return utilities.doStuff(1,5)


if __name__ == '__main__':
    main()
```
This let's me keep all of the nitty-gritty stuff away from what I'm doing at a high level, so I don't get fucked later. Nice.

If I have to make an involved routine somewhere I'll make a file for side experiments too.

## Side experiments
Basically just [Utilities](utilities), except this time with a purpose. I might add a module-level docstring at the top of the file so I can tell myself what super involved thing I'm trying to get done there.

Sometimes side experiments will be just that: experiments. Things don't always go well, and I don't, and have learned that I definitely shouldn't, trust that I knew what I was doing on a first pass. As a result, my projects tend to have a bunch of files that look like [main](main scripts with `click`) files but instead of running some complicated pipeline, they run a simulation related to the project, or test out if I understand some theory (you may very well see the results of that *ON THIS VERY BLOG!*).

The peak of my neuroticism and self-doubt when it comes to coding has to probably be unit-testing, which to be honest I've only recently started doing seriously.

## Testing with python's `unittest`
I doubt I'm (/I know that I'm not) the first person to ever have blogged about unit testing, or even using unittest. So I'm not going to spend too much time here. Basically If I've hacked away at something for long enough, and I still don't trust that my code is doing what I want it to, I turn to unit tests.

Thankfully, other than my unwieldy and complicated main routine, most of the work I've done up to this point is broken up into nice neat, individually testable (hopefully little) functions. This lets me define ~~one big file full of~~ several files with test suites using python's [`unittest`](https://docs.python.org/3.6/library/unittest.html) module.

There's already a lot about the specifics of `unittest` in the documentation linked in the last paragraph, but here's a nice example of/skeleton showing how I use it:

`tests.py`
```python
import unittest
class TestingSuite(unittest.TestCase):
    def setUp(self):
        """This will be called before running any of the tests in this class"""
        pass


    def tearDown(self):
        """This is called after running any of the tests in this class"""
        pass


    def test1(self):
        """tests for one function in this category"""
        self.assertEqual(1,1)


if __name__ == '__main__':
    # here I can define how I want to run the tests above using a
    # unittest.TestSuite() class, or I can run them all with:
    unittest.main()
```

You can run al lthe tests per class really easily from the commandline using the `-m unittest` flag when running the file:
```
(tf_vae) william@comptastic:~/Documents$ python -m unittest tests.py
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

## In summation...
Basically I use a bunch of basic tools that other people use to keep on top of their code and stay organized. Hope that the little insight into my \#basic ways will help you get started or at least get you thinking about something you didn't think to think about before I told you to think that thought.

<h1><center><span style="color:magenta">#ThinkThatThought</span></center></h1>

...and thanks for reading,

William

[^1]: Courtesy of [css-tricks](https://css-tricks.com/snippets/svg/curved-text-along-path/)
