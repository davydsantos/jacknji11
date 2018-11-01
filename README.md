# Java Interface for PKCS#11

Provides a Java PKCS#11 interface that provides low-level interface
as close as possible to the cryptoki C interface and wraps with
Java-styled interface providing convenience methods and using
exceptions for error handling.

Uses a provider architecture to allow any implementation of the 
native mapping.  Includes [JNA](https://github.com/twall/jna)
as default provider to bridge between Java and native cryptoki lib.

## Import
### Maven
Since this is currently not published into any mvn repos, the easiest way is to use [jitpack.io]. For that: 
- add the jitpack as a new repo
```xml
	<repositories>
		<repository>
			<id>jitpack.io</id>
			<url>https://jitpack.io</url>
		</repository>
	</repositories>
```
- add the dependency (slightly different pattern using the matching tag from this repo)
```xml
		<dependency>
			<groupId>com.github.davydsantos</groupId>
			<artifactId>jacknji11</artifactId>
			<version>1.2</version>
		</dependency>
```

## Usage example

```java
import java.util.Arrays;

import org.pkcs11.jacknji11.CE;

public class TestSlotInfo {
    public static void main(String args[]) {
        CE pkcs11 = new CE("c:/windows/system32/aetpkss1.dll");
        pkcs11.Initialize();
        Arrays.stream(pkcs11.GetSlotList(true))
            .mapToObj(pkcs11::GetSlotInfo)
            .forEach(System.out::println);
    }
}
```
