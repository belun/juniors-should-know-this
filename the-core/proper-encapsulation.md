# Proper encapsulation

### Sample application

_\(same as for the bad example\)_

Suppose that we have to write an application to **keep track of people**.

### **Given data**

_\(same as for the bad example\)_

The input of the application will be a **first name, a last name** and **the gender** given for each person.

### The data model

 _\(almost the same as for the bad example\)_

The ****main business concept ****will be _Person_, having attributes _firstName , lastName, gender_ :

```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
}
```

### Business logic

_\(same as for the bad example\)_

Say that, for a given person, we need to **format a full name** \(this is some of the logic expected from the application\). 

The full name must consist of a concatenation of a title \(based on the gender : "Mr." for male and "Mrs." for female\), followed by a space, then _firstName_ and _lastName,_ separated by a space : 

> Mr./Mrs.&lt;space&gt;firstName&lt;space&gt;lastName

#### **Implementation** - _richclass_

_\(new concept\)_

A _rich class_ is class that does things \(contains logic\), not just holds data. The term comes as the opposite of data a class \(that just exposes getters and setters for its data ; sometimes also referred as an _anemic class_, because it is too simple\). 

The term _rich class_ is also a bit misleading, as we want this class to be properly encapsulated.The best name would be a domain class that is properly encapsulated \(but that looks to long\).

{% code-tabs %}
{% code-tabs-item title="encapsulated class" %}
```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String formatFullName() {
        String title = "male".equals(gender) ? "Mr." : "Mrs.";
        return title + " " + firstName + " " + lastName;
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Remarks

* notice how there are no getters ; the properties of _Person_ remain private / hidden \(this is also called _information hiding_\)
* notice how the logic stays in the same class as the data it uses

### What is good with this approach?

As you have probably guessed it, the bad things from section with the counter example :

* biggest win : the encapsulation of the class _Person_ is not broken. The internal state of this class is hidden from the world. 
  * we can rename the concept _lastName_ into _familyName_ without impacting a client of the method _.formatFullName\(\)_ 
  * we can refactor inside of this class \(change the private parts\) without worrying of effects in other parts
* we are writing business logic \(logic requested by business, as a feature\) and we are sticking to business names
  * 
* the logic that works with the internal state of the _Person_ is in the same class and this make it easier to keep track of it. We are following _the Expert Principle_.
  * only in the example \#1 
  * example \#2, with the class _FullName,_ is good example for a later section, "\[Moving state around\]\(../moving-state-around.md\)"

Sure, we only have one concept for now, the _Person_, but we could easily extract the method ._formatFullName\(\)_  into a _FullName_ class \(and we would still be sticking to business concepts as class names\)

{% code-tabs %}
{% code-tabs-item title="encapsulated class with a collaborator" %}
```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String formatFullName() {
        return FullName.format(firstName, lastName, gender);
    }
    
    static class FullName {            
        public static String format(String firstName, String lastName, String gender) {
            String title = "male".equals(gender) ? "Mr." : "Mrs.";
            return title + " " + firstName + " " + lastName;
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The collaborator, _FullName, does not need a state in this example,_  so it only exposes logic \(the method ._format\(\)_ \) that receives the data it needs at runtime. It could have easily had _firstName_, _lastName_ and _gender_ as state, if it needed that data longer than the scope of _Person.formatFullName\(\)_

