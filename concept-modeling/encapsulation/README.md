# Encapsulation

### Tell the door to open itself?

A _Door_ having an _.open\(\)_ method is corect : it is proper _OOP_ and respecting the "the expert principle".

```java
Door.open();
```

In the context of encapsulation, where we want :

* to build an abstraction \(a term at the base of object-oriented programming\) of the "door" concept
* with some available functionality \(that the abstraction offers to its callers\)
* and without necessarily seeing the insides of how this functionality is offered 

Then, the idea of

```java
Door.open();
```

would be correct. 

### A bit counter-intuitive, no?

#### _**The door should open itself??**_

**Wrong question.** The correct question is : _should the door know how to open?_ 

Yes, and preferably only it should know that. This would allow changes on the internals \(not changes of visible functionality, but just internal details\) to not be noticed \(to impact\) the callers.

### Spare the caller

To save a caller some trouble \(he/she should not care how a door is opened\) then the details of opening a door should be hidden inside the _Door_ class. 

We want to build a "black box" and allow the caller to not care what is inside. From the perspective a caller, the door could have a locking mechanism or not, it could open on the inside, on the outside, or it could be a sliding door. [_It could even be a freaky door_](https://www.google.ch/search?q=torggler+kinetic+door)_._

#### The inside should be hidden

Ideally, only the _Door_ should know what is its opening mechanism.

```java
class Door {
    private final OpeningMechanism openingMechanism;    
    public Door(OpeningMechanism openingMechanism) {
        this.openingMechanism = openingMechanism;
    }
    
    public void open() {
        switch(openingMechanism) {
            case OpeningMechanism.INSIDE :
                openOnTheInside();
                break;
            case OpeningMechanism.OUTSIDE :
                openOnTheOutside();
                break;
            case OpeningMechanism.SLIDE
                slide();
                break;
            }
    }
    
    private void openOnTheInside() {
        ...
    }    
    private void openOnTheOutside() {
        ...
    }
    private void slide() {
        ...
    }
    
    private enum OpeningMechanism {
        INSIDE,
        OUTSIDE,
        SLIDE
    }
}
```

### 

