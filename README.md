# Polycircular Bindings

This is an attempt to describe an architecture using polycircular bindings.

**_What are polycircular bindings?_**

Polycircular bindings are derived by the term used in Biology. The principle behind Polycircular bindings are that an effect would trigger if an event is not persisted to an optimal state. 

**How this can be related to Computer Science** 

Asynchronous and Synchronous functions are widely used in Software right now. This means, that at some level, you would need to determine if you are going to use synchronous functions or the opposite at some point. It is pretty easy to have an non-blocking functions which will in the future malfunction. 

**Common traits about Polycircular Bindings**

- Ability to fractionalize other bindings ( I.E circular bindings ) 
- Alters and handles an side-effect if the argument(i.e pure function) is persisted

**Polycircular Bindings in Circular Events** 

Polycircular Bindings in Circular Events are rather ambigious. The end goal of an Circular Binding is to reference to an object at any level. Though this is troublesome in some contexts such as immutability, there should be a way to avoid object recreation in circular values. An Polycircular binding in Circular Events should work as trampolines. This would make sure the structural sharing always bounces back at its original state. 

**Polycircular Bindings in functions with side-effects** 

This is the main intent for Polycircular bindings. To handle some other function if the first one is not persisted. Over time, this means that side-effects would be slim to none. It also means that patterns using and having advantage of Infinity approaching functions, could be limited. Polyciruclar bindings are either "petrifying" the side-effect or making use of it, an extended description of this, I hope to add later. 

**Imaginary example** 

```js
const countreducer = (state= 10, action, ) => {...} // 10, 11 ,12 ,13 ,14, ... ∞
const polycircularBinding = (countreducer) => {...}
// 10,11,12,13,14... ∞
```

This is a bad example, but it is to express and illuminate on impure functions. Consider that `countreducer` did not return a new state and instead was an impure function (`state++`). An Polycircular Binding has the only the side-effect in mind. So if we were to supply the state modification as a second argument later ( se next section ), you'd get the required result. Now, let's put this in consideration. If we were to add the impure section, could we isolate it? 

**Another example**

```js
const countreducer = (state = 10, action) => // 10,11,12,13,14, ...∞
const polycircularBinding = (countreducer, sideEffect) => {...}
// 10,1,2, ...∞
```

This example has one simple fact. We aren't counting state anymore. This is due that our `polycircularBinding` is being binded. An polycircular binding stops once it has reached its original state. Similarly, with Circular Events, this would be the same,except it would stop once it reaches the self-reference.

**Gradiently Submissive Functions** 

```js
const countreducer = (state = 10, action) => // 10,9,8,7,6, ...∞
const polycircularBinding = (countreducer, sideEffect) => {...}
// 10,9,8,7,6,10,9,8,7,6 ...∞
```
(`state--`)
Taking the same example we've used, we can extend the usage of the Polycircular Binding. If it is persited at start, but goes towards not being updated, it should always bounce back to the side-effect. This is, so we could handle the circular reference properly. This might seem like an bad example again, but we can use this in structural sharing. If we were to do this, we could bounce it back to the self-reference. If this were circular references, we could patch each Polycircular Binding.


**Additional Notes** 

This is not yet to be tested and accomplished. I hope we could try to work this out, and experiment around similar experiments. About immutability: We should try to make structural sharing work with circular references as well, as this is the end goal for these experiments. 
