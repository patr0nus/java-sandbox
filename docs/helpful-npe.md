# Helpful NPE Messages



Assume we have the following classes. 

```java
class Person {

    private String name;
    private int age;

    private Address address;

    public Person() {
    }

    public Person(String name, int age) {
        this.age = age;
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

}

class Address {

    private final City city;

    public Address(City city) {
        this.city = city;
    }

    public City getCity() {
        return city;
    }

}

class City {

    private final String name;

    public City(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

And create a `Person` instance like this.

```java
Person person = new Person();
```

When you try to access the address of the `person` object.

```java
person.getAddress().getCity().getName()
```

Compile the application. And run it, you will see the famous `NullPointerException`.

```bash
Exception in thread "main" java.lang.NullPointerException
        at com.example.demo.NpeExample.main(NpeExample.java:12)
```

But the above message does not indicate where causes the exception.  Either `person.getAddress()` or `person.getAddress().getCity()` could raise this exception.

In Java 14, add an extra parameter `-XX:+ShowCodeDetailsInExceptionMessages ` to `java` when running the application, you will get detailed messages about the `java.lang.NullPointerException`.

```bash
#java -XX:+ShowCodeDetailsInExceptionMessages --enable-preview com.example.demo.NpeExample

Exception in thread "main" java.lang.NullPointerException: Cannot invoke "com.example.demo.Address.getCity()" because the return value of "com.example.demo.Person.getAddress()" is null
        at com.example.demo.NpeExample.main(NpeExample.java:12)
```
It is very helpful when you are debugging your application.

​        



