---
title: About
date: '2018-02-22T17:01:34+07:00'
---
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
