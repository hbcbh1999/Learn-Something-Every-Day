# [CS247: Software Engineering Principles](https://www.student.cs.uwaterloo.ca/~cs247/current/general.shtml)
Software Engineering is a collection of practices and priciples, tools, techniques, etc. that aims to:
- imporve software quality
- improve developer productivity
- `g++ -5 -std=14 -Wall`
- overloading vs overriding

### [ADT Design](https://www.student.cs.uwaterloo.ca/~cs247/current/Lectures/02ADTDesign-1up.pdf)
- user defined type, bundles together the range of possible values stored, and operations that can manipulate the varible
- provides compiler ways to perform type assertions at compile time
- allows implementations to be swapped out without affecting code

#### Operator Overloading
- fi

C++ 11 introduced "move" semantics
- compilers have return value optimization, saving the cost of a copy, when returning a temporary object, holding a function return value
  - copies can be expensive for large objects (omiting storage of temp object)
- move constructor subroutine

#### Non-member
A Non-member function is a critical function of the ADT that is declared outside of the class
- reduces the number of functions with direct access to private data members
- streaming operators `<<` and `>>` act on the stream object, returning a modified stream so that operations are chained
```cpp
// this friend function is a problem! If the implementation changes, this needs to as well!
ostream& operator<< (ostream &os, const Rational &r) {
  const char slash = '/';
  os << r.numerator_ << slash << r.denominator_;
  return os;
}

istream& operator>> (istream &is, RationalNumber &r) {
  int num, den; char slash;
  is >> num >> slash >> den;
  if (is.fail()) return is;
  r = RationalNumber(num, den);
  return is;
}
```

What has to be a member?
- accessors + mutators, constructors, destructor, copy/move
- assignment, [] 
- virtual methods

What cannot be a member?
- I/O operations, or operations that don't want first argunment to be the class type 
  - think stream operations and type conversions
  
We always prefer non-member and non-friend
- less code affected when implementations change
- more secure since they are forced to use accessors & mutators

#### Type Coversions
Type conversions will lose private data

How does a compiler find a conversion function?

1. with exact matches
2. lossless conversion via "promotion" (bool to int, char to int, float to double)
3. standard converson (double to int)
4. user-defined conversions

We have defined some level of precedence, but if there are two or more matches at the same level, the compiler will throw an error because the choice is ambiguous
- if one function is better for at least one argument, and same for the rest, then it will win

Implicit Type Conversions:
```
class X { public: X(int); X(string) };
class Y { public: Y(int) };
class Z { public: Z(X); };
X f(X);
Y f(Y);
Z g(Z);
X operator+ (X,X);

// now for resolution:
strings { "MACK" };
f(X(1)); // X(1) give X; f recieves X and outputs X; OK
f(1); // ERROR: f is looking for X type, not int
g(X(s)) // OK
g(Z(s)) // OK
```

### Modules and Interfaces

### Exceptions

### Interface Specifications

### OO Design Principles

### Design Patterns

### UML Modelling

### Generic Programming(STL)

### Testing and Debugging