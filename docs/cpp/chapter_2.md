# Chapter 2.Variables and Basic Types

## 2.1 Primitive [Built-in](内置) Types

The arithmetic types represent <font color='red'>characters, integers, boolean values, and floating-point numbers</font>. Primitive built-in types also includes a special type named <font color='red'>void</font>.

### 2.1.1 Arithmetic Types

Two categories: **integral types**(which include character and boolean types) and **floating-point types**.

*Table 2.1. C++: Arithmetic Types*

​    <img src="https://raw.githubusercontent.com/AnJian2020/md_picture/main/img/202111021226545.png" alt="image-20211102122619366" style="zoom:67%;" />


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

By default, decimal literals are signed whereas octal and hexadecimal literals can be either signed or unsigned types. 