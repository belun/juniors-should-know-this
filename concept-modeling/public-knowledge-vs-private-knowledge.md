# Public knowledge vs private knowledge

### Can a _Person_ .open a _Door_?

Well, it could make the call, but it should not access what is inside. Ideally, it should not even know what is inside.

Suppose we need to give the ability of opening a door to another abstraction, like _Person_.

```java
class Person {
    public void open(Door door) {
        ...
    }
}
```

Then, the only thing it should do is make the call :

```java
class Person {
    public void open(Door door) {
        door.open();
    }
}
```

### Can a _Person_ .push the _Door_? Or .pull the Door?

_Person_ should not care about how the _Door_ opens.

The _Person_ abstraction should not know to much :

{% code-tabs %}
{% code-tabs-item title="too many details" %}
```java
class Person {
    public open(Door door) {
        door.open(OpeningMechanism.INSIDE);
        // OR door.open(OpeningMechanism.OUTSIDE);
        // OR door.open(OpeningMechanism.SLIDE);
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Notice how the caller has to know how the door can open. It can either call _.open\(OpeningMechanism.INSIDE\)_ or _.open\(OpeningMechanism.OUTSIDE\)_ or _.open\(OpeningMechanism.SLIDE\)_.

### Wait, can't some doors open both inside and outside \(and the caller decide which one\)?

Usually no, but in case that we have to model such behavior, the concept should have a name and its own class \(like _OpeningDirection\),_ not be a private concept of the abstraction _Door_ . It should __be separate from the concept _OpeningMechanism_ and it could be passed as parameter_._

```java
enum OpeningDirection {
    INSIDE,
    OUTSIDE,
    SLIDEWAYS
}
```

```text
class Person {
    public open(Door door) {
        door.open(OpeningDirection.INSIDE);
    }
}
```

Plus, each type of the _Door_ must support certain functionality and protect against others.

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
    }     
    private enum OpeningMechanism {
        INSIDE,
        OUTSIDE,
        SLIDE
    }
}
```

Notice how the abstraction _Door_ takes itself care of illegal usages. It is the "owner" of the concept _OpeningMechanism_. Also, it can receive "instructions" on what do to.

_OpeningMechanism_ is an internal concept of _Door,_ while _OpeningDirection_ is an external concept that can act as an "suggestion". It might work, it might not work \(throw an exception\). 

{% code-tabs %}
{% code-tabs-item title="will throw BrokenDoorException" %}
```java
new Door(OpeningMechanism.INSIDE).open(OpeningDirection.OUTSIDE)
```
{% endcode-tabs-item %}
{% endcode-tabs %}



