# Mobx State Tree

[mobxjs/mobx-state-tree](https://github.com/mobxjs/mobx-state-tree)

> Mobx-State-Tree is an opinionated library that imposes a strict architecture on state organization.

> State is stored in an immutable, structurally shared tree.

> Business logic removed from the UI (views are passive) (decouple domain logic and stare from UI)
> Provides a structure for communication  
> Embrace composition and reactivity  
> Relay on the computed properties not on the model
> Subscribe to all the path streams (patches)
> Replay and record snapshots, patches and actions
> Protection against uncoordinated modifications
> Protection against stale reads
> Runtime type checking and inferred TypeScript static type checks, design time type checking

> A good model makes it easier to deal with reality

> State is not just data but identities and relations
> Separates consumption of data and changing of state

> Everything that can be derived from state should be derived. Automatically

> Break into smaller components if not fast enough

> With observable data we know _what changed_ and _where it is relevant_ resulting in code
> which is straight forward to read and write, smart optimized rendering and easy separation of concerns

> State requires mutability - it's impossible to build a meaningful application without mutability
> Control mutability and side-effects in an organized way (state management)

> Observable objects are as a collection of streams, one stream per property

> Use hooks for local state (if it's not needed anywhere outside the component)

Mobx is like a spreadsheet

- _Observables_ - spreadsheet's data cells that have values (state than can be changed over time)
- _Actions_ - the act of changing the values of spreadsheet's data cells (interactions that change state)
- _Computed Values_ - formulas and charts that can be derived from the data cells and other formulas (values that can be derived)
- _Reactions_ - drawing the output of a data cell or a formula (side effects that should respond to state changes)

`observer` - turn components into reactive components
`inject` - connects components to provided stores

## Mobx compared to Angular/Vue/Knockout

Independent solution (use with anything)
Distinct concepts: Side effect and derived values
No change detection but change propagation
Synchronous scheduling (helps with debugging)
Optimally sorted dependency tree for guaranteed glitch-free, minimal amount of computations

## Tree

A node can exist only once in a Tree
Any node in a Tree is a Tree itself
All leaves in the Tree must be serializable
Every change to a model correspond to a snapshot and a patch

Tree consists of 2 thing:

- state (contents)
- shape (type)

```js
const Type = types.model(properties, actions);
const instance = Type.create(snapshot);
instance.someAction();

const snapshot = getSnapshot(instance);
```

```js
const Book = types.model(
  {
    title: types.string,
    price: types.number,
  },
  {
    setPrice(newPrice) {
      this.price = newPrice;
    },
  }
);

const Store = types.model({
  books: types.array(Book),
});

const store = Store.create({
  books: [
    {
      title: "Some Title",
      price: 29.99,
    },
  ],
});

store.books[0].setPrice(99.99);

//composing types
store.books.push(Book.create({ title: "Some Title" }));
store.books.push({ title: "Some Title" });

//references

const cartEntry = types.model({
  amount: types.number,
  book: types.reference(Book), //it's not a Book, it's just a reference
});

cartEntry.book = bookStore.books[0]; //normalization done behind the scenes  and reference management
```

![Feature Comparison](mobx/features-comparison-2.jpg)

## Stores

One root store - can preform actions on everything at once, DI is shared

Multiple root stores - easier to reason by Domain (isolation), can't easily preform actions on everything, DI isn't shared

### Store Communication

> Each Store access directly other Stores `getParent(self).someStore` - each store knows the whole structure
> Actions wrapper - calls directly other Stores, knows the whole structure
> Dependency Injection - injecting stores into one another, can be used for both Actions and Views

```js
const firstStore = FirstStore.Create({});
const secondStore = SecondStore.Create({ someProperty: "Foo" }, { firstStore });
```

### Store Composition

> When data is the same but the behavior is different

`const thirdStore = types.compose(FirstStore, SecondStore);`

- separation of concerns
- reusability

# Actions

> instances can only be modified through actions  
> actions can only modify own subtree

```js
store.books[0].price = 99.99; //Error cannot modify the object is protected
```

> Method invocation produces action description

```js
//MST is fully recursive concept, every node in the tree is state tree in it self and any operation in the tree can be invoked on a node
const bookCopy = clone(store.books[0]);
const recorded = recordActions(bookCopy);

recorder.replay(store.books[0]); //atomic commit of all the changes the user made
```

# Environment

```js
import { getEnv } from "mobx-state-tree";
```

# Comparison

React Context - single event per context  
Redux - global event, but selecting relevant parts  
MobX - event per property, selection is automatic (subscribed to each individual property)

React state - component
Redux - single store
MobX - user defined objects/classes

> Both Redux and MobX have decouple state from UI layer

> Most bugs happen because poor references management - staleness bugs (store id reference not the object reference, identity or value)

# How does MobX works

- Wrap properties with getter and setter - tracks every interaction with an object
- Store running function in a stack
- Getters register observers
- Setters notify observers
- MobX optimizes dependency graph (small as possible, least amount of computations)

> Transparent reactive programming

- decoupling of producers and consumers of information
- straightforward to write
- optimized, minimal dependency tree

# React but for Data

> Both React and MST are contract based (only props, views and actions are exposed, internal state encapsulated, design and runtime type checking)

Component - Type (React composes _Components_, Mobx composes _Types_)

```js
const House = () => (
  <Door />
  <Window>
)

const House = types.mode({
  doors: Door,
  windows: Window
})
```

Props - Snapshot

State - Volatile state

Instance - Instance (React composes a tree of component instances, Mobx composes a tree of rich type instances)

```js
const instance = React.createElement(Component, props);
const instance = Type.create(snapshot);
```

Context - Environment

Reconciliation - Reconciliation (preserve internal state, performance)

> Snapshots are immutable, structurally shared representation of entire state at a specific moment in time (GIT Commit)

> JSON Patch - deltas describing updates that were applied to the tree (Git Patch, describes modifications from one commit to the next) (used for time travelling like Git Revert, Git Rebase)

> Middleware - intercept action invocations (Git hook)

# Asynchronous processes in MST

Built in concept based on generators so middleware can run on every continuation

```js
//same semantics, slightly difference syntax
async function - process(function*)
```

```js
//same semantics, slightly difference syntax
await -yield;
```

## Talks

### Next generation state management - Michel Weststrate aka @mweststrate at @ReactEurope 2017

[![Next generation state management](https://img.youtube.com/vi/rwqwwn_46kA/0.jpg)](https://www.youtube.com/watch?v=rwqwwn_46kA)

### You don’t know MobX State Tree | Max Gallo | iJS London 2018

[![ You don’t know MobX State Tree](https://img.youtube.com/vi/LKyCJB27oNM/0.jpg)](https://www.youtube.com/watch?v=LKyCJB27oNM)

### Introduction to MobX State Tree

[![Introduction to MobX State Tree](https://img.youtube.com/vi/pPgOrecfcg4/0.jpg)](https://www.youtube.com/watch?v=pPgOrecfcg4)

### Michel Weststrate: React, But For Data — ReactNext 2017

[![Michel Weststrate: React, But For Data — ReactNext 2017](https://img.youtube.com/vi/xfC_xEA8Z1M/0.jpg)](https://www.youtube.com/watch?v=xfC_xEA8Z1M)

### Combining GraphQL + mobx-state-tree - Michel Weststrate (@mweststrate) @ReactEurope 2019

[![Combining GraphQL + mobx-state-tree - Michel Weststrate (@mweststrate) @ReactEurope 2019](https://img.youtube.com/vi/Sq2M00vghqY/0.jpg)](https://www.youtube.com/watch?v=Sq2M00vghqY)

### MobX State Tree React pure reactivity served - Luca Mezzalira

[![MobX State Tree React pure reactivity served](https://img.youtube.com/vi/HS9revHrNRI/0.jpg)](https://www.youtube.com/watch?v=HS9revHrNRI)

### Chain React 2019 - Devlin Duldulao - Getting Started with Mobx State Tree

[![Devlin Duldulao - Getting Started with Mobx Statetree](https://img.youtube.com/vi/jD6iCt-Qz5k/0.jpg)](https://www.youtube.com/watch?v=jD6iCt-Qz5k)

### React Native EU 2019: Jamon Holmgren — Resolving the great state debate

[![React Native EU 2019: Jamon Holmgren — Resolving the great state debate](https://img.youtube.com/vi/Wx9slbOTD6Q/0.jpg)](https://www.youtube.com/watch?v=Wx9slbOTD6Q)

### Michel Weststrate — State management beyond the libraries

[![Michel Weststrate — State management beyond the libraries](https://img.youtube.com/vi/JKaJ9r3xYN4/0.jpg)](https://www.youtube.com/watch?v=JKaJ9r3xYN4)

### ReactiveConf 2018 - Michel Weststrate: State management beyond the libraries

[![ReactiveConf 2018 - Michel Weststrate: State management beyond the libraries](https://img.youtube.com/vi/N2mSG28jADQ/0.jpg)](https://www.youtube.com/watch?v=N2mSG28jADQ)

### MobX - Statement Management with no Boilerplate - React Native London - March 2020

[![MobX - Statement Management with no Boilerplate ](https://img.youtube.com/vi/3Gt-Cxjld3g/0.jpg)](https://www.youtube.com/watch?v=3Gt-Cxjld3g)

### MobX, or: Going from Mutable to Immutable to Reactive State Management - Michel Weststrate - CityJS

[![MobX, or: Going from Mutable to Immutable to Reactive State Management](https://img.youtube.com/vi/ZHxFrbK3VB0/0.jpg)](https://www.youtube.com/watch?v=ZHxFrbK3VB0)

### Michel Weststrate: MobX: The Quest For Immer Mutable State Management

[![MobX: The Quest For Immer Mutable State Management](https://img.youtube.com/vi/ta8QKmNRXZM/0.jpg)](https://www.youtube.com/watch?v=ta8QKmNRXZM)

### Michel Weststrate — MobX and the unique symbiosis of predictability and speed

[![Michel Weststrate — MobX and the unique symbiosis of predictability and speed](https://img.youtube.com/vi/NBYbBbjZeX4/0.jpg)](https://www.youtube.com/watch?v=NBYbBbjZeX4)

### Michel Weststrate - Modern React and the case for Reactive State Management

[![Michel Weststrate - Modern React and the case for Reactive State Management](https://img.youtube.com/vi/hHF33WGqQ5U/0.jpg)](https://www.youtube.com/watch?v=hHF33WGqQ5U)

### Mattia Manzati - Advanced Types in TypeScript

[![Mattia Manzati - Advanced Types in TypeScript](https://img.youtube.com/vi/dmBxWgVwJqs/0.jpg)](https://www.youtube.com/watch?v=dmBxWgVwJqs)

### Flutter Reactive State Management With MOBX | Flutter Stream Day Season 1

[![Flutter Reactive State Management With MOBX | Flutter Stream Day Season 1](https://img.youtube.com/vi/JYOBORVtJ50/0.jpg)](https://www.youtube.com/watch?v=JYOBORVtJ50)

### Max Gallo - Reinventing MobX

[![Max Gallo - Reinventing MobX](https://img.youtube.com/vi/P_WqKZxpX8g/0.jpg)](https://www.youtube.com/watch?v=P_WqKZxpX8g)

### Advanced state management patterns with JavaScript & MobX with Michel Weststrate

[![Advanced state management patterns with JavaScript & MobX with Michel Weststrate](https://img.youtube.com/vi/uWIT9M95mqQ/0.jpg)](https://www.youtube.com/watch?v=uWIT9M95mqQ)

### Michel Weststrate: Real World MobX — ReactNext 2016

[![Michel Weststrate: Real World MobX — ReactNext 2016](https://img.youtube.com/vi/Aws40KOx90U/0.jpg)](https://www.youtube.com/watch?v=Aws40KOx90U)

### React Amsterdam Autumn Meetup: MobX and Large Scale React Applications

[![React Amsterdam Autumn Meetup: MobX and Large Scale React Applications](https://img.youtube.com/vi/etnPDw5PKqg/0.jpg)](https://www.youtube.com/watch?v=etnPDw5PKqg)

### Spreadsheets with MobX and react-virtualized

[![Spreadsheets with MobX and react-virtualized](https://img.youtube.com/vi/VVLSzpxq_KU/0.jpg)](https://www.youtube.com/watch?v=VVLSzpxq_KU)

# Courses

[Manage Application State with Mobx-state-tree](https://egghead.io/courses/manage-application-state-with-mobx-state-tree)

[Manage Complex State in React Apps with MobX](https://egghead.io/courses/manage-complex-state-in-react-apps-with-mobx)

[Immutable JavaScript Data Structures with Immer](https://egghead.io/courses/immutable-javascript-data-structures-with-immer)

_How do I work with state in React?_  
[![How do I work with state in React?](https://img.youtube.com/vi/x-ioxWvuZMg/0.jpg)](https://www.youtube.com/watch?v=x-ioxWvuZMg)

_What is MobX-State-Tree and how can it help me with React?_  
[![What is MobX-State-Tree and how can it help me with React?](https://img.youtube.com/vi/eQGwNIYXELI/0.jpg)](https://www.youtube.com/watch?v=eQGwNIYXELI)

_How do I get started with MobX-State-Tree and React?_  
[![How do I get started with MobX-State-Tree and React?](https://img.youtube.com/vi/Dxhd5uawayk/0.jpg)](https://www.youtube.com/watch?v=Dxhd5uawayk)

_How do I modify state values in React with MobX-State-Tree?_  
[![How do I modify state values in React with MobX-State-Tree?](https://img.youtube.com/vi/FdhWx18qm5g/0.jpg)](https://www.youtube.com/watch?v=FdhWx18qm5g)

_How do I create views with MobX-State-Tree?_  
[![How do I create views with MobX-State-Tree?](https://img.youtube.com/vi/sC3rbp6iBbQ/0.jpg)](https://www.youtube.com/watch?v=sC3rbp6iBbQ)

# Blogs

[The Curious Case of Mobx State Tree](https://codeburst.io/the-curious-case-of-mobx-state-tree-7b4e22d461f)

[Why Infinite Red uses MobX-State-Tree instead of Redux](https://shift.infinite.red/why-infinite-red-uses-mobx-state-tree-instead-of-redux-d6c1407dead)

[Understanding MobX and MobX State Tree](https://medium.com/game-development-stuff/understanding-mobx-and-mobx-state-tree-7bd37f734789)

[State Management with MobX State Tree](https://medium.com/react-native-training/state-management-with-mobx-state-tree-373f9f2dc68a)

# mst-gql

[https://github.com/mobxjs/mst-gql](mst-gql)

> Bindings for mobx-state-tree and GraphQL
> Run scaffolding in your CI/CD against production endpoint to verify readiness

```bash
yarn mst-gql --format ts http://localhost:4000/graphql
```

[![Combining GraphQL + mobx-state-tree](https://img.youtube.com/vi/Sq2M00vghqY/0.jpg)](https://www.youtube.com/watch?v=Sq2M00vghqY)

> Stop defending all the choices you don't make. "Didn't try" is fine.
> You have to learn to be able to use, but, you don't have to use to be able to learn. (read a bit, grab an idea, software engineering is all about patterns)
