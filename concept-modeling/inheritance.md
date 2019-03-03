# Inheritance

### Do you think that the _Door_ is getting too big, by now?

{% code-tabs %}
{% code-tabs-item title="this particular implementation has repetive \"ifs\" \(and needs cleanup\)" %}
```java
class Door {
    private final OpeningMechanism openingMechanism;
    public Door(OpeningMechanism openingMechanism) {
        this.openingMechanism = openingMechanism;
    }
    
    public void open(OpeningDirection openingDirection) {
        check(openingDirection);
        ...
        
        switch(openingMechanism) {
            case OpeningMechanism.INSIDE :
                openOnTheInside();
                break;
            }
            case OpeningMechanism.OUTSIDE :
                openOnTheOutside();
                break;
            }
            case OpeningMechanism.SLIDE:
                slide();
                break;
            }
            ...
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
    private void check(OpeningDirection openingDirection) {
        if(openingDirection == OpeningDirection.INSIDE &&
            openingMechanism != OpeningMechanism.INSIDE) {
            
            throw new BrokenDoorException("Damn!! You strong.");
        }
    }
    private enum OpeningMechanism {
        INSIDE,
        OUTSIDE,
        SLIDE
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Inheritance to the rescue

Let's introduce the third core concept of object-oriented, _polymorphism._

```java
class NormalDoor implements Door {
    
    public void open(OpeningDirection openingDirection) {
        if(openingDirection != OpeningDirection.INSIDE) {            
            throw new BrokenDoorException("Damn!! You strong.");
        }
        openOnTheInside();
    }
    
    private void openOnTheInside() {
        ...
    }
}
```

```java
class ReverseDoor implements Door {
    
    public void open(OpeningDirection openingDirection) {
        if(openingDirection != OpeningDirection.OUTSIDE) {            
            throw new BrokenDoorException("Damn!! You strong.");
        }
        openOnTheOutside();
    }
    
    private void openOnTheOutside() {
        ...
    }
}
```

```java
class SlidingDoor implements Door {
    
    public void open(OpeningDirection openingDirection) {
        if(openingDirection != OpeningDirection.SLIDING) {            
            throw new BrokenDoorException("Damn!! You broke the wall, too.");
        }
        slide();
    }
    
    private void slide() {
        ...
    }
}
```

```java
interface Door {
    void open(OpeningDirection openingDirection)
}
```

Since lots of business logic revolves around different opening directions \(relies on if-statements based on different values of the enum _OpeningDoor_\), the class _Door_ could be split in _NormalDoor, ReverseDoor_ and _SlidingDoor_.

 Try to have a look at the cohesion of the class _Door_ versus the classes _NormalDoor, ReverseDoor_ and _SlidingDoor._ 

Also, conceptually speaking, a method _slide\(\)_ makes more sense in a _SlidingDoor_.

Starting from a small abstraction of a _Door_ \(the class _Door\),_ as __"owner" of the state of _OpeningMechanism -_ keeping it internal by protecting against illegal usages and hiding the details ; basically doing the logic around internal state -  further additions \(business logic\) to the concept _Door_ could be spread to classes like _NormalDoor, ReverseDoor_ and _SlidingDoor_ that incorporate predominant concepts directly in their name \(e.g. _Sliding_\).

