tags: #model_construction


## Main takeaway
You should promote variables up a level if they are generally useful at that level or used in many components, whereas you should connect variables if you need more precise control of where the data is being passed.

## What does promoting mean
Promoting is when you push a variable up a level. This allows it to come from the component level and go up to the group level. Then, any component that also promotes that variable has access to it within that group.

You must promote both the inputs and outputs if you want them to be linked. OpenMDAO specifically has different keyword args for that, or you can use promotes straight up.

You can also change the name of what you're promoting by using a tuple instead of just the string of the name.

Promoting with a wildcard is a personal preference that might be valid for small models but becomes untenable with larger models. We highly suggest you explicitly name what you are promoting to make it clear what is coming in and out of the system.

TODO: viz showing block groups and promoting variables up

## What does connecting mean?
Connecting means that you specifically call out where the variable is coming from and going. This allows precise control over the variable passing. This is especially useful when you might have multiple versions of something with the same name and want to keep them separate. For instance, the cargo load of a plane within a fleet of planes.

Connecting often takes a bit more time and effort to get right as you need to know where in your model the variables live that you want to connect.

There are some handy Python manipulations to help you achieve a fully connected model a bit faster. F-strings are amazingly helpful, and if you have many connections coming from the same models you can add shortcuts to make your code more readable.

It's also a bit easier to do connections that are based on logic as compared to promotions.

## We need to discuss absolute vs promoted names
In OpenMDAO, there are two types of names for a single variable. There's the absolute name, which is where it lives in absolute terms within the model. This means that all groups and components are represented in the name. If you have a very nested variable, this name might be quite long.

There's also the promoted name, which is a moniker available when you promote variables. You can access variables via this name once you pass them up to different levels.

Viz showing the promoted and absolute name and how it shifts