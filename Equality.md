## Equality in C#

* equality override

```c#
public static bool operator ==(iType x, iType y)
{
    // define the behavior of ==
}

public static bool operator !=(iType x, iType y)
{
    return !(x == y);
}
```
