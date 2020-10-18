# Architecture

## Intro
React and React Native projects themselves, and the community already gives us enough 
waypoints when it comes to architecting our projects. From the way we use components 
to the way we use dependencies and a lot more. To keep this documentation nimble, 
instead of going through specific steps of creating a project and implementing an 
architecture, we will go over React and React Native features, language preferences 
and the tools we use that shape our architecture.

Unless necessary, this chapter will not go into detail on the preferences that make up 
the architecture. There are lots of amazing people who can explain these preferences 
much better, repeating or copy pasting their words would be both a waste of time and 
disservice to their work. So please check all the shared resources thoroughly, and 
research more on your own if the resources provided are not enough, or you feel that they 
are not compatible with your current level of understanding.

## Language Preferences

We use TypeScript, because we want to suffer less by making the complier help us.

Resources:

[Typescript vs Javascript by Ben Award](https://www.youtube.com/watch?v=D6or2gdrHRE)

Q:
Wait! I don't know TypeScript and never used it before, what am I gonna do?

A:
Don't worry, just check some tutorials, start getting your hands dirty, and know 
that your RN department teammates are always ready to help.

## Components and Local State Management Preferences

We use Functional Components and hooks.

What is `Local State`?

Local state can be considered as any state that is specific to a single component 
and is not required to be shared across the application. The state of a smaller component
in a bigger component (like a screen component (i.e. Settings), which has a button component 
(i.e. Logout) that has isDisabled prop that is stored in Settings component) 
can be also considered as local state, as long as we don't have to pass
the props multiple levels down.

Basic examples could be (let's imagine these are in useState hooks in a functional component):

`[email, setEmail], [password, setPassword], [isLoginButtonActive, setIsLoginButtonActive]` in a login component.

`[isProfileDetailHidden, setIsProfileDetailHidden]` in a Profile component.

Resources:

[Using React Hooks vs. Class Components by Ben Award](https://www.youtube.com/watch?v=vbaIZ3xMj9U)

[React Function Components by Robin Wieruch](https://www.robinwieruch.de/react-function-component)

[When to break up a component into multiple components](https://kentcdodds.com/blog/when-to-break-up-a-component-into-multiple-components)

## Navigation

We use [React Native Navigation](https://github.com/wix/react-native-navigation). 
Our main reasoning is its performance compared to [React Navigation](https://reactnavigation.org/).

## Global State Management Preferences

We use [Redux](https://redux.js.org/introduction/getting-started) with 
[hooks](https://react-redux.js.org/api/hooks), and [reselect](https://github.com/reduxjs/reselect) 
library for complex selections.

We use [Redux Thunk](https://github.com/reduxjs/redux-thunk) to write async 
logic that interacts with the store.

What is global state and why do I need it?

Let's think our app as a top down tree, and each component user can navigate to and access 
is a node on the branches of this tree. If we only had our state on top of 
the tree that starts the application, we would have to pass all information 
we need from one component to another, one by one.

Above model in mind, let's think that we need to pass User object to both 
Home component and Settings component. In our current state usage, we are 
passing these as props to each component. Then probably also to their 
(Home and Settings component) child components.

As you might imagine, or maybe already experienced, all this props drilling 
can be a pain in the ass. To fix this, we can use a global state management tool, 
and have the data that needs to be read/written by multiple places in the global state, 
and then use hooks to access/modify the data.

## Server State Management Preferences

We use [React Query](https://github.com/tannerlinsley/react-query) to manage the server state.

You might be asking yourself "What does this title even mean?". To answer that question, 
please take 30 minutes and [watch this video](https://www.youtube.com/watch?v=seU46c6Jz7E), 
I promise it will be worth your time. It will let you achieve more with much less code.

To give a very short summary, putting all of the logic related to your server state in your global state
management tool can (or let's be more honest, CERTAINLY WILL) make your life a boilerplate 
hell and result in a lot of code that needs to be maintained. 

React Query helps with this by giving you an amazing tool to `fetch, cache and update 
data in your React and React Native applications all without touching any "global state"`.

Resources:

[Quick start docs](https://react-query.tanstack.com/docs/quick-start)

# To be continued with:

## Handling Form State Management 
(can be considered as a point under Local State Management)

## Localization

## Testing
