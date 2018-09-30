# Java Base64 Encoding and Decoding

**encode a simple String**

```java
String originalInput = "test input";
String encodedString = Base64.getEncoder().encodeToString(originalInput.getBytes());
```

*decode that String back to the original form:*

```java
byte[] decodedBytes = Base64.getDecoder().decode(encodedString);
String decodedString = new String(decodedBytes);
```

---

## Java 8 URL Encoding

```java
String originalUrl = "https://www.google.co.nz/?gfe_rd=cr&ei=dzbFV&gws_rd=ssl#q=java";
String encodedUrl = Base64.getUrlEncoder().encodeToString(originalURL.getBytes());
```

Decoding happens in much the same way – the getUrlDecoder() utility method returns a java.util.Base64.Decoder that is then used to decode the URL:

```java
byte[] decodedBytes = Base64.getUrlDecoder().decode(encodedUrl);
String decodedUrl = new String(decodedBytes);
```

---

## Encoding/Decoding Using Apache Commons Code

define the commons-codec dependency in the *pom.xml*

```xml
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.10</version>
</dependency>
```

```java
String originalInput = "test input";
Base64 base64 = new Base64();
String encodedString = new String(base64.encode(originalInput.getBytes()));
```

The `decode()` method of Base64 class returns the decoded string:

```java
String decodedString = new String(base64.decode(encodedString.getBytes()));
```

Another simple option is using the static API of `Base64` instead of creating an instance:

```java
String originalInput = "test input";
String encodedString = new String(Base64.encodeBase64(originalInput.getBytes()));
String decodedString = new String(Base64.decodeBase64(encodedString.getBytes()));
```



---
