# Flux

## What is Flux?

Flux is an *architecture* developed by Facebook for frontend webapps.  It provides a logical - unidirectional data flow.

The flow of data in Flux follows the below diagram:

![alt text](https://facebook.github.io/react/img/blog/flux-diagram.png "Flux")

The core of Flux are the React Component Views, the Dispatcher, and Data Stores.

A store is an object with functions that expose a resource.  It provides access to our models and has methods to add and remove models.  Stores are *singletons*.

The dispatcher is also a *singleton* object.  It holds callbacks and triggers them when an action occurs.  Actions change stores.  All actions, at the very least, must have an `actionType`, which informs the Stores what kind of action is being dispatched.  The store is notified and can decide how to react to this message - including ignoring it.

When a store changes, it should emit an event so that all views that depend on the stores contents can update themselves.  Views listen to tevents emitted by stores.

## More Specifically:

### Dispatcher

#### Overview

The central information hub. A singleton object.  Stores callbacks from **stores** so it can notify them when **actions** are triggered.

#### Users

**Actions** create objects that are *dispatched* through the dispatcher.

#### Observers

**Stores** receive all objects (sometimes known as actions) that are dispatched through the dispatcher.  It is up to the individual stores to decide what to do with the payload.

### Stores

#### Overview

Hold resources and provide functionality for reading. If your application is about managing todo's, you will likely have a `TodoStore` which holds all the actual todo items. Implemented as singletons.

#### Users

Data can be **read** by views, but **NOT** written. The only component that has any right to change a store's contents is the **Dispatcher** when an **action** has been dispatched through it.

#### Observers

When a store changes, it should `emit` an event. Views will register event listeners on these events so they will be notified when the contents change and can get the latest data.

### Views

#### Overview

Usually React components.

#### Users

Users interact with views. Events `emit`ted from **stores** cause views' properties/state to be updated.

#### Observers

User interaction can cause **actions** to be triggered.

### Actions

#### Overview

Used to prepare objects to be **dispatched**. Also used for communicating with web APIs.

#### Users

Can be triggered by **views** or API callbacks.

#### Observers

The **dispatcher** is...dispatched as part of an action.

## Resources

- [Facebook Docs](https://facebook.github.io/flux/)
