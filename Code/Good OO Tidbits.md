### Avoid Globals

Global references introduce the strongest of couplings, naming a specific thing. Eliminates abstraction and things like polymorphism and generalization.

#### Class references and Singletons

**Don't: access a Class static**

```java
Foo.doSomething()
```

**Do inject an Object implementing an Interface**

```java
//Inject a Foo instance reference, where Foo is an interface
buzLogicMethod(Foo fooer, ...) { fooer.doSomething(); }
```

**Use a "Factory" class (injected) instead of a Singleton pattern**

```java
// NO!  fooer = Foo.getInstance(id);
// YES!
fooer = fooFact.forId(id);
```

#### Accessors and Tell Don't Ask

```java
// NO!
Glass glass = bartender.getCleanGlass(); // Give me something I shouldn't have
DrinkVolume beer = bartender.getTappedBeer("beerName").getTap().dispense(12 /* ounces */); // Train wreck, beer on the floor
glass.setContents(beer); 

// YES!
Glass glass = bartender.order().beer("beerName"); // Tell the object what to do, it knows how
```