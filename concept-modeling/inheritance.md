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
        if(openingDirection == OpeningDirection.INSIDE &&
            openingMechanism != OpeningMechanism.INSIDE) {
            
            throw new BrokenDoorException("Damn!! You strong.");
        }
        ...
        
        switch(openingMechanism) {
            case OpeningMechanism.INSIDE :
                openOnTheInside();
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

Let's introduce the third core concept of object-oriented, _polimorfism._

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

Starting from a small abstraction of a _Door_ \(the class _Door\),_ as __"owner" of the state of _OpeningMechanism -_ keeping it internal by protecting against illegal usages and hiding the details ; basically doing the logic around internal state -  further implementations of the concept can lead to classes like _NormalDoor_ and _SlidingDoor_  that incorporate inner concepts directly in their name.

