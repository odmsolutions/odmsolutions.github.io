---
layout: post
title: "The Man In The Pub | Buying Beers and Overreaching"
tags: [code, abstraction, modular code, clean interfaces, beer, encapsulation]
---

![Buying Beers](/galleries/2010-07-01-an-object-oriented-story-the-man-in-the-pub/buying_beer.png){: style="float:left; padding-right: 4px"}

# I Like Beer

I enjoy drinking it, and in a pub that is pleasant, and not crammed, it can also be nice buying it.

Let me tell you a story, which starts with a man going into a bar...

A man goes into a bar. He wants to buy a drink. He has money to pay for that drink.
He does not own the bar. He is not a barkeeper. He is not involved in the beer industry at all, apart from consuming it. He may have a discerning taste for beer he likes and may be able to make bearable homebrew, but he'd prefer to buy beer and drink that.

This story can go a few ways...

# Story One: Serving Yourself - The Bar With No barkeeper

The man goes to the bar. There is no barkeeper present.

He eyes up the beer pumps and then consults a price list. He checks his wallet to see what he can afford and chooses a beer.
He then selects a glass from the shelf of glasses behind the bar, and if there are not enough clean glasses on the shelf, looks in the dishwasher to see if there are any there, and if that is empty, goes to collect an empty glass from a table and then cleans it.

The man then starts to fill his beer (badly - he doesn't know how to pull a good beer), but the pump runs part dry, so he must now go down to the cellar and somehow change the barrel (at this point he may injure himself, break something or put the wrong barrel in).

He may now find that there are no barrels of that particular beer, in which case he can choose another beer (oops wasted half a beer - spillage or drink it?), and rewash the glass (or get another), and start on another beer, or put an order to a brewery in to get more beer.

Finally, his beer is pulled and settling, and its time to pay. The man takes the amount he should pay (or may choose not to, or pay less - who is to say this guy can be trusted?). He then types his beer purchase into the till (which takes a while - these can be quite complicated), the till opens, and he puts in his money and takes his change (if he is trustworthy).

He drinks his beer - and leaves.

In reality, you'd probably call for attention and leave when nobody appeared. Or looters would have drunk the pumps dry and stolen the till contents. No bar in their right mind would operate this way. It is not hard to see how wrong this is. The man is exposed to far more than he wants or should be.

# Story Two: The Overreaching Bar

A man goes into a pub for a beer. The barkeeper asks him for his full personal details and birth certificate and chooses a beer. The barkeeper pulls the beer.

The barkeeper now reaches over, takes the man's wallet from his jacket, then the appropriate money out of the man's wallet, and puts the change back in his wallet.

The barkeeper now proceeds to hold the glass and tip it for the man to drink from. 
All this time, the barkeeper is unable to serve another customer, and the man is not much able to control the choice, flow, or cost of the flow of beer. 
The barkeeper is unable to speak to another customer, and we dread to think what happens if the man needs the bathroom.

It is not a particularly great experience for man or barkeeper, although the barkeeper knows far more about the man than they need to, including the content of his wallet. 
The man seems to have little choice, perhaps a really good barkeeper can choose a great drink, maybe not.

# Story Three: How you or I'd expect it to work

A man goes into a bar. A barkeeper is present.

The man probably has an idea of the content of his wallet.  He looks over the available beers and may already know his favourite beers. If he cannot see one he knows, he perhaps asks the barkeeper for a suggestion (which the barkeeper may or may not be able to give). 

He asks the barkeeper for a beer. The barkeeper tells him if the beer is available or not, and if so, pulls his beer. The barkeeper tells the customer the price, the man pays, takes his beer, and drinks it.

In this version of the story - neither the man nor the barkeeper need to know too much about the state of each other's business. The barkeeper does not need to know the man's wallet contents or age. The barkeeper doesn't choose a beer, although he could make a suggestion if asked.

The man simply asks for the beer, and the barkeeper provides it. All the business about barrels, cellars, till operation, ordering new barrels, knowing where clean glasses are (etc...) are things the punter buying the beer does not need to know or care about - to him, beer is available or not.

The arrangement is much simpler than both of the alternatives. The man gets his beer sooner. The barkeeper is free to serve the next customer faster. 

There is probably even the right atmosphere for a chat at the bar...

# Applying this to the design of systems

When you design your systems and write your code, try to keep this interaction in mind. Have you overreached? Is your object doing things that it should not? Why provide a bar (which is kind of useful) without a barkeeper to operate it? Why have a barkeeper who pours beer down the customer's throat?

A good object-oriented paradigm should be built like a service you'd happily use again. Thinking in the right way about your objects, or API's or even just a few functions in a header can make all the difference between complicated hard-to-maintain code, and simple, elegant code.

It may take a bit more thought and a little more domain understanding of each object to get it right. But interfaces will save a lot of time ultimately because there will be less duplication and less time needed to go and find how somebody interacts with an object.

I've expressed in a story a helpful paradigm for good code design and also some stories to show how it would be bad too. I keep these stories in mind when I write programs. I think if my code is overreaching, or expecting too much of the systems using its API.

Now, if it is your tipple, go reward yourself with a beer...

# Related content

## [The Lazy Programmer](http://www.youtube.com/watch?v=eL5o4PFuxTY)

This video shows how the best kind of programmer is a lazy one. They are lazy by employing good abstractions and knowing the right level of responsibility for classes. By avoiding overreaching and being clear where your boundaries lie, you will promote cleaner code, with fewer bugs and fewer security issues.

# A Code example - Coding for beers: A Bar Object

Yay - coding for beers - sounds excellent. Well, kind of - I am going to give a reasonable idea of what the public API for a pub bar to a customer would look like.

    class Bar {
        public List whatBeersDoYouHave();
        public beer buyABeer(beerSelector customerChoice, Payment payment);
    }
    
The whatBeerDoYouHave method returns a list of beerInfo objects. Each beer has a name, image, price and description. The customer has enough information to choose a beer.
    
The buyABeer method is where the customer makes the transaction. The beerSelector represents the beer they've chosen, and can be set up with the name of a beer, "that one over there" or "your best bitter please." The payment represents a method of getting the right money from the customer - could be cash or a card, etc. Payment could be used by the Bar to nicely wrap up the money handed over, the return of change, the handing over of a card, typing a pin, etc.

The API provided here to a punter says nothing about barrels or warehouses - it assumes that the bar will handle messy details, so the list given is correct. Ordering a beer with a problem may simply throw an exception (OutOfBeerError anyone?).

This concept is portable to many languages, not just the explicitly Object-Oriented ones. Designing your APIs and headers in C like this makes it easier to maintain, improve, and integrate with just as much as in Python, Java, or C#.
