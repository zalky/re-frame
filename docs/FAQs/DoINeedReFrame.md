### Question

Reagent looks terrific.  Why do I need re-frame?  It looks like extra layers and
conceptual overhead for not much benefit!

### Answer 

Yes, Reagent is terrific. If your application is small and simple, 
then standalone Reagent is absolutely a fine choice.

But it only supplies the V part of the MVC triad. As your application 
gets bigger and more complicated, you'll need to find solutions to 
questions in the M and C realms. 
Questions like "where do I put control logic?".
And, "how do I manage state?".  
And, How should new websocket packets be communicated with the broader app? Or GET failures? 
"How do I put up a spinner
when waiting for CPU intensive computations to run, while allowing the user to press Cancel?"
How do I ensure efficient view updates?  How do I write my control logic in a way that's testable? 

These questions accumulate. 

Reagent, by itself, provides little guidance and, so, you'll need to
design own solutions. Your choices will also accumulate and,
over time, will become baked into your codebase.

Now, any decision which is hard to revisit later is an architectural decision - 
"hard to change later" is pretty much the definition of "architecture".  So, 
as you proceed, baking your decisions into your codebase, you will be 
incrementally growing an architecture.

So, then, the question becomes: is your architecture better than re-frame's?  Because 
that's what re-frame gives you ... an architecture ... answers to the
various challenges you'll face when developing your app.

Now, in response, some will enthusiastically say "yes, I want to grow my own 
architecture. I like mine!". Fair enough - its a fun ride!

The problems arise ONLY when this process is not conscious and purposeful. You 
can accelerate quickly with Reagent and get a bunch of enjoyable early wins, but then
ultimately end up off the road, in the paddock, because of the twists and turns 
leading up to a bigger application.

I've had many people (20?) privately say to me that's what happened to them. The real
number would obviously be much higher. And that's pretty much the reason for
this FAQ - this happens a bit too often.

So, my advice is ... if your application is a little more complicated,
be sure to make a conscious choice around architecture. Don't think 
"Reagent is all I need", because it isn't. One way or
another you'll be using "Reagent + a broader architecture".

### Some Choices Made By re-frame

1. Events are cardinal. Nothing happens without an event. 
2. Events are data  (which means they are loggable, and can be queued, etc)
3. Events are handled async  (A critical decision. Engineered to avoid core.async problems!)
4. For efficiency, subscriptions (reactions) should be layered and de-duplicated
5. Views are never imperative or side effecting (best effort)
6. Unidirectional data flow only, ever
7. Interceptors over middleware. Provide cross cutting concerns like logging and debugging. 
8. Event handlers capture control and contain key code. Ensure purity via coeffects and effects. 
9. State is stored in one place and is committed-to transactionally, never piecemeal.

Hmm. I feel like I'm missing a couple, but that's certainly an indicative list.

re-frame is only about 500 lines of code.  So it's value is much more in the honed 
choices it embodies (and documents), than the code it provides.

### What Reagent Does Provide

Above I said:
> Reagent, by itself, provides little guidance ...

which is true but, it does provide useful building blocks. If you do want to create 
your own architecture, then be sure to check out Reagent's `track`, `reaction` and `rswap`. 

There's also other Reagent-based architectures like [keechma](https://github.com/keechma/keechma) and 
[carry](https://github.com/metametadata/carry) which make different choices - ones which may 
better suit your needs.

***

Up:  [FAQ Index](README.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- END doctoc generated TOC please keep comment here to allow auto update -->
