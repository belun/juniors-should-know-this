# Getters

Notice how in the "transferring data" section, there was no mention of "exposing data" \(as in, make use of getters\). 

That is because Getters can lead to breaking of encapsulation.

#### What if I need to expose data?

Surely, data might need to be "exposed" for presentation \(or even for persistence\). And in this case, use Getters. 

Or, even more straight forward, expose directly the fields of the class.

Lets presume that the field _gender_ it is not needed for any other layer, so it is not exposed \(just to show how not all data will have a getter\).

{% code-tabs %}
{% code-tabs-item title="rich class with getters" %}
```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String formatFullName() {
        ...
    }
    
    public String getFirstName() {
        return firstName;
    }
    public String getLastName() {
        return lastName;
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

A more elegant _way_ would be to create _data transfer objects_ \(DTOs ; objects that do not perform logic\). This, however, adds a new layer of abstraction.

{% code-tabs %}
{% code-tabs-item title="rich class that exposes a DTO" %}
```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String formatFullName() {
        ...
    }
    
    public DTO toDTO() {
        return new DTO(firstName, lastName);
    }
    
    public class DTO {
        private String firstName;
        private String lastName;
        private DTO(String firstName, String lastName) {
            this.firstName = firstName;
            this.lastName = lastName ;
        }
        
        public String getFirstName() {
            return lastName;
        }
        public String getLastName() {
            return gender;
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### What if I do not want extra objects \(DTOs\), but would still like to avoid Getters?

You can make use of interfaces. 

The most straight forward way would be to have **interfaces with setters** \(that accept data\) and let the classes the need that data implement those interfaces.

{% code-tabs %}
{% code-tabs-item title="rich class that pushes data" %}
```java
class Person {
    private String firstName;
    private String lastName;
    private String gender;
    
    public String formatFullName() {
        ...
    }
    
    public <DTO> DTO toDTO(DTOBuilder<DTO> builder) {
        return builder
            .withFirstName(firstName)
            .withLastName(lastName)
            .build();
    }
}

interface DTOBuilder<DTO> {
    public DTOBuilder<DTO> withFirstName(String firstName);
    public DTOBuilder<DTO> withLastName(String lastName);
    public DTO build();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Here, the rich class, _Person_, does not know in which concrete class the data is going. This is useful when the concrete class that will receive the data is part of another layer that we do not want to depend on, from the layer that pushes the data.

This still respects the principle : _Tell, don't ask._

Note that setters do not have to receive a single piece of data. A setter can receive more that one piece of data \(more than one parameter\).

{% code-tabs %}
{% code-tabs-item title="interface with one setter" %}
```java
interface DTOBuilder<DTO> {
    public DTOBuilder<DTO> withNames(String firstName, String lastName);
    public DTO build();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

_This approach also adds another layer of abstraction \(the Builder interface\), in the attempt to allow data to be pushed into unknown classes._ 

The _Builder_ defines formally \(as it is an interface\) what data can be made available externally.

#### So, are Getters are bad?

Not necessarily, but they can easily lead to breaking the encapsulation of classes, as the caller can start doing logic on the data collected. 

{% hint style="info" %}
Keep an eye on the caller of the getters. 
{% endhint %}

The same applies for any of above approaches.

#### When \(or what for\) can I use Getters \(or an alternative\)?

Getters \(or an alternative\) can be used for data transfer to other layers of the application, other than the layer that contains the classes that perform the logic on that data\).

In the previous examples, _Person_ was built as a business rich class, a class in the business layer that does business logic \(where the only defined business logic needed, for now, is implemented in _.formatFullName\(\)_ \)

_As a side note_, classes in business layer do not depend on classes from external technologies \(Hibernate classes for example\) or on classes from other layers \(like DTOs defined in the presentation layer\). They only depend on other classes from business layer, that do business logic. 

#### What to avoid?

Bad code steals data from its owner and does logic on that data \(that is otherwise meant to be done by the owner\). 

This is a bad practice, as a reader might not expect \(and should not expect\) to find logic scattered all over the place.

#### What are some guidelines I can use?

Make sure that :

* no logic is done in one layer that is not part of that layer \(e.g. presentation logic in presentation layer and business logic in business layer\)
* within one layer, the data owners are clear \(rich classes contain the logic together with data, properly guard that data and do proper transfer of it, if needed\)



