# Counter example

### Sample application

Suppose that we have to write an application to **keep track of people**.

### **Given data**

The input of the application will be a **first name, a last name** and **the gender** given for each person.

### The data model

The ****main business concept ****will be _Person_, having attributes _firstName , lastName, gender_ :

```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String getFirstName() {
        return firstName;
    }
    
    public String getLastName() {
        return lastName;
    }
    
    public String getGender() {
        return gender;
    }
}
```

### Business logic

Say that, for a given person, we need to **format a full name** \(this is some of the logic expected from the application\). 

The full name must consist of a concatenation of a title \(based on the gender : "Mr." for male and "Mrs." for female\), followed by a space, then _firstName_ and _lastName,_ separated by a space : 

> Mr./Mrs.&lt;space&gt;firstName&lt;space&gt;lastName

#### **Implementation** - _Service_ class

What one might do, to implement this logic, is to create a _Service_ that does the required logic.

```java
class PersonService {
    public String formatFullName(Person person) {
        String title = "male".equals(person.getGender()) ? "Mr." : "Mrs.";
        return title + " " + person.getFirstName() + " " + person.getLastName();
    }
}
```

#### Alternative - _Util_ class

An alternative to a service could be an util class \(e.g. _PersonUtil_\) or a helper class \(e.g. _PersonHelper_\)

```java
class PersonUtil {
    public String formatFullName(Person person) {
        String title = "male".equals(person.getGender()) ? "Mr." : "Mrs.";
        return title + " " + person.getFirstName() + " " + person.getLastName();
    }
}
```

### What is wrong with this approach?

Several things :

* biggest issue : the encapsulation of the class _Person_ has been broken. The internal state of this class is exposed to the world. 
  * someone that relies on the internals of this class \(e.g. _PersonService_\), would have to change when we want to change the internal state of this class \(for example, if we want to rename the concept _lastName_ into _familyName_\)
  * or, another way put, the writer of this code might not be able to change the internal state of this class without : either breaking compatibility with its users \(making their code non-compilable\) or will not be able to change at all, if there is no access to that code or if we do not want to change that code
    * we encounter lots of cases like this in big applications, where the code is so coupled together, that changing one thing has deep, and often unknown, effect in other parts, and we would like to touch as little as possible to avoid bugs and having to do to many regression tests.
* _Util_ and _Helper_ names are to generic and they even represent technical terms. In code that does business logic, it is best to stick to business terms. 
  * much of the code we write is some kind of "helper" of another class ; there has got to be a better way
* the logic that works with the internal state of the _Person_ is in another class and this make it difficult to keep track of it.



