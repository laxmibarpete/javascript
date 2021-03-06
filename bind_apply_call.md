# bind, apply and call

> these are the prototype methods of functions to alter behavior to achieve something.

> Use `.bind()` when you want that function to later be called with a certain context, useful in events. 

My understanding -- `.bind()` affects permanently after its call

> Use `.call()` or `.apply()` when you want to invoke the function immediately, with modification of the context.

My understanding -- one time 

- Example

Suppose your maths teacher asked you to create a library and submit it.
You wrote an abstract library which finds area and circumference of the circle.

```
var mathLib = {
    pi: 3.14,
    area: function(r) {
        return this.pi * r * r;
    },
    circumference: function(r) {
        return 2 * this.pi * r;
    }
};

```
You submitted library to the professor. Now it is time to submit code which calls that math library.
```
mathLib.area(2);
12.56
```
While submitting second code samples, you found in guidelines that professor asked you to use
constant `pi` with 5 decimals precision. Oh gosh! You just used 3.14, not 3.14159.
Now you have no chance to send library as the deadline was over. JS call function saves you. 
Just call your code in this way

`mathLib.area.call({pi: 3.14159}, 2);`

and it takes your new pi value on the fly. The output is

`12.56636`


```
var mathLib = {
    pi: 3.14,
    area: function(r) {
        return this.pi * r * r;
    },
    circumference: function(r) {
        return 2 * this.pi * r;
    }
};
mathLib.area(2);
12.56
mathLib.area.call({pi: 3.14159}, 2);
12.56636

mathLib.area(2);
12.56
```
> now you can understand why im talking about one time operation with call and apply.

If you observe the call function takes two arguments:

- Context
- Function arguments

A context is an object that replaces `this` keyword inside the area function.
Later arguments are passed as function arguments.

```
var cylinder = {
    pi: 3.14,
    volume: function(r, h) {
        return this.pi * r * r * h;
    }
};

cylinder.volume.call({pi: 3.14159}, 2, 6);
75.39815999999999
```

Did you see those function arguments are passed as subsequent arguments after context object.

Apply is exactly same except Function arguments are passed as a list

```
cylinder.volume.apply({pi: 3.14159}, [2, 6]);
75.39815999999999
```

> Bind attaches a brand new this to a given function. In bind’s case, the function is not executed instantly like Call Apply.
```
var newVolume = cylinder.volume.bind({pi: 3.14159}); // This is not instant call
// After some long time, somewhere in the wild 
newVolume(2,6); // Now pi is 3.14159
```

> What is the use of Bind?
It allows us to inject a context into a function which returns a new function with updated context. 
It means this variable will be user supplied variable. This is very useful while working with JavaScript events.

### now you can understand 

My understanding -- `.bind()` affects permanently after its call
