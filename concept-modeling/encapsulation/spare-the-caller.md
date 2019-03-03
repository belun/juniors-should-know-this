# Spare the caller

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

