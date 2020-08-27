# Jackson Annotations

## Jackson Serialization Annotations
### @JsonAnyGetter
```java
public class ExtendableBean {
    public String name;
    private Map<String, String> properties;
 
    @JsonAnyGetter
    public Map<String, String> getProperties() {
        return properties;
    }
}
```
```
// before
{
  "name": "yeob32",
  "properties": {
    "attr2": "val2",
    "attr1": "val1"
  }
}

// after
{
  "name": "yeob32",
  "attr2": "val2",
  "attr1": "val1"
}
```

### @JsonGetter("name")
```java
public class MyBean {
    public int id;
    private String name;
 
    @JsonGetter("name")
    public String getTheName() {
        return name;
    }
}
```
```
// before
{
  "id": 1,
  "theName": "yeob32"
}

// after
{
  "id": 1,
  "name": "yeob32"
}
```

### @JsonPropertyOrder
```java
@JsonPropertyOrder({ "name", "id" })
public class MyBean {
    public int id;
    public String name;
}
```
```
// before
{
  "id": 1
  "name": "yeob32",
}

// after
{
  "name": "yeob32",
  "id": 1
}
```

### @JsonRawValue
```java
public class RawBean {
    public String name;
 
    @JsonRawValue
    public String json;
}
```
```
// before
{
  "name": "yeob32",
  "json": "{\"attr\": false}"
}

// after
{
  "name": "yeob32",
  "json": {
    "attr": false
  }
}
```

### @JsonValue
```java
public enum TypeEnumWithValue {
    TYPE1(1, "Type A"), TYPE2(2, "Type 2");
 
    private Integer id;
    private String name;
 
    // standard constructors
 
    @JsonValue
    public String getName() {
        return name;
    }
}
```
```
// before
Type A

// after
Type A
```

### @JsonRootName
```java
@JsonRootName(value = "user")
public class UserWithRoot {
    public int id;
    public String name;
}
```
```
// before
{
    "UserWithRoot":{
        "id":1,
        "name":"John"
    }
}

// after
{
    "user":{
        "id":1,
        "name":"John"
    }
}
```

## Jackson Deserialization Annotations
### 
```java

```
```
// before


// after

```

## Jackson Property Inclusion Annotations
### @JsonIgnoreProperties
```java
@JsonIgnoreProperties({ "id" })
public class BeanWithIgnore {
    public int id;
    public String name;
}
```
```
// before
{
  "id": 1
  "name": "yeob32"
}

// after
{
  "name": "yeob32"
}
```

### @JsonIgnore
```java
public class BeanWithIgnore {
    @JsonIgnore
    public int id;
 
    public String name;
}
```
```
// before
{
  "id": 1
  "name": "yeob32"
}

// after
{
  "name": "yeob32"
}
```

### @JsonIgnoreType
```java
public class User {
    public int id;
    public Name name;
 
    @JsonIgnoreType
    public static class Name {
        public String firstName;
        public String lastName;
    }
}
```
```
// before
{
  "id": 1,
  "name": {
    "firstName": "yeob",
    "lastName": "32"
  }
}

// after
{
  "id": 1
}
```

### @JsonInclude
```java
@JsonInclude(Include.NON_NULL)
public class MyBean {
    public int id;
    public String name;
}
```
```
// before
{
  "id": 1,
  "name": null
}

// after
{
  "id": 1
}
```

## Jackson General Annotations
###  
```java

```
```
// before


// after

```

### 
```java

```
```
// before


// after

```

### 
```java

```
```
// before


// after

```