# Object Orientation

## Objectives


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

Object-Oriented Programming, however, requires more than just the bundling up of individual pieces of data in order to represent a "thing"—it also bundles customized functions that can be performed *on* that data. These are called **methods**: behaviors that an object can perform upon its internal data, called its "**member variables**". 

Methods are, in effect, functions that can only be called upon the their associated object's member variables. Without the inclusion of methods into a programming language, those "bundles of data" remain inert except when changed by an outside force (i.e. a global function call). Our coded representation of a `pipe` remains just a hunk of raw material with some interesting attributes but no practical application or usefulness.

However, if it can *perform* a method, such as channeling a water supply from one reservoir to another, our previously inert "bundle of data" now has a *behavior*. It can now be appropriately called an **object**. A `channelWater` method on our `pipe` object might be written to accomplish the task of moving water a distance equivalent to the `pipe`'s `length` value and at a flow rate based upon its `diameter` value.

### Property Basics

In the previous lessons, you got practiced with declaring and setting local variables. **Properties** are just like local variables except that a property is a component of forming a larger object.

The `length` value of our `pipe` object from above would be programmed as a property—as would `diameter`, `material`, and `manufacturer`. Together, these make up the information that represents our abstraction of a pipe, which in our code we have named `pipe`. 

If the `length` property is an integer variable, then it will itself function in the same ways that any local integer variable will function, but with the added association of being a component of `pipe` object. The `diameter` property might be a float value, while the `material` and ` manufacturer` properties might be strings. A string object that is a property is still a string in every way, and contains its own properties that are assembled to represent the text that it holds.

#### Dot Notation








## Class Versus Instance

*That's what a ship is, you know. It's not just a keel and a hull and a deck and sails. That's what a ship needs. But what a ship is...what the* Black Pearl *really is...is freedom.*  
—Jack Sparrow, [*The Pirates of the Caribbean (2003)*][imdb_potc]

[imdb_potc]: http://www.imdb.com/title/tt0325980/?ref_=nv_sr_2

If we were to write a program that simulates naval combat, we might start by creating a `ship` object with properties that detail all of the data for a naval warship: `name`, `rating`, `shipClass`, `length`, `beam`, `keel`, `displacement`, `captain`, `crew`, `topSpeed`, `currentSpeed`, `heading`, `hullCondition`, `armament`, `ammunition`, `rumSupply`, and so on. 

What if we had to manually declare the value of *every* property for *every* warship that we wish to have in our simulation program? That's a lot of variable declarations! But every warship in our simulation will have data for each of these fields; it would save us a lot of work if we could find some way of creating a "warship" template, and then populate the data for the properties of each separate warship whenever we copy the template.

![](https://upload.wikimedia.org/wikipedia/commons/0/0a/Battle_Group_Alpha_%28Midway%2C_Iowa%29_underway%2C_1987.jpg)  
—*Battle Group Alpha (*Midway*,* Iowa*) underway, 1987*, [image by US Navy](https://en.wikipedia.org/wiki/File:Battle_Group_Alpha_(Midway,_Iowa)_underway,_1987.jpg)

This is exactly what [Ole-Johan Dahl][ojd] and [Kristen Nygaard][kristen_nygaard] realized as they worked on developing the [Simula I and Simula 67 languages][simula] in the 1960s. Simula introduced the concept of **class** and **instance** (among other breakthroughs), and was a language that was instrumental in the development of [Smalltalk][smalltalk], the first fully-realized object-oriented programming language, at [Xerox PARC][parc] in the 1970s.

[ojd]: https://en.wikipedia.org/wiki/Ole-Johan_Dahl
[kristen_nygaard]: https://en.wikipedia.org/wiki/Kristen_Nygaard
[simula]: https://en.wikipedia.org/wiki/Simula
[smalltalk]: https://en.wikipedia.org/wiki/Smalltalk
[parc]: https://en.wikipedia.org/wiki/PARC_(company)

If we can set up the template for the warships (let's call it "Warship", capitalized), then we've outlined the data points that are necessary for creating an individual "warship" (lowercase). In the object-oriented paradigm, the template "Warship" is referred to as the `Warship` **class**, and all individual "warship"s created from the "Warship" template are referred to as **instances** of the `Warship` class.

Maritime tradition often uses similar language when describing the design form (or "class") of a ship. The [USS *New Jersey* (BB-62)][uss_new_jersey], for example, is an [*Iowa*-class battleship][iowa_class]; the ship class being named after that design's "lead ship", or first constructed ship, in this case, the [USS *Iowa* (BB-61)][uss_iowa]. Two other *Iowa*-class battleships were commissioned by the U.S. Navy, the [USS *Missouri* (BB-63)][uss_missouri] and the [USS *Wisconsin* (BB-64)][uss_wisconsin]. For our purposes, we could describe each of the four battleships as **instances** of the "*Iowa*-class battleship" **class**.

[iowa_class]: https://en.wikipedia.org/wiki/Iowa-class_battleship
[uss_iowa]: https://en.wikipedia.org/wiki/USS_Iowa_(BB-61)
[uss_new_jersey]: https://en.wikipedia.org/wiki/USS_New_Jersey_(BB-62)
[uss_missouri]: https://en.wikipedia.org/wiki/USS_Missouri_(BB-63)
[uss_wisconsin]: https://en.wikipedia.org/wiki/USS_Wisconsin_(BB-64)

![](https://upload.wikimedia.org/wikipedia/commons/7/70/USS_Missouri_transfers.JPG)
—*USS Missouri (BB-63) (at left) transferring personnel to USS Iowa (BB-61), while operating off Japan on 20 August 1945.*, [image by US Navy](https://en.wikipedia.org/wiki/File:USS_Missouri_transfers.JPG)

**//Flat-fact:** *The* Iowa*-class was the largest and final battleship design of the US Navy, whose four ships saw intermittent service from 1943 until 1992, a span of nearly fifty years. Between them, participated in five US wars (including the Cold War) and the* Iowa*-class is the only WWII ship class whose entire membership still survives. Each of the four ships were donated by the US Navy to preservation society who maintain them in maritime museums across the United States.*

All four of the individual battleships may have slight differences in measurements, but each share a common set of attributes such as having a length of 887 feet (270 m), a beam of 108 feet (33 m), nine 16-inch primary guns, and twenty 5-inch secondary guns. While their individual displacement tonnage, crew complements, and specific armaments varied across their service careers, the specific values of these "member variables" are not part of what defines each ship as an *Iowa*-class battleship, but rather, the *possession* of these attributes is what does.

### Member Variables vs. Instance Variables

When we create an instance object, its member variables can (and should) get populated with individual pieces of data whose values are not shared by other instance objects of the same class. The term "**instance variable**" refers specifically to these pieces of data that are associated with an instance object.

An instance of our `Warship` class (let's call it `ussIowa`) which has a member variable for `length`, will have an instance variable for the "length" attribute associated with that ship. In Objective-C, the instance variable is typically denoted by prefixing the member variable's name with an underscore (`_`), so `_length` would be the conventional name for `ussIowa`'s instance variable that contains the information associated with the "length" attribute.

**Top-tip:** *It is bad practice to access an instance variable directly unless within the context of an initializer, setter, or getter method implementation. Otherwise, you should rely on these methods to read from and write to the instance variable itself.* 


## Accessing A Property

When we set up our `Warship` class, its member variables `name`, `length`, `beam`, `keel`, etc., would most likely get programmed as *properties*. A **property** generally refers to a toolset of three things: an instance variable, a setter method, and a getter method.

The **instance variable** is the actual piece of data that the property manages, typically named after the property but prefixed with and underscore (`_`).

The **setter** is a method that is responsible for writing to the instance variable, typically named after the property that it writes to (or "sets"), but is prefixed with "`set`", as in `setLength:` for the `length` property.

The **getter** is a method that is responsible for reading the instance variable, typically named after the property whose value it retrieves (or "gets"), as in `length` (method) for the `length` property.

**Advanced:** *A read-only property is, in effect, just an instance variable with no associated setter method—only a getter method.*

Whenever possible, use the setters and getters to interact with an instance variable. Avoid modifying it directly.

You've already interacted with the `count` getter method on arrays:









## The Class Object



### Metaphor of the Printing Press


### Class Methods


^^^Mark^^^


## Instance variables and Properties

That said, instance variables apply to instances! Therefore when being used, we should not expect them to apply to the entire class. In other words, if you haven't told our program how funny I am explicitly, it won't know (or at best, it will set me, an instance of the class `HumanBeing`, to have a default standard level of humor, instead of the ROFL level of humor with which I should actually be attributed.)

And again, since instance variables apply to specific instances, they may not be called within class methods.

## Initializers 

Let's say though that we do want to setup a default set of arms, legs, height, weight, and sense of humor. We can do that when we "initialize" a new instance of `Human`. What does initialization mean in the context of programming? Well, think of the class `HumanBeing` as the instruction manual for creating a `Human` object. When we initialize a new instance of a `Human`, we are really giving that instance of the `Human` being all of the properties and behaviors of the class. Initialization is the point at which the `Human` instance becomes formed, or is born, you might say. And every human is born with some innate properties. Generally speaking, the default initialization of a `Human` includes 2 arms, 2 legs, 7.5 lbs, 20 inches long, and no sense of humor. (Babies don't laugh for a few weeks to months!) 

Additionally, every `Human` has a name. And it wouldn't make much sense for a `Human` to be nameless. So, we use custom initializers to ensure that the required properties of a `Human` are setup from the start and never `nil`. 

Here's how that might look:

######Example
```objc
//Human.m

#import "Human.h";

...

@implementation Human

- (instancetype)init
{
	self = [super init];

	if (self) 
	{
		_name = @"Average Joe"
		_weight = 7.5;
		_height = 20;
		_arms = 2;
		_legs = 2;
		_senseOfHumor = @"average";
	}

	return self;
}

@end

```

Line by line, this code is first making sure our superclass is initialized. It is an odd line of code but will always exist in our designated initializer. There will only be one designated initializer in the class. All others will point to this initializer. (You will see this in our next example.)

Then, assuming we initialize our superclass successfully, we will initialize all of the instance variables of our class.

And finally, we return ourselves, fully formed!

But what if we don't want to wait to hold an in-depth conversation with them about computer programming? In that case we would like to build a custom initializer that allows us to set the properties of our new `Human` object such that they are more of an adult from the start (or an oversized baby?)

```objc
//Human.m

#import "Human.h";

...

@implementation Human

- (instancetype)initWithName:(NSString *)name WeightInPounds:(NSNumber *)weight HeightInInches:(NSNumber *)height SenseOfHumor:(NSString *)senseOfHumor 
{
	self = [super init];

	if (self) 
	{
		_name = name;
		_weight = weight;
		_height = height;
		_senseOfHumor = senseOfHumor;
		_arms = 2;
		_legs = 2;
	}

	return self;
}

- (instancetype)init
{
	return [self initWithName:@"Average Joe" WeightInPounds:7.5 HeightInInches:20 SenseOfHumor:@"average"];
}

@end

```
Here we have both a designated initializer (`initWithName:WeightInPounds:HeightInInches:SenseOfHumor:`) and what we call the default initializer (`init`). Our designated initializer is also known as a convenience initializer, because it provides us the convenience of initializing the properties of our `Human` instance all up front. Note also the fact that our designated initializer has the boilerplate code that checks to ensure our super class has been initialized, while our default only returns values to the designated initializer. This is what we meant earlier when we said that other initializers point us to the designated initializer.

## Public vs. Private methods

If you place a method or property in your `.h` file, it will be "public", visible to other classes / users of the class in which those methods or properties are declared and defined.

######Example
```objc
//Human.h

@interface Human : NSObject

@property (nonatomic, strong) NSNumber *weight;
@property (nonatomic, strong) NSNumber *height;

- (void)socializeWithAnotherHuman:(Human *)otherHuman;

@end
```

If you place a method or property in your `.m` file, it will be "private", and only visible to other users of the class in which those methods and/or properties are defined. Just an aside: Methods and properties defined in your .m are not actually unavailable to a third party; however, they do not announce themselves either. Someone who really wanted to know what the insides of your classes looked like could get in their and check out your classes' innards. (In fact, programmers do this regularly with Apple's proprietary Cocoa framework!) 

######Example
```objc
//Human.m

@interface Human()

@property (nonatomic, retain) NSString * name;
@property (nonatomic, strong) NSNumber *birthdate;

- (NSString *)sayHi
{
	return @"Hi!";
}

@end

```

The thing to keep in mind, and how to decide whether something belongs in the `.h.` or `.m` file, is this: When you put something in your `.h` file you are responsible to the classes' users of that method. So, in order to avoid excess accountability, we try to keep things private. In other words, if you are not sure whether a method should be public or private, you should default to making it private.

##Collections of Objects

As you become more familiar with objects, you'll begin to realize that an object's properties are really just other objects. Until now, those objects were standard data types such as `NSString` or `NSNumber`. But once we build our own objects, they also may be properties of an object. For instance, consider the `House` object. Every `House` has `Room` objects, it is painted a certain `color`, and is a certain number of `squarefeet`. So our house interface might look like this, with some added properties:

######Example
```objc

//  House.m

#import "Room.h"
#import "Chimney.h"
#import "WaterHeater.h"
@interface House ()

@property (strong, nonatomic) NSArray *rooms;
@property (strong, nonatomic) NSArray *chimneys;
@property (strong, nonatomic) NSNumber *squarefeet;
@property (strong, nonatomic) NSNumber *floors;
@property (strong, nonatomic) NSString *color;
@property (strong, nonatomic) WaterHeater *waterHeater;

@end

@implementation House
...
@end
```

Besides our standard `NSString` and `NSNumber` objects above, we have collections of custom objects. Somewhere in our project there is a `Room` class, and another class called `Chimney`, and these classes define the properties of a `Room` and a `Chimney`, respectively. This allows us to really capture the complexity at any level of granularity we wish. There is also a `WaterHeater` class, and given each home has only one `WaterHeater` by default, the property for this custom object is not a collection. 

Some folks we have spoken with in the past have had trouble with separating this concept from inheritance. Let us be clear now -- a room is not a subclass, or type of house. A room is in a house, but a `Room` is not a type of `House`, nor is a `Chimney` a type of `House`. If we had a class called `Residence`, then `House` might inherit from that class, because it is a type of `Residence` (as is `Apartment`, `Condo`, `Yurt`, and `MobileHome`). 

There is a major difference between an object being made up of other objects as in the case of `House` and `Room` or `Engine` and `Cylinders`, and an object being a subclass or type of another object as with `Residence` and `House`. Be sure to read up on inheritance as well if you haven't already, and make sure you understand the difference between these concepts!
