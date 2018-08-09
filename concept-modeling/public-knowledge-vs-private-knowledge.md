---
description: some information hiding
---

# Public knowledge vs private knowledge

### Can a _Person_ .open a _Door_?

Well, it could make the call, but it should not access what is inside. Ideally, it should not even know what is inside.

Suppose we need to give the functionality of opening a door to our abstraction of a _Person_.

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

~~_Person_ should not know to much~~ :

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

### Wait, can't a door open both ways?

In that case, the concept should be called _OpeningDirection,_ not be a private concept of the abstraction _Door_ and be separated from the concept of _OpeningMechanism._

```java
enum OpeningDirection {
    INSIDE,
    OUTSIDE,
    SLIDEWAYS
}
```

Plus, each instance of the _Door_ must support a certain functionality \(or protect against it\).

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

Notice how the abstraction _Door_ takes itself care of illegal usages. It is the "owner" of the concept _OpeningMechanism_. Also, it can receive "instructions" on what do to.

_OpeningMechanism_ is an internal concept of _Door,_ while _OpeningDirection_ is an external concept that can act as an "suggestion". It might work, it might not work. 

{% code-tabs %}
{% code-tabs-item title="will throw BrokenDoorException" %}
```java
new Door(OpeningMechanism.INSIDE).open(OpeningDirection.OUTSIDE)
```
{% endcode-tabs-item %}
{% endcode-tabs %}



