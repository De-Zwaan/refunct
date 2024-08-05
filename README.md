# ReFunct
ReFunct is a primitive attempt at a functional programming language, inspired by the syntax of Rust.

It is mostly meant as a learning opportunity for myself, especially in the design of a language, writing a compiler and all the associated aspects.

# Requirements
I want the language to be as 'functional' as possible, such that there are no internal states. 

I would like:
1. smooth integration with C.
2. granular memory control for embedded applications.
3. 

# Syntax
To be easy to use, the syntax will look a lot like (modern) languages like C++, Rust and Zig.

## Example
```
/// Structs (with default values)
struct StructName {
    field1: type = <default_value>,
    field2: type,
}

/// Bitflags to increase ease of use in embedded situations
bitflags RegisterName {
    enable: b1,
    read: b1,
    config: b3 {
        QUICK_CONFIG = 0;
        ...
        SLOW_CONFIG = 7;
    },
    write: b1,
}

/// Functions
fn function_name(parameter1: type, parameter2: type) -> type {
    // Expression    
}

/// Constant functions and expression to be evaluated at compile-time
const fn function_name(parameter1: const type) -> type {
    // Constant expression
}

/// Currying
var f = function(b, _, _); // This will return a function with the first argument already specified

/// Mapping
var a = b#function(c);
var d = b#(x => x + 1);

// Enums/Monads
enum Option<T> {
    Some(T)
    None
}
```
