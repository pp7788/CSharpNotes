## equality in C#

## equality override

#### 1. overload `==`

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

public static bool operator !=(iType x, iType y)
{
    return !(x == y);
}
```

#### 2. override `Equals`

```csharp
public override bool Equals(object obj)
{
    if (obj is iType)
    {
        return this == (iType)obj;
    }
    else
    {
        return false;
    }
}
```

#### 3. override `GetHashCode`

## check NaN via == ?

```csharp
var x = float.NaN;
Console.WriteLine(float.NaN == x); // return False
Console.WriteLine(float.IsNaN(x)); // return True
```

Because the NaN value is neither greater than, less than, nor equal to any other double (or float) value, including NaN. 
