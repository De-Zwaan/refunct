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
StructName = Struct {
    field1: type = <default_value>,
    field2: type,
}

/// Bitflags to increase ease of use in embedded situations
RegisterName = Struct {
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
function_name = (type, type) -> type {
    (1, b) => {
        // Expression
    }
    (a, b) => {
        // Expression
    }
}

/// Constant functions and expression to be evaluated at compile-time
const_function_name = (const type) -> type {
    a => {
        // Constant expression
        3 * a
    },
}

/// Currying
f = function(b, _, _); // This will return a curried function 
// This results in the same:
f = b.function(_, _);

/// Mapping
a = b#function(c);
d = b#(x => x + 1);

/// Enums/Monads
Option<T> = Enum {
    Some(T)
    None
}
```

Merge sort:
```
// Main function, the entry point of the program. 
// Cannot be called. 
// Returns nothing.
main <= () {
    // Define the list to be sorted
    list <= [4, 3, 0, 10, 3, 7, 8];

    // Note that the call signature of functions can be f(a, b) or a.f(b)
    sorted <= list.merge_sort();
    std::print(sorted.to_string());
}

/* 
 * Functions are defined the same way as variables, where they are assigned
 * to a symbol. This function takes in a single parameter, a list of objects
 * of type A, where A implements the Ord trait and returns a list of objects
 * of type A, where A implements the Ord trait.
 * 
 * Then the parameters are patten matched (a bit like Haskell, the first line 
 * matches if the list is empty. The second patten matches if the list contains
 * a single item. The last pattern matches if the other two patterns don't
 * match. The pattern matching needs to be exhaustive.
 * 
 * If a line does not end with a semicolon, the result from the line gets
 * returned (like Rust).
 */
merge_sort = [A<Ord>] -> [A<Ord>] {
    []  => [],
    [a] => [a],
    list  => { 
        (left, right) <= as.splitAt(list.len() / 2);
        merge(left.merge_sort(), right.merge_sort())
    },
}

// Like the previous function, but with more arguments.
merge <= ([A<Ord>], [A<Ord>]) -> [A<Ord>] {
    ([], b) => b,
    (a, []) => a,
    (a, b) if a[0] <= b[0] => a[0] ++ merge(a[1:], b)
    (a, b)                 => b[0] ++ merge(a, b[1:])
}
```
