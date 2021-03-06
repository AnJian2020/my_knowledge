# Chapter 2.Variables and Basic Types

## 2.1 Primitive  [Built-in](内置) Types

The arithmetic types represent <font color='red'>characters, integers, boolean values, and floating-point numbers</font>. Primitive built-in types also includes a special type named <font color='red'>void</font>.

### 2.1.1 Arithmetic Types

Two categories: **integral types**(which include character and boolean types) and **floating-point types**.

*Table 2.1. C++: Arithmetic Types*

<img src="https://raw.githubusercontent.com/AnJian2020/md_picture/main/img/202111021226545.png" alt="image-20211102122619366" style="zoom:67%;" />


The bool type represents the truth values true and false.

**A char is the same size as single machine byte.**

| float  | one word(32 bits) |
| ------ | ----------------- |
| double | two word(64 bits) |

The float and double types typically yield about 7 and 16 significant digits, respectively. The type long double is often used as a way to accommodate special-purpose floating-point hardware; its precision is more likely to vary from one implementation to another.

**Signed and Unsigned Types**

The integral types may be signed or unsigned. <font color='cornflowerblue'>A signed type represents negative or positive numbers (including zero); an unsigned type represents only values greater than or equal to zero.</font>

<font color='red'>The types int, short, long, and long long are all signed</font>. We obtain the corresponding unsigned type by adding unsigned to the type.

Three distinct basic character types: <font color='red'>char, signed char and unsigned char</font>. In particular, char is not the same type as signed char. Although there are three character types,<font color='red'> there are only two representations: signed and unsigned.</font>

In an unsigned type, all the bits represent the value.

How to decide which type to use:

- Use an unsigned type when you know that the values cannot be negative.
- Use int for integer arithmetic. 
- Do not use plain char or bool in arithmetic expressions. Use them only to hold characters or truth values. If you need a tiny integer, explicitly specify either signed char or unsigned char.
- Use double for floating-point computations; float usually does not have enough precision, and the cost of double-precision calculations versus single-precision is negligible. 

### 2.1.2 Type Conversions

What happens depends on the range of the values that the types permit:

- One of the nonbool  arithmetic types is assigned to a bool object, the result is false if the value is 0 and true otherwise.

- A bool is assigned to one of the other arithmetic types, the resulting value is 1 if the bool is true and 0 if the bool is false.

- A floating-point value is assigned to an object of integral type, the value is truncated. The value that is stored is the part before the decimal point.

- When we assign an integral value to an object of floating-point type, the fractional part is zero. Precision may be lost if the integer has more bits than the floating-point object can accommodate.

- If we assign an out-of-range value to an object of unsigned type, the result is the remainder of the value modulo the number of values the target type can hold. 

  > (-1)%256 = (-1+256)%256=255%256=255

- If we assign an out-of-range value to an object of signed type, the result is undefined.


**Expressions Involving Unsigned Types**

```c++
#include<iostream>
int main()
{
    unsigned u=10;
    int i = -42;
    std::cout<<i+i<<std::endl;
    // the int value -42 is converted to unsigned before the addition is done
    std::cout<<i+u<<std::endl; 
    return 0;
}
```

Converting a negative number to unsigned behaves exactly as if we had attempted to assign that negative value to an unsigned object. The value “wraps around” as described above.

```c++
#include<iostream>
using namespace std;
int main(){
    unsigned u1=42,u2=10;
    cout<<u1-u2<<endl;
    cout<<u2-u1<<endl;
    return 0;
}
```

**Integer and Floating Point Literal**

<font color='red'>Integer literals that begin with 0 (zero) are interpreted as octal. Those that begin with either 0x or 0X are interpreted as hexadecimal.</font>

By default, <font color='cornflowerblue'>decimal literals are signed whereas octal and hexadecimal literals can be either signed or unsigned types</font>. A decimal literal has the smallest type of int, long, or long long in which the literal’s value fits. Octal and hexadecimal literals have the smallest type of int, unsigned int, long, unsigned long, long long, or unsigned long long in which the literal’s value fits. There are no literals of type short.

*Table 2.2. Specifying the Type of a Literal*

<img src="https://raw.githubusercontent.com/AnJian2020/md_picture/main/img/202111030928383.png" alt="image-20211103092812089" style="zoom: 67%;" />

The value of a decimal literal is never a negative number. The minus sign is an operator that negates the value of its (literal) operand.

Floating-point literals include either a decimal point or an exponent specified using scientific notation. <font color='red'>Using scientific notation, the exponent is indicated by either E or e</font>. 

  > 3.14159 3.14159E0 0. 0e0 .001

By default,<font color='cornflowerblue'> floating-point literals have type double.</font> 

**Character and Character String Literal**

A character enclosed within single quotes is a literal of type char. Zero or more characters enclosed in double quotation marks is a string literal:

```c++
'a' // character literal
"Hello World!" // string literal
```

The type of a string literal is array of constant chars. The compiler appends a null character (’\0’) to every string literal. Thus, the actual size of a string literal is one more than its apparent size. 

Two string literals that appear adjacent to one another and that are separated only by spaces, tabs, or newlines are concatenated into a single literal.

**Escape Sequences**

C++ defines several escape sequences:

|     newline     |  \n  | horizontal tab |  \t  | alert(bell)  | \a   |
| :-------------: | :--: | :------------: | :--: | :----------: | ---- |
|  vertical tab   |  \v  |   backspace    |  \b  | double quote | \\"  |
|    backslash    | \\\  | question mark  |  \?  | single quote | \\'  |
| carriage return |  \r  |    formfeed    |  \f  |              |      |

We can also write a generalized escape sequence, which is \x followed by one or more hexadecimal digits or a \ followed by one, two, or three octal digits. The value represents the numerical value of the character. 

> \7  (bell)		\12  (newline)		\40  (blank)
>
> \0  (null)		\115  ('M')				\x4d  ('M')

Note that if a \ is followed by more than three octal digits, only the first three are associated with the \\. In contrast, \x uses up all the hex digits following it.

**Specifying the Type of a Literal**

We can override the default type of an integer, floating- point, or character literal by supplying a suffix or prefix.

**Boolean and Pointer Literals**

The words true and false are literals of type bool.

The word nullptr is a pointer literal.

## 2.2 Variables

### 2.2.1 Variable Definitions

A simple variable definition consists of a <font color='red'>type specifier, followed by a list of one or more variable names separated by commas, and ends with a semicolon</font>. Each name in the list has the type defined by the type specifier. A definition may (optionally) provide an initial value for one or more of the names it defines.

<font color='cornflowerblue'>*What is an Object? Most generally, an object is a region of memory that can contain data and has a type.*</font>

**Initializers**

 When a definition defines two or more variables, the name of each object becomes visible immediately. Thus, it is possible to initialize a variable to the value of one defined earlier in the same definition.

```c++
double price = 109.99, discount = price * 0.16;
double salePrice = applyDiscount(price, discount);
```

> **Warning**
>
> <font color='red'>Initialization is not assignment. Initialization happens when a variable is given a value when it is created. Assignment obliterates an object’s current value and replaces that value with a new one</font>.

**List Initialization**

<font color='cornflowerblue'>The use of curly braces for initialization is referred to as  list initialization</font>. When used with variables of built-in type, this form of initialization has one important property: The compiler will not let us list initialize variables of built-in type if the initializer might lead to the loss of information.

```c++
long double ld = 3.1415926536;
int a{ld}, b = {ld}; // error: narrowing conversion required
int c(ld), d = ld; // ok: but value will be truncated
```

The compiler rejects the initializations of a and b because using a long double to initialize an int is likely to lose data. At a minimum, the fractional part of ld will be truncated. In addition, the integer part in ld might be too large to fit in an int.

**Default Initialization**

When we define a variable without an initializer, the variable is default initialized. What that default value is depends on the type of the variable and may also depend on where the variable is defined.

<font color='red'>The value of an object of built-in type that is not explicitly initialized depends on where it is defined. </font>

- Variables defined outside any function body are initialized to zero.
- Variables of built-in type defined inside a function are uninitialized. It is an error to copy or otherwise try to access the value of a variable whose value is undefined.

Each class controls how we initialize objects of that class type. In particular, it is up to the class whether we can define objects of that type without an initializer. If we can, the class determines what value the resulting object will have.

<font color='red'>Most classes let us define objects without explicit initializers.</font> Such classes supply an appropriate default value for us. Some classes require that every object be explicity initialized.

> Uninitialized objects of built-in type defined inside a function body have undefined value. Objects of class type that we do not explicitly initialize have a value that is defined by the class.

### 2.2.2 Variable Declarations and Definitions

C++ distinguishes between declarations and definitions. <font color="red">A declaration makes a name known to the program. A file that wants to use a name defined elsewhere includes a declaration for that name.</font> A definition creates the associated entity.

- **declaration**: the type and name of a variable

- **defination**:	specify the name and type, and it allocates  storage and may provide the variable with an initial value.

```c++
extern int i; // declares but does not define i
int j; // declares and defines j
```

Any declaration that includes an explicit initializer is a definition. An extern that has an initializer is a definition. It is an error to provide an initializer on an extern inside a function.

```c++
extern double pi = 3.1416; // definition
```

> Variables must be defined exactly once but can be declared many times.

 To use the same variable in multiple files, we must define that variable in one—and only one—file. Other files that use that variable must declare—but not define—that variable.

### 2.2.3 Identifiers

Identifiers in C++ can be composed of letters, digits, and the underscore character. Identifiers must begin with either a letter or an underscore. Identifiers are case-sensitive; upper- and lowercase letters are distinct.

*Table 2.3 C++ Keywords*

<img src="https://raw.githubusercontent.com/AnJian2020/md_picture/main/img/202111041441586.png" alt="image-20211104144105484" style="zoom:80%;" />

*Table 2.4 C++ Alternative Operator Names*

<img src="https://raw.githubusercontent.com/AnJian2020/md_picture/main/img/202111041438349.png" alt="image-20211104143828280" style="zoom:80%;" />

The identifiers we define in our own programs may not contain two consecutive underscores, nor can an identifier begin with an underscore followed immediately by an uppercase letter. In addition, identifiers defined outside a function may not begin with an underscore.

**Conventions for Variable Names**

- An identifier should give some indication of its meaning. 
- Variable names normally are lowercase—index, not Index or INDEX. 
- Like Sales_item, classes we define usually begin with an uppercase letter. 
- Identifiers with multiple words should visually distinguish each word, for example, student_loan or studentLoan, not studentloan

### 2.2.4 Scope of a Name

Most scopes in C++ are delimited by curly braces. <font color='red'>Names are visible from the point where they are declared until the end of the scope in which the declaration appears.</font>

```c++
#include <iostream>
int main()
{
    int sum = 0;
    for (int val = 1; val <= 10; ++val)
        sum += val;
    std::cout << "Sum of 1 to 10 inclusive is "
              << sum << std::endl;
    return 0;
}
```

The names defined outside a function have global scope. Once declared, names at the global scope are accessible throughout the program.

**Nested Scope**

Scopes can contain other scopes. The contained (or nested) scope is referred to as an inner scope, the containing scope is the outer scope. 

Once a name has been declared in a scope, that name can be used by scopes nested inside that scope. Names declared in the outer scope can also be redefined in an inner scope.

```c++
#include <iostream>
// Program for illustration purposes only: It is bad style for a function
// to use a global variable and also define a local variable with the same name
int reused = 42;
int main()
{
    int unique = 0;
    std::cout << reused << " " << unique << std::endl;
    int reused = 0;
    std::cout << reused << " " << unique << std::endl;
    std::cout << ::reused << " " << unique << std::endl;
    return 0;
}
```

## 2.3 Compound Types

The declarations we have seen so far have declarators that are nothing more than variable names. The type of such variables is the base type of the declaration.

### 2.3.1 References

A reference defines an alternative name for an object. A reference type “refers to” another type. We define a reference type by writing a declarator of the form &d, where d is the name being declared.

```c++
int ival = 1024;
int &refVal = ival;//refVal refers to (is anothor name for) ival
int &refVal2;//error:a reference must be initialized
```

<font color='cornflowerblue'>Ordinarily, when we initialize a variable, the value of the initializer is copied into the object we are creating. When we define a reference, instead of copying the initializer’s value, we bind the reference to its initializer.</font> <font color='red'>Once initialized, a reference remains bound to its initial object. There is no way to rebind a reference to refer to a different object. Because there is no way to rebind a reference, references must be initialized.</font>

**A Reference Is an Alias**

> <font color='red'>A reference is not an object. Instead, a reference is just another name for an already existing object.</font>

After a reference has been defined, all operations on that reference are actually operations on the object to which the reference is bound.

Because references are not objects, we may not define a reference to a reference.

**Reference Definitions**

Each identifier that is a reference must be preceded by the & symbol.

The type of a reference and the object to which the reference refers must match exactly. A reference may be bound only to an object, not to a literal or to the result of a more general expression.

```c++
int &refVal4 = 10; // error: initializer must be an object
double dval = 3.14;
int &refVal5 = dval; // error: initializer must be an int object
```

### 2.3.2 Pointers

A pointer is a compound type that “points to” another type. Pointers are used for indirect access to other objects. <font color='red'>A pointer is an object in its own right</font>. Pointers can be assigned and copied; <font color='red'>a single pointer can point to several different objects over its lifetime</font>. Unlike a reference, <font color='cornflowerblue'>a pointer need not be initialized at the time it is defined</font>. Like other built-in types, <font color='red'>pointers defined at block scope have undefined value if they are not initialized</font>.

We define a pointer type by writing a declarator of the form *d, where d is the name being defined. The * must be repeated for each pointer variable.

```c++
int *ip1,*ip2; // both ip1 and ip2 are pointers to int
double dp1,*dp2;	// dp2 is a pointer to double, dp1 is a double
```

**Taking the Address of an Object**

A pointer holds the address of another object. We get the address of an object by usin the address-of operator (the & operator).

```c++
int ival = 42;
int *p = &ival; // p is a pointer to ival, and it holds the address of ival
```

> Because references are not objects, they don't have address. Hence, we may not define a pointer to a reference.

<font color='red'>The types of the pointer and the object to which it points must match</font>. The types must match because the type of the pointer is used to infer the type of the object to which the pointer points. If a pointer addressed an object of another type, operations performed on the underlying object would fail.

**Pointer Value**

The value (the address) stored in a pointer can be in one of four states:

1. It can point to an object.
2. It can point to the location just immediately past the end of an object. 
3. It can be a null pointer, indicating that it is not bound to any object. 
4. It can be invalid; values other than the preceding three are invalid.

Although pointers in cases 2 and 3 are valid, there are limits on what we can do with such pointers. Because these pointers do not point to any object, we may not use them to access the (supposed) object to which the pointer points. If we do attempt to access an object through such pointers, the behavior is undefined. 

**Using a Pointer to Access an Object**

When a pointer points to an object, we can use the dereference operator (the * operator) to access that object:

```c++
int ival = 42;
int *p = &ival;
cout<< *p;
```

Dereferencing a pointer yields the object to which the pointer points. We can assign to that object by assigning to the result of the dereference. When we assign to *p, we are assigning to the object to which p points.

> We may dereference only a valid pointer that points to an object

**Null Pointers**

A null pointer does not point to any object. There are several ways to obtain a null pointer:

1. We can initialize the pointer by the literal nullptr. nullptr is a literal that has a special type that can be converted to any other pointer type.
2. We can initialize a pointer to the literal 0.
3. Older programs sometimes use a preprocessor variable named NULL, which the cstdlib header defines as 0

```c++
int *p1 = nullptr;//equivalent to int *p1 = 0
int *p2 = 0;	// directly initializes p2 from the literal constant 0
// must #include cstdlib
int *p3 = NULL;	//quivalent to int *p3 = 0
```

When we use a preprocessor variable, the preprocessor automatically replaces the variable by its value. Hence, initializing a pointer to NULL is equivalent to initializing it to 0.

It is illegal to assign an int variable to a pointer, even if the variable’s value happens to be 0.

```
int zero = 0;
pi = zero; // error
```

**Assignment and Pointers**

 The important thing to keep in mind is that assignment changes its left-hand operand.

```c++
pi = &ival; //value in pi is changed; pi now points to ival
```

We assign a new value to pi, which changes the address that pi holds.

```c++
*pi = 0;	// value in ival is changed; pi is nuchanged.
```

Then *pi (the value to which pi points) is changed.

**Other Pointer Operations**

Because  the pointer has a valid value, we can use a pointer in a condition. If the pointer is 0, then the condition is false.

```c++
int ival = 1024;
int *pi = 0; // pi is a valid, null pointer
int *pi2 = &ival; // pi2 is a valid pointer that holds the address of ival
if (pi) // pi has value 0, so condition evaluates as false
 // ...
if (pi2) // pi2 points to ival, so it is not 0; the condition evaluates as true
```

> <font color="red">Any nonzero pointer evaluates as true.</font>

Given two valid pointers of the same type, we can compare them using the equality (==) or inequality (!=) operators. The result of these operators has type bool. 

<font color='red'>Two pointers are equal if they hold the same address and unequal otherwise</font>. <font color='cornflowerblue'>Two pointers hold the same address (are equal) if they are both null, if they address the same object, or if they are both pointers one past the same object.</font> Note that it is possible for a pointer to an object and a pointer one past the end of a different object to hold the same address. Such pointers will compare equal.

Because these operations use the value of the pointer, a pointer used in a condition or in a comparsion must be a valid pointer.

**void\* Pointers**

The type void* is a special pointer type that can hold the address of any object. A void* pointer holds an address, but the type of the object at that address is unknown.

Some things we can do with a void* pointer:

- We can compare it to another pointer.
- We can pass it to or return it from a function.
- We can assign it to another void* pointer.

We cannot use a void* to operate on the object it addresses—we don’t know that object’s type, and the type determines what operations we can perform on the object. 

Generally, we use a void* pointer to deal with memory as memory, rather than using the pointer to access the object stored in that memory. 

### 2.3.3 Understanding Compound Type Declarations

**Defining Multiple Variables**

There are two common styles used to define multiple variables with pointer or reference type. 

- The first places <font color='red'>the type modifier adjacent to the identifier</font>. This style emphasizes that the variable has the indicated compound type.

  ```c++
  int *p1, *p2; // both p1 and p2 are pointers to int
  ```

- The second places <font color='red'>the type modifier with the type but defines only one variable per statement</font>. This style emphasizes that the declaration defines a compound type.

  ```c++
  int* p1; // p1 is a pointer to int
  int* p2; // p2 is a pointer to int
  ```

We indicate each pointer level by its own \*. That is, we write ** for a pointer to a pointer, and so on.

```c++
#include <iostream>
using namespace std;
int main()
{
    int ival = 1024;
    int *pi = &ival; // pi points to an int
    int **ppi = &pi; // ppi points to a pointer to an int
    cout << "The value of ival\n"
         << "direct value: " << ival << "\n"
         << "indirect value: " << *pi << "\n"
         << "doubly indirect value: " << **ppi << endl;
    return 0;
}
```

Just as dereferencing a pointer to an int yields an int, dereferencing a pointer to a pointer yields a pointer. To access the underlying object, we must dereference the original pointer twice.

<img src="https://raw.githubusercontent.com/AnJian2020/md_picture/main/img/202111051709007.png" alt="image-20211105170906872" style="zoom: 67%;" />

**References to Pointers**

```c++
int i = 42;
int *p; // p is a pointer to int
int *&r = p; // r is a reference to the pointer p
r = &i; // r refers to a pointer; assigning &i to r makes p point to i
*r = 0; // dereferencing r yields i, the object to which p points; changes i to 0
```

<font color='cornflowerblue'>The easiest way to understand the type of r is to read the definition right to left</font>. <font color="red">The symbol closest to the name of the variable (in this case the & in &r) is the one that has the most immediate effect on the variable’s type</font>.

 Thus, we know that r is a reference. The rest of the declarator determines the type to which r refers. The next symbol, * in this case, says that the type r refers to is a pointer type. Finally, the base type of the declaration says that r is a reference to a pointer to an int.

> It can be easier to understand complicated pointer or reference declarations if you read them from right to left.

## 2.4 const Qualifier

We can make a variable unchangeable by defining the variable's type as const.

```c++
const int bufSize = 512;	// input buffer size
```

<font color='red'>Because we can’t change the value of a const object after we create it, it must be initialized</font>. <font color='cornflowerblue'>As usual, the initializer may be an arbitrarily complicated expression</font>.

```c++
const int i = get_size(); // ok: initialized at run time
const int j = 42; // ok: initialized at compile time
const int k; // error: k is uninitialized const
```

**Initialization and const**

Among the operations that don’t change the value of an object is initialization— when we use an object to initialize another object, it doesn’t matter whether either or both of the objects are consts.

```c++
int i = 42;
const int ci = i; // ok: the value in i is copied into ci
int j = ci; // ok: the value in ci is copied into 
```

The constness of ci matters only for operations that might change ci. Copying an object doesn’t change that object. Once the copy is made, the new object has no further access to the original object.

**By Default, const Objects Are Local to a File**

When a const object is initialized from a compile-time constant, the complier will usually replace uses of the variable with its corresponding value during compilation.

<font color='red'>Yet avoid multiple definitions of the same variable, const variables are defined as local to the file</font>. When we define a const with the same name in multiple files, it is as if we had written definitions for separate variables in each file.

Sometimes we have a const variable that we want to share across multiple files but whose initializer is not a constant expression. In this case, we don’t want the compiler to generate a separate variable in each file. Instead, we want the const object to behave like other (nonconst) variables. <font color='red'>We want to define the const in one file, and declare it in the other files that use that object</font>.

To define a single instance of a const variable, we use the keyword extern on both its definition and declaration(s).

```c++
// file_1.cc defines and initializes a const that is accessible to other files 
extern const int bufSize = fcn();	// definition
// file_1.h
extern const int bufSize; // same bufSize as defined in file_1.cc declaration
```

> <font color='red'>To share a const object among multiple files, you must define the variable as extern.</font>

### 2.4.1 References to const

 To do so we use a reference to const, which is a reference that refers to a const type. Unlike an ordinary reference, a reference to const <font color='red'>cannot</font> be used to change the object to which the reference is bound.

```c++
const int ci = 1024;
const int &r1 = ci; // ok: both reference and underlying object are const
r1 = 42; // error: r1 is a reference to const
int &r2 = ci; // error: non const reference to a const object
```

> const Reference is a Reference to const.

 Whether a reference refers to a const or nonconst type affects what we can do with that reference, not whether we can alter the binding of the reference itself.

**Initialization and References to const**

There are two exceptions to the rule that the type of a reference must match the type of the object to which it refers:

1. We can initialize a reference to const from any expression that can be converted to the type of the reference.
2. We can bind a pointer of reference to a base-class type to an object of a type derived from that base class.

A temporary object is an unnamed object created by the compiler when it needs a place to store a result from evaluating an expression.

```c++
const int temp = dval; // create a temporary const int from the double
const int &ri = temp; // bind ri to that temporar
```

The reason that we can't initialize a reference to an int from a variable of type double:

If ri weren’t const, we could assign to ri. Doing so would change the object to which ri is bound. That object is a temporary, not dval. The programmer who made ri refer to dval would probably expect that assigning to ri would change dval. After all, why assign to ri unless the intent is to change the object to which ri is bound? Because binding a reference to a temporary is almost surely not what the programmer intended, the language makes it illegal.

**A Reference to const May Refer to an Object That Is Not const**

It is important to realize that a reference to const restricts only what we can do through that reference. Binding a reference to const to an object says nothing about whether the underlying object itself is const.

### 2.4.2 Pointers and const

A pointer to const may not be used to change the object to which the pointer points. We may store the address of a const object only in a pointer to const.

```c++
const double pi = 3.14; // pi is const; its value may not be changed
double *ptr = &pi; // error: ptr is a plain pointer
const double *cptr = &pi; // ok: cptr may point to a double that is const
*cptr = 42; // error: cannot assign to *cptr
```

There are two exceptions to the rule that the types of a pointer and the object to which it points must match:

1. We can use a pointer to const to point to a nonconst object.
2. We can bind a pointer or reference to a base-class type to an object of a type derived from that base class.

```c++
double dval = 3.14;
cptr = &dval;
```

**const Pointers**

Like any other const object, a const pointer must be initialized, and once initialized, it's value(the address that it holds) may not be changed. . We indicate that the pointer is const by putting the const after the *. This placement indicates that it is the pointer, not the pointed-to type, that is const.

```c++
int errNumb = 0;
int *const curErr = &errNumb; // curErr will always point to errNumb
const double pi = 3.14159;
const double *const pip = &pi; // pip is a const pointer to a const object
*pip = 2.72; // error: pip is a pointer to const
// if the object to which curErr points (i.e., errNumb) is nonzero
if (*curErr) {
 errorHandler();
 *curErr = 0; // ok: reset the value of the object to which curErr is bound
}
```

The fact that a pointer is itself const says nothing about whether we can use the pointer to change the underlying object. Whether we can change that object depends entirely on the type to which the pointer points. 

### 2.4.3 Top-Level const

We use the term top-level const to indicate that the pointer itself is a const. When a pointer can point to a const object, we refer to that const as a low-level const.
