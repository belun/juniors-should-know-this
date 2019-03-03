---
description: measuring performance
---

# Cohesion

## What is cohesion?

Cohesion is a metric \(something that can be measured\) that shows how well put together a class is.

## How do you measure it?

Suppose we have a class with 4 fields and 5 methods.

{% code-tabs %}
{% code-tabs-item title="sample class" %}
```java
class SomeClass {
    private String field1;
    private String field2;
    private String field3;
    private String field4;

    public void method1() {
        ...
    }

    public void method2() {
        ...
    }

    public void method3() {
        ...
    }

    public void method4() {
        ...
    }

    public void method5() {
        ...
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

_If all methods use all fields, than this class has highest cohesion possible_. This is ideal.

{% code-tabs %}
{% code-tabs-item title="high cohesion" %}
```java
class IdealClass {
    private String field1;
    private String field2;
    private String field3;
    private String field4;

    public void method1() {
        // does something with field1, field2, field3, field4
    }

    public void method2() {
        // does something with field1, field2, field3, field4
    }

    public void method3() {
        // does something with field1, field2, field3, field4
    }

    public void method4() {
        // does something with field1, field2, field3, field4
    }

    public void method5() {
        // does something with field1, field2, field3, field4
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The opposite of this \(_low cohesion_\) would be when each method uses only 1 field \(and not the same field\), or no field at all.

{% code-tabs %}
{% code-tabs-item title="low cohesion" %}
```java
class BadlyBuiltClass {
    private String field1;
    private String field2;
    private String field3;
    private String field4;

    public void method1() {
        // does something with field1
    }

    public void method2() {
        // does something with field2
    }

    public void method3() {
        // does something with field3
    }

    public void method4() {
        // does something with field4
    }

    public void method5(String someParameter) {
        // does something with someParameter
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In this example, _BadlyBuiltClass.method5\(\)_ does not make use of any internal state. The parameter _someParameter_ was used just to give some data to this method to use for its logic.

### Is there an even worse case?

Well, all methods can just receive data as parameters and work with those, not making use of any of the state of the class. Or, they could grab the data needed for their logic from other sources, like static methods of other classes or by just opening a file.

## Let's look at a more common scenario

Suppose the first 3 fields are used in methods 1 through 3, while the fields 3 and 4 are used in the last 2 methods. The field 3 is common just to make things more difficult later.

{% code-tabs %}
{% code-tabs-item title="medium cohesion" %}
```java
class CommonClass {
    private String field1;
    private String field2;
    private String field3;
    private String field4;

    public void method1() {
        // does something with field1, field2, field3
    }

    public void method2() {
        // does something with field1, field2, field3
    }

    public void method3() {
        // does something with field1, field2, field3
    }

    public void method4() {
        // does something with field3, field4
    }

    public void method5() {
        // does something with field3, field4
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## How can this be improved?

Let's split the _CommonClass_ in 2 classes, and keep together the methods that use common fields. Of course, the methods that work on some fields, stay in the same class as those fields \(the expert principle\)

{% code-tabs %}
{% code-tabs-item title="high cohesion again" %}
```java
class CommonClassPart1 {
    private String field1;
    private String field2;
    private String field3;

    public void method1() {
        // does something with field1, field2, field3
    }

    public void method2() {
        // does something with field1, field2, field3
    }

    public void method3() {
        // does something with field1, field2, field3
    }
}

class CommonClassPart2 { 
    private String field3;
    private String field4;  

    public void method4() {
        // does something with field3, field4
    }

    public void method5() {
        // does something with field3, field4
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now we have, again, classes with high cohesion.

Notice how _field3_ is part of the state of both classes \(as it is needed for the logic in both\)

## What is it useful for?

* cohesion can be used as a hint whether our class is doing more than one responsibility or not.  Single responsibility and high cohesion give a good meaning to a class. A meaningful class is easy to work with.
* low cohesion _can be used as a code smell_ that tells us that we should split our class.

