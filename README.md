# Introduction to Object Orientation

## Objectives

1. Understand programming paradigms as a form of human abstraction.
2. Learn the distinguishing characteristics of Object Oriented Programming (OOP).
3. Define the terms "methods" and "properties" in the context of OOP.
4. Use dot notation to access an object's properties.
5. Chain dot notation to access a property of a property.

## Programming Paradigms and Languages

*An object-oriented approach to application development makes programs more intuitive to design, faster to develop, more amenable to modification, and easier to understand.*  
—[*Object-Oriented Programming with Objective-C*][apple_oop_guide_intro], Apple Inc.

[apple_oop_guide_intro]: https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/OOP_ObjC/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005149-CH1-SW2

Object-oriented programming (OOP) is a "[programming paradigm](https://en.wikipedia.org/wiki/Programming_paradigm)"—meaning that it is an *approach* to writing code. There exists a variety of paradigms in the software industry which overlap with or build on top of other paradigms, such as the procedural, structured, and functional programming paradigms.

Programming *languages* are said to follow or "fit into" programming paradigms. Some languages follow a single paradigm rather strictly, such as Objective-C with object-orientation, but a number of languages can be classified as "[multi-paradigm](https://en.wikipedia.org/wiki/Comparison_of_multi-paradigm_programming_languages)", meaning, as you would expect, that they contain primary elements of more than one paradigm. Such is the case with Ruby and Python which both qualify as object-oriented languages but which also heavily rely on functional programming techniques as well.

### Levels of Abstraction

All of these "high-level" programming languages are forms of human abstraction. The terminology of "high-level" versus "low-level" languages are relative terms used to express how far removed that language is from the CPU's understanding of it. The lowest level of programming is [machine language](https://en.wikipedia.org/wiki/Machine_code) (also "machine code") which is essentially some defined way of interpreting actual binary (ones and zeroes). CPUs can only execute (i.e. run) code that's been translated into the binary that it can understand.

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/machine_code.jpeg)  
—Machine language is scary. *Machine language monitor in a W65C816S single-board computer, displaying code disassembly, as well as processor register and memory dumps.* [Wikimedia Commons](https://en.wikipedia.org/wiki/Machine_code#/media/File:W65C816S_Machine_Code_Monitor.jpeg)

The trouble with programming in machine language is that it's nigh-unreadable to humans. So, [assembler languages](https://en.wikipedia.org/wiki/Assembly_language) (also "assembly") were developed to make programming a little easier to understand. Assembler languages are still closely related to CPUs and translate pretty readily in machine code. If the machine that you're reading this on has an Intel or AMD CPU, it almost certainly runs on some version of [x86-64 assembler](https://en.wikipedia.org/wiki/X86-64). 

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/assembly_language.png)  
—Assembly language is still pretty scary. *Motorola MC6800 Assembly listing, showing original assembly language and the assembled form* [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Motorola_6800_Assembly_Language.png)

However, assembler is still pretty technical, requiring micro-management instructions for every single operation. So "high-level" or "third-level" languages were developed to bring increased readability via increased abstraction. Third-level languages are compiled down to assembler (which is then compiled down to machine code). Some of the earliest and most recognizable third-level languages include Fortran, Cobol, and [C][c].

[c]: https://en.wikipedia.org/wiki/C_(programming_language)

```c
#include <stdio.h>

int main(void)
{
    printf("hello, world\n");
}
```
—*Hello, World* in C, from [Wikipedia][c]

The [C language][c] is a procedural language that has become one of the most widely used programming languages in the world. Originally developed by [Dennis Ritchie](https://en.wikipedia.org/wiki/Dennis_Ritchie) at Bell Labs between 1969 and 1973, it still forms the basis of many contemporary programming languages and operating systems. Objective-C, Ruby, Java, Swift, and Python are all [C-family](https://en.wikipedia.org/wiki/List_of_C-family_programming_languages) languages that extend C's functionality into object-orientation. But yet, these high levels of abstraction are all compiled down to machine code when the application is run.

## Object-Oriented Programming (OOP)

### This Is Not An Object

Since all computer code boils down to binary, it's natural to wonder "how can a string of ones and zeroes be referred to as an 'object'?" The use of the word "object" is another abstraction of thought. An "object" in code has no more physical form than does a word in any human language. Sure, words have physical representations: speaking a word causes air to vibrate in a sound wave, ink on a page can be shaped into symbols that represent the word, a meaning can be pointed at or mimed out; but none of these are the word itself. Human language is also a system of abstraction: it communicates the *idea* of a thing, but not the thing itself.

![](https://curriculum-content.s3.amazonaws.com/ios-intro-to-objects-unit/MagrittePipe.jpg)    
—[*The Treachery of Images*][not_a_pipe], [René Magritte][magritte], 1927  
trans. "This is not a pipe."

[not_a_pipe]: https://en.wikipedia.org/wiki/The_Treachery_of_Images
[magritte]: https://en.wikipedia.org/wiki/Ren%C3%A9_Magritte

This image of a pipe is no more a pipe than the word "pipe" is a pipe; in the same way, a code object named `pipe` is not a pipe, but only another form of representing the *idea* of a pipe.

>As humans, we’re constantly faced with myriad facts and impressions that we must make sense of. To do so, we must abstract underlying structure away from surface details and discover the fundamental relations at work. Abstractions reveal causes and effects, expose patterns and frameworks, and separate what’s important from what’s not. Object orientation provides an abstraction of the data on which you operate; moreover, it provides a concrete grouping between the data and the operations you can perform with the data—in effect giving the data behavior.  
>—[*Object-Oriented Programming with Objective-C*][apple_oop_guide_oop], Apple Inc.

[apple_oop_guide_oop]: https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/OOP_ObjC/Articles/ooOOP.html#//apple_ref/doc/uid/TP40005149-CH8-SW3

A code object representing a water pipe (instead of a smoking pipe) might contain values for `length`, `diameter`, `material`, and `manufacturer`. The bundling of these individual pieces of information together begins to form a larger whole.

### Methods

Object-Oriented Programming, however, requires more than just the bundling up of individual pieces of data in order to represent a "thing"—it also bundles customized functions that can be performed *on* that data. These are called **methods**: behaviors that an object can perform upon its internal data, which are its "**properties**". 

Methods are, in effect, functions that can only be called upon their associated object's properties. Without the inclusion of methods into a programming language, those "bundles of data" remain inert except when changed by an outside force (i.e. a global function call). Our coded representation of a `pipe` remains just a hunk of raw material with some interesting attributes but no practical application or usefulness.

However, if it can *perform* a method, such as channeling a water supply from one reservoir to another, our previously inert "bundle of data" now has a *behavior*. It can now be appropriately called an **object**. A `channelWater` method on our `pipe` object might be written to accomplish the task of moving water a distance equivalent to the `pipe`'s `length` value and at a flow rate based upon its `diameter` value.

### Property Basics

In the previous lessons, you practiced declaring and setting local variables. A **property** is just like a local variable except that a property is a component of forming a larger whole—called an 'object'.

The `length` value of our `pipe` object from above would be programmed as a property—as would `diameter`, `material`, and `manufacturer`. Together, these make up the information that represents our abstraction of a pipe, which in our code we have named `pipe`. 

If the `length` property is an integer variable, then it will itself function in the same ways that any local integer variable will function, but with the added association of being a component of the `pipe` object. The `diameter` property might be a float value, while the `material` and ` manufacturer` properties might be strings. A string object that is a property is still a string in every way, and contains its own properties that when assembled represent the text that it holds.

#### Dot Notation

The best-practice way to interact with a property, and the way suggested by Apple, is by using dot (`.`) notation. This syntax can be used for either setting (writing to) or getting (reading from) a property's value—unless, of course, that property is read-only (or "write-protected").

The `length`, `uppercaseString`, and `lowercaseString` methods on `NSString` that we've used repeatedly in previous lessons are actually the "getter" methods for properties by the same name. Calling them as methods is valid syntax:

```objc
// method syntax (valid)

NSString *magritte = @"Ceci n`est pas une pipe.";

NSLog(@"Length: %lu", [magritte length]);
NSLog(@"%@", [magritte uppercaseString]);
NSLog(@"%@", [magritte lowercaseString]);
```
This will print:

```
Length: 24
CECI N`EST PAS UNE PIPE.
ceci n`est pas une pipe.
```
But, it's actually better practice to use dot notation when accessing properties:

```objc
// dot notation (preferred)

NSString *magritte = @"Ceci n`est pas une pipe.";

NSLog(@"Length: %lu", magritte.length);
NSLog(@"%@", magritte.uppercaseString);
NSLog(@"%@", magritte.lowercaseString);
```
This will also print:

```
Length: 24
CECI N`EST PAS UNE PIPE.
ceci n`est pas une pipe.
```
**Advanced:** *Using* `self.property` *allows access to a property within the same file.*

#### Chaining Dot Notation

One of the values of dot notation is the ability to daisy-chain properties without having to nest method calls. With method syntax, the enclosing square brackets quickly pile up:

**Note:** *In this next example, we're going to experiment with uppercasing and then lowercasing the German word "Straße". The uppercase form of the "ß" ("ess-tsett") character is "SS", which then gets lowercased into "ss". This has the side effect of changing the length of the string.*

```objc
// method syntax (valid)

NSString *strasse = @"Straße";

NSLog(@"Length: %lu", [strasse length]);
NSLog(@"Length: %lu", [[[strasse uppercaseString] lowercaseString] length]);
```

This will print:

```
Length: 6
Length: 7
```

But writing it out in dot notation provides a much cleaner syntax:

```objc
// dot notation (preferred)

NSString *strasse = @"Straße";

NSLog(@"Length: %lu", strasse.length);
NSLog(@"Length: %lu", strasse.uppercaseString.lowercaseString.length);
```

This will also print:

```
Length: 6
Length: 7
```
Using dot notation improves readability and avoids the stumbling block of counting a group of brackets.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/reading-ios-introToObjects' title='Introduction to Object Orientation'>Introduction to Object Orientation</a> on Learn.co and start learning to code for free.</p>
