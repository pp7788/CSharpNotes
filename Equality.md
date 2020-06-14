# Equality in C#

## 1. How C# handles equality?

#### 1.1 `==`

The behavior of `==` operator is determined by the __compile-time types__ of its operands. This is determined by the declared types of variables, the declared return types of methods or properties, and the rules for evaluating expressions. 

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

   No, because the NaN value is neither greater than, less than, nor equal to any other double (or float) value, __including NaN__. 

   ```csharp
   var x = float.NaN;
   float.NaN == x; // return False
   ```

   Use `IsNaN` instead.
   ```csharp
   float.IsNaN(x); // return True
   ```
#### 1.2 non-static Equals method

* The biggest difference between this method and the `==` operator is that the behavior of x.Equals(y) is determined by the __run-time type__ of x. This is determined by the actual type of the object, independent of how any variables or return types are declared.

   ```csharp
   bool comp3 = a.Equals(b); // return True
   bool comp4 = a.Equals(x); // return True
   bool comp5 = x.Equals(a); // return True
   bool comp6 = x.Equals(y); // return True
   ```

* Another difference occures when two types are different, more specifically, __when x is not a super-type of y.__ In this case, x.Equals(y) returns false by default; however x == y either will be disallowed (if the two types are inconsistent) or will be performed using the type of y. 

   ```csharp
   5.Equals(5.0) // return False
   5 == 5.0 // return True
   ```

#### 1.3 static methods

* static bool Equals(object x, object y)

   The main purpose of this method is to __avoid the NullReferenceException__ that is thrown by x.Equals(y) when x is null.

* static bool ReferenceEquals(object x, object y)

   This method returns true if x and y refer to the same object or are both null. 
   
   ```csharp
   string a = "abc";
   string b = "0abc".Substring(1);

   bool comp3 = Equals(a, b);          // return True
   bool comp4 = ReferenceEquals(a, b); // return False
   ```

## 2. How to redefine equality?

#### step 1. overload `==`

* When overload `==`, don't forget to overload `!=` as well.

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

* The hashCode is used as a shortcut to determine equality, thus __equal objects should have the same hash code.__ If we override equals, we must create a matching hashCode implementation, otherwise things that are equal according to our implementation would likely not have the same hash code because they use object‘s implementation.

* Use the same fields that are used in equals (or a subset thereof).

