#Objects

## What is an object?

Back in the day, we had procedural programming. 

######Example (in BASIC)
```
READY
10 PRINT "Hello there."
20 INPUT "Do you like me? (Type y or n)"; ans$
30 IF ans$ = "n" then GOTO 50
40 END "Cool. I like you too!"
50 PRINT "Maybe you didn't understand the question. Let me ask it again."
60 GOTO 20
```

Then, programmers made a transition to naming blocks of code, which became known as functions or methods. All of a sudden instead of going to a specific line number we could say something that was somewhat english-y to tell the program what code we wanted to run next and call it by name.

######Example (in C)

```
void DisplayWhoIAm(){
    printf("I am the writer of this tutorial!");
}
```

But then we realized that digital life really reflects our real lives, in many ways. And object-oriented programming was born. In the 1970's, Alan Kay developed an object-oriented language at Xerox Parc called Small Talk, the language to be used in the first personal computer. Coincidentally, Objective-C, the language used for developing in iOS / OS X was built based on the style of Small Talk.

## Behaviors of objects

So, today we have objects, which have behaviors and attributes associated with them. Think of them as a set of related functions (methods) and properties, that as a human being, we can make sense of. We "encapsulate" (think: box up) all of these related methods and properties in one place, and then give it a name, the name of the object. The box we keep all of these methods and properties in is our Class. It serves as the instruction manaul or factory to create a specific type of object.

Think about it. Let's take a `Car` class as an example. A `Car` has attributes (aka properties) such as its `color` and its `make` and `model` and `year` and `numberOfDoors`. It also has behaviors (aka methods). Its engine can be turned on and off. It can accelerate and brake. And it can signal the direction it is turning (well, perhaps with the help of its driver object.) The combination of all of this information in one place defines a `Car`. This is the `Car` class, with which we can make `Car` objects (also known as instances).

######Example
```objc
//  Car.m

@interface Car ()

@property (strong, nonatomic) NSNumber *numberOfDoors;
@property (strong, nonatomic) NSString *make;
@property (strong, nonatomic) NSString *model;
@property (strong, nonatomic) NSString *year;

- (void)accelerate;
- (void)decelerate;
- (void)signalTurnToDirection:(NSString *)direction;
- (void)toggleEngine:(BOOL)isOn;

@end

@implementation Car
...
@end
```

## Difference between an instance and a class

In order to explain classes vs. instances, let's use another analogy. 

A human being has a set of standard properties (arms, legs, vision, height, weight, sense of humor, etc.)

But the specifics of those differ by individual. While most folks have two arms and legs, other properties such as height, weight, and sense of humor are more variable across individuals.

Likewise, there are behaviors of the entire race of humans and there are behaviors that apply just to the writer of this lesson, an individual. I (the writer) might be a class clown, but not all humans are class-clowns. All humans (well, most) think for themselves. That is a behavior of the entire class of human beings.

So you can think of the class as applying to every individual human being, and the instance as just a copy of the details of the class applying to a specific person (we're all just a carbon copy of each other, with our little bits of DNA that are slightly different.) That said, if we all become zombies one day, we might need to change the behavior (method) of thinking for ourselves, to simpler behavior applying to the entire class of humans such as "not thinking much."

######Example 
```objc

- (void)thinkForOurselves:(NSString *)whatIAmThinking {
	
	NSLog(@"%@",whatIAmThinking);
}

```

######Example
```objc

+ (void)notThinkingMuch {
	
	NSLog(@"GIVE ME FOOOOOOOD.")
}
```

Notice the primary difference between the two above methods is that one begins with a `+` and the other with a `-`. The `+` indicates that this is a class method. It applies to the entire class of an object. If we were all zombies, we would all think about food all the time and not much else, so this applies to the entire class. On the other hand, if we are all individuals, we all have our own thoughts, and with the creation of each `Human` object, we can run the method `thinkForOurselves:` (and log our own thoughts.)

When we call instance methods, we either call the method with the instance as the "receiver." If we call the instance method within the instance's class, we refer to the receiver as `self`.


######Example
```objc
//Human.m

@interface Human()

- (void)thinkForOurselves:(NSString *)whatIAmThinking;
- (void)buyALotteryTicket;

@end

@implementation Human

- (void)buyALotteryTicket
{
	[self whatIAmThinking:@"Will I win the lottery?"];
}

- (void)thinkForOurselves:(NSString *)whatIAmThinking {
	
	NSLog(@"%@",whatIAmThinking);
}

...

@end
```

######Example
```objc
//ClassOtherThanHuman.m

#import "Human.h";

@interface

- (void)methodThatIsInterestedInWhatASpecificHumanIsThinking:(NSString *)whatAHumanIsThinking;

@end 

@implementation ClassOtherThanHuman

- (void)methodThatIsInterestedInWhatASpecificHumanIsThinking:(NSString *)whatAHumanIsThinking
{
	Human *aNewHuman = [Human alloc] init];
	[aNewHuman whatIAmThinking:whatAHumanIsThinking];
}

...

@end
```
However, when we call class methods, we call the method with the class as the receiver, whether we are calling the method from within the same class or another class.

######Example
```objc
//Zombie.m

@interface Zombie()

+ (void)notThinkingMuch
- (void)buyALotteryTicket;

@end

@implementation Zombie

+ (void)notThinkingMuch {
	
	NSLog(@"GIVE ME FOOOOOOOD.")
}

- (void)interactWithAnotherZombie
{
	[Human notThinkingMuch];
}

...

@end
```

Keep in mind, whereas normally we might call a class method from within an instance method, or an instance method from within an instance method, we *cannot* call an instance method in a class method. If you try to do so, you will get the following error message from the linter.

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
