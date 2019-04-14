# Webreflection ecosystem

Some notes trying to pick apart and understand the webreflection ecosystem.

- [lit-html vs hyperHTML vs ligherhtml](https://medium.com/@WebReflection/lit-html-vs-hyperhtml-vs-lighterhtml-c084abfe1285): - lit is google.  hyperHTML is bigger and more compatable.  ligther is the next iteratino of hyperHTML... sort of.

- 3rd party walkthough of hyper: https://medium.com/easy-apps-with-hyperhtml/easy-apps-with-hyperhtml-1-4a56acad9327


## Module relationships

- [HyperHTML](https://github.com/WebReflection/hyperHTML) - browser implementation.  Older more robust.
- [ViperHTML](https://viperhtml.js.org/viper.html) - Node.js rendering engine for HyperHTML
- [lighterhtml](https://github.com/WebReflection/lighterhtml) - The newer version of hyperhtml
  - [neverland](https://github.com/WebReflection/neverland) - React hooks for ligher. Component state, insertions + updates (effects), dom reference.  Closure based components.
  - [Haunted](https://github.com/matthewp/haunted) - neverland for hyper / lit.  Basically neverland but for the other ecosystems.
- [HyperHTML Element](https://github.com/WebReflection/hyperHTML-Element) - Custom Elements based components for hyper.
- [regular-elements](https://github.com/WebReflection/regular-elements) - Component system, but attatches via CSS selectors.  Does not use custom elements.
- [wicked-elements](https://github.com/WebReflection/wicked-elements) - The same as regular elements but more.  I can't tell what the difference is.  See https://medium.com/@WebReflection/a-wicked-custom-elements-alternative-6d1504b5857f


## Submodules

These are the submodules that are used underneatht the main abstractions:

- [augmentor](https://github.com/WebReflection/augmentor): Generalized hooks implementation
- [dom-augmentor](https://github.com/webreflection/dom-augmentor): hooks implementation with browser `connected and disconnected` events.
- [disconnected](https://github.com/WebReflection/disconnected/): webreflections onload like module.  Provides `connected and disconnected` events with MutationObservers.  Uses CustomEvents which is interesting.
- [domdiff](https://github.com/WebReflection/domdiff): dom diffing algorithm.
- [attributechanged](https://github.com/WebReflection/attributechanged): Lets you update components when their 'attributechanged`.

## Ecosystem

- [hyperhtml-app](https://github.com/WebReflection/hyperhtml-app) router

## Interesting ideas

### Wiring

This ecosystem has the concept of a wire.  Whats a wire?  Good question, I knew at one point but then forgot because the name is rather nondescript, and I didn't get enough hands on time to really commit to memory..  "The persistent fragment like class used in hyperHTML."

- [hyperhtml-wire](https://github.com/WebReflection/hyperhtml-wire):  module version of wiring.

### Frozen template literal chunks

- [under the hood](https://viperhtml.js.org/hyperhtml/documentation/#introduction-1)

> If you have a generic function and place it in front of a template literal without invoking it, the function will be executed receiving an Array as its first argument which will contain the list of chunks between interpolations, the rest of the arguments will contain the interpolated values.

> Not only is the function invoked, its first parameter will be a frozen, unique, Array. In this way, even if a template generates different strings due to changed interpolated values, its chunks will always be the same.

> This native feature, even reflected when transpiled via Babel, is key to generating a DOM structure and parsing it once, creating a unique relationship between a template literal and a DOM template.

> What hyperHTML adds on top of this feature is a context to operate in, like a context you could use for any generic function or method call.

What this means (untested):  If your template doesn't change, updating the the context only costs the interpolated values calculaton + ...updating them.  (Diffing? SOmething else?)  AKA "smart DOM content".

> While using hyper`<p>runtime</p>` for one-off operations just works, binding a DOM node to create its own content or weakly relating generic objects are the best way to recycle the DOM and obtain best performance.


I think it works like this:

- When you 'wire' a template to an object, when it renders the dom node the first time, it weak maps the object to the dom node, unless that object is already weak mapped to an existing dom node.  Ok... say its already rendered.  What if the data changes?  Is it re-rendered?

Wiring a template lets you associate it with a rendered node.  How does it know if its needs updating or not though?

https://medium.com/easy-apps-with-hyperhtml/easy-apps-with-hyperhtml-2-1d60fd41bb67
