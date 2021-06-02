---
title: About
date: '2018-02-22T17:01:34+07:00'
---


Objective 3 - compose hooks in a custom hook to extend multiple pieces of stateful logic



## Overview

Just as we can compose functions in vanilla JavaScript and components in React to create new functionality, we can extend our stateful logic by combining several hooks in a powerful, single custom hook. This compositional ability allows us to build out interesting abilities by combining various hooks in our application.

We can develop this complexity using multiple hooks inside a single custom hook. We've done this already when we called useState inside useInput. Pretty cool! Now imagine writing several custom hooks and combining all of that logic into a single custom hook to use in your components. The possibilities are dizzying! And amazing! Let's try it out by expanding the useInput custom hook we've already built.

## Follow Along

We need to start by building out a second custom hook. Later on, we'll combine it with the useInput custom hook from the previous objective to achieve a more compelling hook with multiple pieces of stateful logic.

First, we'll implement the new hook that we will call useLocalStorage:

Let's walk through what we're doing here. First, we pass in a key-value (like: "input1," "input2" ) and an initialValue. These two parameters (key and value) are used in the useState hook call and used immediately inside our custom hooks. Instead of just passing in an initial value to this useState hook, we are using an anonymous arrow function as a callback to do two things:

1.  Check if the window.localStorage has a specific item (retrieved by key) in it

2.  Return that item from local storage if it exists or the initialValue otherwise

Because of this, our hook can now successfully check to see if a specific state item exists in localStorage, **and** it can use that item if it exists instead of the provided initialValue. Then, we also have a setValue function that takes a value as a parameter, sets it to the current storedValue by using the setStoredValue provided by useState, and sets it localStorage. As our state is now stored, our custom hook will check here on refresh to see if the state exists.

Now that we have a custom hook for controlling value placement (and updates) in localStorage, we can combine it with useInput to create powerful logic. Take a look at the completed code, and then we'll talk about what it's doing:

While our useLocalStorage hook has stayed the same, our useInput custom hook has some nice upgrades going on. Instead of implementing useState from React as before, we're now using useLocalStorage. Furthermore, we're also taking in two parameters instead of one - key and initialValue. These are then passed directly into the useLocalStorage hook. Immediately, the hook sets about implementing special logic with the variables as described above. This returns to our useInput custom hook with either a value from localStorage or our initialValue, and our useInput custom hook then returns a value, setValue function, and a handleChanges function in an array just the same as it did before.

Now when we call the useInput hook in a component to control inputs dynamically, we just need to pass in a unique key for each input to keep track of it in localStorage. Something like this:

Although this isn't something you will often do (storing input values in localStorage), this setup is quite powerful, and it effectively demonstrates how composable hooks can be; by combining the stateful logic of multiple custom hooks, you can compose a really nice custom hook with advanced stateful logic.

One final thing to note is that we can employ the useLocalStorage custom hook in other places now as well. So, not only do we have an extra-powerful useInput created by composing multiple hooks together, we also have another custom hook available to us anytime we want to persist data in localStorage.

## Challenge

Try to think of different instances where you could compose different custom hooks together, particularly with the new useLocalStorage hook that you learned above. Be as creative as possible in the implementations that you think of.



\---

\---

# Objective 2 - apply non-visual behavior (stateful logic) with custom hooks&#xA;&#xA;

## Overview

Custom Hooks, are so-called because you are building the hook yourself (customizing it), to apply non-visual behavior and stateful logic throughout your components. This way, you can reuse the same hook over and over again. Custom hooks follow the same patterns of naming that you've already learned (i.e. prefacing the function name with use, as in useState). You can build a reusable custom hook for anything from handling controlled inputs, to managing event listeners, or watching for key presses.

## Follow Along

Let's start with the same component that we evaluated in the objective above. Go ahead and look over it one more time, this time making sure to understand what the various parts are doing.

See how we have a useState hook, a handleChange function to update based on any changes, and a changeTitle function to change the actual title of the component when we submit the form?

Now, what happens if we need to issue state for multiple input tags? If we were to follow the lead of the patterns shown above, we would end up having to rewrite large amounts of our code for each useState call that we've invoked in order to create state for our second, third, and fourth inputs.

Instead, let's build out our custom hook that to reuse stateful logic. In this way, we avoid repeating code unnecessarily. Read the following function and try to guess what each piece of code is doing:

In this useInput custom hook function, we're taking in an initialValue and returning three new values. We pass initialValue as a parameter on the function. initialValue is then passed into the useState hook, which returns an array with our value variable and setValue function (just the same as what you've used up to this point).

Next, we have a handleChanges function that uses the setValue function to update state to a new value. Finally, we return an array from our useInput custom hook containing the value variable, the setValue function, and the handleChanges function.

Let's take a look at this custom hook when it's imported and used in a component.

Whoa. That looks crazy, right? Don't worry. We're going to dissect this whole script to figure out exactly what each part is doing.

First off, notice that we're invoking the useInput custom hook three times at the top of the component and passing in an empty string as each one's initial value:

Our useInput hook returns a new copy of our custom hook and state each time. Also, because array destructuring is based on positioning and not the name, we are allowed by JavaScript to name each of the three items returned from useInput in different ways. This is why we can set the first item to username, the second to setUsername, and the third to handleUsername while the next two useInput calls return differently-named variables and functions.

From these invocations, it now becomes easy to rig up each of our input tags in our JSX just the same as we did before. Here they are again for your reference:

Notice how we are setting our handleUsername, handlePassword, and handleEmail functions to process changes to the input. Remember how we returned a handleChanges function from our custom hook? Well, we've renamed them here (again, thanks to array destructuring) and are using them just the same as before. However, now, we have less code for them in our component.

The final thing you should notice is the resetValue function. When we invoke it, we use the setValues returned from each useInput (again, each one is named differently) and pass it in our reset value (in this case, an empty string). Isn't this an easy way to change your state?

Here they are again for your reference:

By building out a custom hook, we can skip writing out all of the stateful logic for our non-visual behavior. Custom hooks produce beautiful, DRY code that is easy to read *and* use. You have built a *reusable* piece of code that makes it easy for you to import anywhere in your application and build out stateful logic in any of your components.





\---

\---

# Objective 1 - define stateful logic&#xA;&#xA;

## Overview

Stateful logic is logic that is built into a component. It can be a function that handles a click event or maybe a function that sets toggle state, or even a function that formats data before it gets displayed. Usually, this kind of logic deals with state in the component. Thus the moniker "stateful logic."

## Follow Along

Look at this component. Can you spot the stateful logic built into it?

You are probably looking at the two functions - handleChanges and changeTitle. If so, that is correct! And we can probably also count the title and inputText state in there as well. Those are all great examples of stateful logic. And really, the sky's the limit on what could be considered stateful logic in a React component.

\---

\---

## Overview&#xA;&#xA;

The componentDidMount method is a part of the mounting phase in the React Lifecycle. This method gets called as soon as the render method is called the first time, and it begs the question…now what?

When our component has mounted, we have the bare bones minimum we need to put something on the screen, so now what?

Inside of componentDidMount we can call setState which forces a re-render of our component. This way, any asynchronous actions should be performed inside of our componentDidMount function, especially when it comes to fetching data via HTTP. Data fetching is the de-facto purpose for using componentDidMount within a component because of its position within the component lifecycle.

**This method is guaranteed to be called only once in the whole lifecycle , immediately after a component is mounted.**

Until we know more about async AJAX calls, we'll use componentDidMount to set up state data living in a separate file. We'll do this by pulling the data in and setting it on state. This is also something you're going to have to do for your "Insta-clone" assignment today.

## Follow Along

Let's now put some of our knowledge together and build a react component that consumes some data from a separate resource.

To follow along, go ahead and click on [this link (Links to an external site.)](https://codesandbox.io/s/xlx1714w8w){:target="\_blank"} that will take you to a codesandbox.

Your index.js file should look a lot like this:

We are merely importing in a component called CitiesList and returning it to the screen. CitiesList is a pure functional Component whose only responsibility is to render the props passed down to it on to the screen. We have two very different styles of components here.

The only problem is that CitiesList wants to render something out, in fact, right now, if you look at the console, you'll see that props is an empty object. Our goal is to try and fix that.

Inside of the cities.js file, you'll find a global object with a property data as an array of cities. Let's import that into our index.js file and utilize the data.

If we console.log our cities, you'll see that we now have access to them. To fix the issue set forward earlier, we need to set this data on state and pass that data down as props to our CitiesList component. We'll do this inside of componentDidMount

## Challenge

Use this function inside of a componentDidMount call in an app with a state object set up. Fetch a list of Dogs you can see their beautiful images.

Once the dogs are on state. Build out a list of \<img> tags that display each doggo.







\---

\---

### The Constructor Function&#xA;&#xA;

You already know all about the constructor function as it pertains to classes in JavaScript. It's not much different in React. The constructor's purpose in React is to create components with inciting state data for the initial render. Any other props that the component receives on state can be done through the constructor function. We also used to bind all of our event handlers to the component via the constructor, and now we don't have to because of some special ESNext syntax that allows us to use arrow functions on our class methods. The following snippet is an example of this.

We will have ample time to practice application set up with state data via the constructor, so for now, soak in these examples.

Let's say we have some data from an external file living within our application. Let's say, too, that we want our component to render a list of that data out to the DOM. We would need to import the external data as an array, ( we don't care about the shape, or what type of data just that it lives on an array ) and use the constructor to set it up on state.

This how we use the constructor in the mounting phase of our component's lifecycle. Now that our data is set up on state, we can access it during our render portion of the mounting phase.

In conclusion, the constructor function on a React Class' Component's purpose is to serve up initial state data for when the time comes to mount up your DOM elements.

### The Render Method

The render() method is one of the React lifecycle methods that is used to tell React, to return some piece of DOM. The React virtual DOM will then handle the steps to mount those DOM pieces.

The render() method is required for a class component, and without it, the component won't work.

render should be a pure function, meaning it should return the same thing each time you call it. Its concern is to look at this.props and this.state and return some DOM element, a boolean, an array of DOM elements, and a couple of other things that you may want to reference or look into later.

The function is there to return what your component should render to the screen. Though many developers ignore it, Component is an important lifecycle method and should be regarded as such.

Another essential item to remember about render is that it is called not only in the Mounting Phase of the component lifecycle but also during the Updating Phase. This duality makes the render() method unique because it exists across multiple phases.

Now that we have our state data set up for us, we can use that state data to give a list of elements to React and let it do it's thing. Inside the render method of our component, let's return a list of items that the arbitraryStateData property (found on our state object) will generate.

One last thing to note is that any changes from setState invoke a call to our render method as well. We'll discuss more on this later, but it's important to remember that render() is called during mounting, and will be reinvoked if anything changes in our state object. You can think of the state object and render methods as existing together. The state object is like the bigger brother to the render function, it tells the render function what to do, and the render function obeys.

In conclusion, the render() method is how we tell React what data we want to turn into DOM elements. render() is necessary for every class component we create because we need it to return \<JSX/> elements. It is involved in the Mounting Phase and the Updating Phase of our component's lifecycle.

Continue to think about these methods as the mounting methods in our Component LifeCycle as you create more and more professional-looking code.

## Follow Along

Let's build out some friends together using [this code sandbox link (Links to an external site.)](https://codesandbox.io/s/5v3pql3y8x){:target="\_blank"}

Once there, you should see a page that renders out a \<h1> and \<p> tags. You should also notice a people.js file that contains an array of objects with this shape.

This is the data that our application will consume. Using the knowledge of the React LifeCycle methods, we will discuss how to get this data from one place to another while.

Let's start at the beginning with our constructor method. First, let's define a name for our state data. Our data object is all about people, so let's call our state object "persons" (intentionally not "people," so that we can tell the two apart.)

Let's import the people and set them up on our constructor's state object.

Now that we imported data, we can loop over that friend's array and generate a DOM element for each item in the array.





\---

\---

## Overview&#xA;&#xA;

React is, in essence, a combination of multiple components. A component can be as simple as a single piece of user interface that represents a small portion of our application. Conceptually, a component lifecycle happens in three phases. This idea is displayed nicely in the following diagram from one of the maintainers of React "Dan Abramov".

![](https://image.ibb.co/j8CzEd/lifecycle.jpg)

As you can see, the three React lifestyle phases are 1) Birth/Mounting, 2) Growth/Updating, and 3) Death/Unmounting.

### The Birth/Mounting Phase

This is the phase when the component is being built out from the ground up. A few things are happening here:
Whatever initial data you want access to will be defined on the constructor of this phase

*   Your render method is invoked.

*   componentDidMount gets called as well.

### Growth/Updating Phase

In the Growth/Updating phase you're updating compnent data.

*   setState can be used to change the component's state data, forcing a call to render.

*   shouldComponentUpdate is a method one could use here to stop a component from calling render if necessary.

### Death/Un-mounting Phase

Again, self-explanatory, but the unmounting phase includes removing the component from the screen.

*   Component is removed from the screen.

*   componentWillUnmount is called and can be used for any clean up you may need to do.

## Follow Along

Dive into the documentation at [ReactJS (Links to an external site.)](https://reactjs.org/docs/react-component.html#the-component-lifecycle)and look into some of the key pieces of the LifeCycle API.

The methods that we're going to look at are:

*   constructor

*   render

*   componentDidMount

*   componentDidUpdate

*   componentWillUnmount

Let's also compare where each of these methods belong within the react lifecycle by taking a look at [this diagram (Links to an external site.)](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/).

We will explore these in depth later on but for now, focus on warming up to the documentation and the idea that components have a lifecycle.





\---

\---

## Overview&#xA;&#xA;

In our last objective, we explored how state can be displayed and changed by passing state value and state modifying functions respectively through props. We explored this using the onChange eventlistener. That is, of course, only one of many user event you can integrate into your applications!

We have already seen how events are handled within React class components. We need an event handler function and we need to link it to an eventlistener method within our DOM.

Notice once again the need for that this object when referencing our event handler. Within class components, just like our props and state, our event handlers are bound to the instance of this class and are accessed through this.

We have also seen that "e" parameter before. This parameter is known is React as a synthetic event object. Inside this object, we will have access to various pieces of information regarding this event triggered, including the target DOM element, the type of event, and methods that control the propagation of that event like preventDefault. For more details on the synthetic event objects, check out the reference materials [here (Links to an external site.)](https://reactjs.org/docs/events.html).

Let's add in some functionality to our event handler.

Now, when we click on our button, we can actually print out our synthetic event object. We can now do anything we want within event handler, from triggering a change of state to starting an external api call.

## Follow Along

Now, let's build out a little Application that can handle some data that we pass through a few JSX elements. We're going to build out some event handler functions using the following event listeners:

*   onClick

*   onDoubleClick

*   onMouseEnter

*   OnChange

First, let's build out a singleClickHandler function.

Now, we add it to a button within our app's render function.

Lets repeat the process for our doubleClick, mouseEnter and onChange events.

Try playing around with the events and see how are interacting one with another.

Lets take a closer look at the input onChange event for a min. Let's pass in the synthetic event through the function body by adding it as a parameter to the event handler connected to it.

One of the most useful properties attached to synthetic events is target. This provides information on the text, value, style, attached attributes and other useful data within our DOM element. In this case we can print out our input's value.

Lets add in some state to get realtime feedback of what we are typing. Once again, we do this within class components by within the class constructor and make our app display that change.

Lets also update our change handler to update our state:

Excellent! Now, setState will update our display property on our state object by simply typing in the input field. Let's prove this by logging our state object inside the render function.

You can see a working copy of this example [here (Links to an external site.)](https://codesandbox.io/s/rmnj2r1o0p).



\---

\---

## Overview&#xA;&#xA;

Up until this point, our applications have been fairly simple. One or two components with a bit of state to allow for interaction. As our applications grow, so to do the complexity way components relate to each other. To do this, it helps to see our components as being structure in a parent / child relationship.

Here is an example of a more complicated application hierarchy.

![](https://drive.google.com/uc?id=1Ahn_s5WHHcJDD_t17eWAGOlIoX7ZTy4i)

Simple or complex, every application needs shared, persistent data to run.

Currently, we have been using state to hold that data. Unlike statically defined data within our component, state is persistent, changeable and can flow into other components through use of prop drilling. Changes to state immediately rerender the parts of our components effected by that change of state in a process called reactivity. When working with more complex component trees, state always runs from a parent component down to a child.

![](https://drive.google.com/uc?id=1fjz_nVILoUG0kr1m0jzfUtQAiKf\_-kga)

What if we want to modify that data? Well, just as we can pass parent state down through props, we can also pass functions that modify child state! Executing these functions in our child components will cause state to change at our parent level components, resulting in reactive rendering through out all our application!

![](https://drive.google.com/uc?id=1-xf6YVOb38HINlQOnBMhkYYXy8ypOP2u)

We have already seen how to pass state through props using functional components. Now, let's take a look at how we work with state in class based components.

## Follow Along

Consider the following component:

Let's create a sub component using functional components to hold our welcome message.

Now, lets refactor our component using React classes.

Notice that props are not passed in as they were in functional components. Instead, props are attached to the this object, just like state.

Great! We are sharing data between a component's state and a component's props. This means that when the state object changes, so too will the props.

Now let's add in the ability to modify that state. To do this we will need to:

*   Connect a state change method to an event listener in our child component.

*   Create the substance of that method in our parent.

*   Pass that method to the child through props.

Let's start at bottom, our child component. Let's say that we want use a form to dynamically update our message statement. This small component should do nicely:

The only problem is, we don't have access to state all the way down here! Let's build out our state changing method where it belongs, in App.js our parent. While we are at it, let's add our form component to our rendering so we can see it in the first place.

And there we go! We successfully passed our state data downstream through props in WelcomeBanner. At the same time, we can also successful pass data back upstream by executing state modifying functions passed through props in FormComponent.

## Challenge

Using the components we just created (App, FormComponent and MessageComponent), try building out a form that will allow a user to handle data. You'll need a button, input field, and some data-bound to a DOM element that displays what the user is submitting.

When a user clicks submit, show the data that's on state in an alert statement.

### Stretch 

Loop over a list of items showing those items to the screen. (Can be a list of strings). When a user clicks submit, instead of logging the item, push an item into that list, and watch the magic happen.

*   We're going to be updating some state on a parent component.

*   That state will be wired up to a few other components as we pass the props around.

*   We will also be passing around a few handler functions that help us update/delete our state.

Lets set up a form component that we can use to update our message component from above.

Now let's build a form component that can handle some data defined on state, below on the child components.

We're going to need to build out a change handler function on our App component that we can pass down to the form. We'll have to define the prop as updateStateMessage in order to make our onChange event handler work out properly.

## Challenge

Using the following tools:

*   Class component

*   functional FormComponent, MessageComponent

*   click, and change handlers

*   setState

Build out a form that will allow a user to handle data. You'll need a button, input field, and some data-bound to a DOM element that displays what the user is submitting.

When a user clicks submit, show the data that's on state in an alert statement.

**Stretch** Loop over a list of items showing those items to the screen. (Can be a list of strings). When a user clicks submit, instead of logging the item, push an item into that list, and watch the magic happen.



\---

\---

## Overview&#xA;&#xA;

React gave us the idea of components as independent pieces of UI. And thus far, you have learned how to build out functional components for use in making multiple DOM elements. Now, we're going to be learning about the React.Component base class that allows us to use some of the methods that the React team has curated to tap into what we call the Component Lifecycle. These methods (known as life cycle hooks *more on these to come*) give us control over how our components work, and if we'd like to use them, we have to build out a class component that extends the React.Component parent class. Any time you see a line of code that looks like the following, you're using the React.Component parent class, and you have the ability to tap into these methods.

By creating components as classes, you can set up a data object that your component is concerned with. This is done using state and setting up that object on our constructor method. Once we have some data that we can render out to the DOM, we need a vehicle that will allow us to render that data. This is achieved with the JSX method render() from within the life-cycle hook. We'll walk you through the steps below.

Declare your class component by extending the React.Component parent class. class FooComponent extends React.Component {}.
Use the constructor function to set up some state. *because we're calling extends, we also need to call super(); otherwise we won't have access the this*
We need to render some sort of UI to the DOM. We do this by calling the life-cycle method render.

I like to remember these steps by referencing one of my favorite bands: Creedence Clearwater Revival (CCR), which stands for class, constructor, and render/return.

1.  Declare your *class*, and extend the React.Component Base class.

<!---->

1.  Now we'll set up our *constructor* and add state.

<!---->

1.  *Render* some UI and *return* some JSX.

Our final component should look like this.

Now that we have constructed a skeleton for our Class component, it can be a bit more dynamic. The way we'll achieve this will be to use some data that we'll pre-define as some information we'd like our component to display. We'll then take that data and do this really cool thing called interpolation in order to present it to the DOM within some Text.

Components built out extending the Base React.Component class come with a bunch of benefits directly from the React API. A list of the benefits to what we get out of the Component class can be found [here (Links to an external site.)](https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate), in theReact documentation about class components. We will be discussing the life-cycle methods at another place in time, so don't worry too much about those for now.

For now, let's focus on a component caring about its own state (data) and managing that state in a reactive way. The state object that we set up on our constructor has a very React-specific way of doing things. It allows us to drive our UI using data. Again, think about Facebook here. You see a LOT of data and interact with it all of the time when you're using the Facebook app. Because of the way we work with social media today, we expect this data the UI to represent that data in close to real-time. This is one reason why React is really good and how reactivity can be achieved.

## Follow Along

Let's work together to build out a class component that prints a message to the screen using a few DOM elements. We will hold a message on state, and print that message to the screen by selecting it an assigning it to a DOM element. Then we will take it a step further and pass that message down to another component using props.

Go ahead and navigate over to [this Codesandbox (Links to an external site.)](https://codesandbox.io/s/3xwzql38nm), where we will write our React Code. CodeSandbox is an online editor that can be used to write React Code right away! I can't emphasize how cool this really is. For now, you'll just have to trust me.

You'll notice that we're getting an error on this page. As we begin to define our app class, elements will start to come to life on for us. For now, let's start by simply adding the class through CCR.

When you're done, your browser window should re-render without any errors. Your app class should look like this:

Now, let's add a property to our state data. Define a message property on the state object.

Now that we have the message on our component's state, we can use it through interpolation. In our render method, let's change the message inside of div to reference the state object. Remember the this keyword when pointing to an object on the Class constructor.

Hooray! You've now built your first class component, and you're ready to rock n' roll.

## Challenge

Let's take the functionality of this class component that we built earlier and extend it just a little bit. Declare a Functional Component called RenderMessage inside [this CodeSandbox (Links to an external site.)](https://codesandbox.io/s/103jkor46q).

*   Make sure you declare your Props Object that will be passed into this component.

*   Return a div who's child is props.message

*   Now inside of the App class pass in that RenderMessage component and pass down a message prop to RenderMessage. This message prop should be set equal to the message property on the state object.

*   Once it's all wired up properly you've done it!
