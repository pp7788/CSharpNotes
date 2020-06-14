## equality in C#

## equality override

#### step 1. overload `==`

* When overload `==`, don't forget to overload `!=`.

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

#### step 2. override `Equals`

* __If overload ==, then must override Equals.__ When a type overloads the equality operator, it must also override the Equals(Object) method to provide the same functionality. 

* This is typically accomplished by writing the Equals(Object) method __in terms of the overloaded equality operator.__

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

#### step 3. override `GetHashCode`

## check NaN via == ?

* The NaN value is neither greater than, less than, nor equal to any other double (or float) value, __including NaN__. 

```csharp
var x = float.NaN;
Console.WriteLine(float.NaN == x); // return False

Console.WriteLine(float.IsNaN(x)); // return True
```
