# Introduction to Object Orientation

## Objectives

1. Understand programming paradigms as a form of human abstraction.
2. Learn the distinguishing characteristics of Object Oriented Programming (OOP).
3. Define the terms "methods" and "properties" in the context of OOP.
4. Use dot notation to access an object's properties.
5. Chain dot notation to access a property of a property.

## Object-Oriented Programming (OOP)

*An object-oriented approach to application development makes programs more intuitive to design, faster to develop, more amenable to modification, and easier to understand.*  
—[*Object-Oriented Programming with Objective-C*][apple_oop_guide_intro], Apple Inc.

[apple_oop_guide_intro]: https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/OOP_ObjC/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005149-CH1-SW2

Since all computer code boils down to binary it's natural to wonder, "how can a string of ones and zeroes be referred to as an 'object'?" The use of the word "object" is an abstraction of thought. An "object" in code has no more physical form than does a word in any human language. Sure, words have physical representations: speaking a word causes air to vibrate in a sound wave, ink on a page can be shaped into symbols that represent the word, a meaning can be pointed at or mimed out; but none of these are the word itself. Human language is a system of abstraction: it communicates the *idea* of a thing, but not the thing itself.

![](https://upload.wikimedia.org/wikipedia/en/b/b9/MagrittePipe.jpg)  
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

Methods are, in effect, functions that can only be called upon the their associated object's properties. Without the inclusion of methods into a programming language, those "bundles of data" remain inert except when changed by an outside force (i.e. a global function call). Our coded representation of a `pipe` remains just a hunk of raw material with some interesting attributes but no practical application or usefulness.

However, if it can *perform* a method, such as channeling a water supply from one reservoir to another, our previously inert "bundle of data" now has a *behavior*. It can now be appropriately called an **object**. A `channelWater` method on our `pipe` object might be written to accomplish the task of moving water a distance equivalent to the `pipe`'s `length` value and at a flow rate based upon its `diameter` value.

### Property Basics

In the previous lessons, you got practiced with declaring and setting local variables. **Properties** are just like local variables except that a property is a component of forming a larger object.

The `length` value of our `pipe` object from above would be programmed as a property—as would `diameter`, `material`, and `manufacturer`. Together, these make up the information that represents our abstraction of a pipe, which in our code we have named `pipe`. 

If the `length` property is an integer variable, then it will itself function in the same ways that any local integer variable will function, but with the added association of being a component of `pipe` object. The `diameter` property might be a float value, while the `material` and ` manufacturer` properties might be strings. A string object that is a property is still a string in every way, and contains its own properties that when assembled represent the text that it holds.

#### Dot Notation

The best-practice way to interact with a property, and the way suggested by Apple, is by using dot (`.`) notation. This syntax can be used for either setting (writing to) or getting (reading from) a property's value—unless, of course, that property is read-only (or "write-protected").

The `length`, `uppercaseString`, and `lowercaseString` methods on `NSString` that we've used repeatedly in the previous lesson are actually the "getter" methods for properties by the same name. Calling them as methods is valid syntax:

```objc
// method syntax (valid)

NSString *magritte = @"Leci n`est pas une pipe.";

NSLog(@"Length: %lu", [magritte length]);
NSLog(@"%@", [magritte uppercaseString]);
NSLog(@"%@", [magritte lowercaseString]);
```
This will print:

```
Length: 24
LECI N`EST PAS UNE PIPE.
leci n`est pas une pipe.
```
But, it's actually better practice to use dot notation when accessing properties:

```objc
// dot notation (preferred)

NSString *magritte = @"Leci n`est pas une pipe.";

NSLog(@"Length: %lu", magritte.length);
NSLog(@"%@", magritte.uppercaseString);
NSLog(@"%@", magritte.lowercaseString);
```
This will also print:

```
Length: 24
LECI N`EST PAS UNE PIPE.
leci n`est pas une pipe.
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
Using dot notation vastly improves readability.
