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

Table 2.4 C++ Alternative Operator Names

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

