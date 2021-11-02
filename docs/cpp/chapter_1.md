# Chapter 1.Getting Started

## 1.1 Writing a Simple C++ Program

Every C++ program contains one or more functions, one of which must be named main. The operating system runs a C++ program by calling main. Here is a simple version of main that does nothing but return a value to the operating system.

```c++
int main()
{
    return 0;
}
```

<font color='red'>**Four elements: a return type, a function name, a (possibly empty) parameter list enclosed in  parentheses, and a function body.**</font>

The main function is required to have a return type of int. A return value of 0 indicates success. A nonzero return indicates what kind of error occurred.

1.1.1 Compiling and Executing the Program

## 1.2 A First Look at Input/Output

&nbsp;&nbsp;&nbsp;&nbsp;Fundamental to the iostream library are two types named istream and ostream, which represent input and output streams, respectively. A stream is a sequence of characters read from or written to an IO device. 

&nbsp;&nbsp;&nbsp;&nbsp;The library defines four IO objects. To handle input, we use an object of type istream named cin (pronounced see-in). This object is also referred to as the standard input. For output, we use an ostream object named cout (pronounced see-out). This object is also known as the standard output. The library also defines two other ostream objects, named cerr and clog (pronounced see-err and see-log, respectively). We typically use cerr, referred to as the standard error, for warning and error messages and clog for general information about the execution of the program.

