### Ways to check if an instance x is null.

#### 1. use `==`

```csharp
x == null
```

Note, this way is not safe when the operator '==' is overloaded, as shown below.

```csharp
class Nully
{
    public static bool operator ==(Nully n, Object o)
    {
        return true;
    }

    public static bool operator !=(Nully n, Object o)
    {
        return !(n == o);
    }

    public static void Main()
    {
        var x = new Nully();
        Console.WriteLine(null == x); //Expect "False" but return "True".
    }
}
```

#### 2. use `is`

To solve the concern in using `==`, we can use `is` instead because it cannot be overloaded.

```csharp
x is null
```

#### 3. use `.Equals()`

```csharp
x.Equals(null)
```

Note, this way is not safe when the method '.Equals()' is overridden, as shown below.

```csharp
class Nully
{
    public override bool Equals(object o)
    {
        return true;
    }
    
    public static void Main()
    {
        var x = new Nully(); 
        Console.WriteLine(x.Equals(null)); //Expect "False" but return "True".
    }
}
```

#### 4. use `.ReferenceEquals()`

To solve the concern in using `.Equals()`, we can use `.ReferenceEquals()` instead because it cannot be overridden.


```csharp
x.ReferenceEquals(null)
```

#### 5. use `try catch`

```csharp
class Nully
{
    public String Name { get; set; }

    public static void Main()
    {
        try
        {
            Nully x = null;
            Console.WriteLine(x.Name);
        }
        catch(NullReferenceException e)
        {
            Console.WriteLine("Exception: Null reference!");
        }
    }
}
```

#### 6. use null-conditional operator `?.` and `?[]`

It applies to member access or element access. The null-conditional operators are short-circuiting. That is, if one operation in a chain of conditional member or element access operations returns null, the rest of the chain doesn't execute.

```csharp
Student[] students;
students?[1]?.Name?.LastName;
```

#### 7. use null-coalescing operator `??`

When work with _nullable value types_ and need to provide a value of an underlying value type, use the `??` operator to specify the value to provide in case a nullable type value is null.

```csharp
int? a = null;
int b = a ?? -1;
Console.WriteLine(b);

bool isNull = a is null;
Console.WriteLine(isNull);

a ??= 0;
Console.WriteLine(a);
```

Note, 
* `a ??= 0` is the same as `a == null ? -1 : a`, the former is neat.
* `??` is available in C# 8.0 and later.
