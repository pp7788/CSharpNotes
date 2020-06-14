# Equality in C#

## 1. How C# handles equality?

#### 1.1 `==`

* value type
    * `==` evaluates to __True__ if its operands contain the same values.
    
* reference type
    * `==` evaluates to __True__ when the two operands refer to the same object (i.e., they refer to the same memory location). 
    
* string type
    * The string class defines the `==` operator to evaluate to __True__ if the given strings are the same length and contain the same sequence of characters.

    ```csharp
    string a = "abc";
    string b = "0abc".Substring(1);

    object x = a;
    object y = b;

    bool comp1 = a == b; // return True
    bool comp2 = x == y; // return False
    ```
* Can we check NaN via == ?

   No, because the NaN value is neither greater than, less than, nor equal to any other double (or float) value, __including NaN__. 

   ```csharp
   var x = float.NaN;
   Console.WriteLine(float.NaN == x); // return False
   ```

   Use `isNaN` instead.
   ```csharp
   Console.WriteLine(float.IsNaN(x)); // return True
   ```

## 2. How to re-define equality?

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


