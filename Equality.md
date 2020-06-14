## equality in C#

## equality override

#### 1. override `==`

```csharp
public static bool operator ==(iType x, iType y)
{
    if (Equals(x, null))
    {
         return (Equals(y, null));
    }
    else if (Equals(y, null))
    {
        return false;
    }
    else
    {
        // code to determine if x == y
    }
}
```
```csharp
public static bool operator !=(iType x, iType y)
{
    return !(x == y);
}
```
