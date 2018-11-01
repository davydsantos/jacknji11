# Java Interface for PKCS#11

Provides a Java PKCS#11 interface that provides low-level interface
as close as possible to the cryptoki C interface and wraps with
Java-styled interface providing convenience methods and using
exceptions for error handling.

Uses a provider architecture to allow any implementation of the 
native mapping.  Includes [JNA](https://github.com/twall/jna)
as default provider to bridge between Java and native cryptoki lib.

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