---
description: some tricks
---

# Small classes

#### Since logic is supposed to stay with the data \(and respect encapsulation\), won't some classes become huge?

This is what the cohesion metric is for. It can be used a guide to split classes in smaller classes.

#### Won't I run out of names? How do I name classes that represent similar concepts?

Well, respecting the expert principle and maintaining encapsulation does not mean one concept cannot appear in the names of multiple classes. 

Let's introduce a class called _VerifiedPerson._

The class _Person_, from previous examples could exist in the same application as a the class _VerifiedPerson._ 

The class _VerifiedPerson_ could represent a person whose identity has been verified, while the class _Person_ could represent a person that was just introduced in the system. 

{% hint style="info" %}
Make use the life cycle \(or better said, the stage of a life cycle\) of an concept to name classes \(together with the name of the concept\).
{% endhint %}

In the previous example, an instance of the class _Person_ can come become an instance of the class _VerifiedPerson_, once the verification has been done.

```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String formatFullName() {
        ...
    }
    
    public VerifiedPerson verifiedBy(String verifier) {
        return new VerifiedPerson(formatFullName(), verifier);
    }    
}

class VerifiedPerson {
    private String fullName;
    private String verifier;
}
```

Notice how the _VerifiedPerson_ has a totally different state from a _Person._ This is to show that a concept's state can change through the application, as the logic needed from that class also changes. 

Also, the _VerifiedPerson_ does not have any defined logic right \(for simplicity reasons\). It could be used only for :

```text
somePerson instanceof Verified
```



