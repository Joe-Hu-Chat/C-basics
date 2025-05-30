C++ 20

1. Hello World in C++

2. Object-Oriented Programming Fundamentals
- classes and objects: 
  - model `real-world entities`
  - encapsulate `data`
  - define `behaviors` in an organized manner
- encapsulation, inheritance, and polymorphism
  - Compile-Time Polymorphism: Function `Overloading`, Operator Overloading
  - Run-Time Polymorphism: Function `Overriding` and `virtual function`
  - Advantage: Code reusability, Modularity, Flexibility
  practice OOP concepts

3. Advanced Features and Memory Management
- `new` and `delete`
  - C++ `operators`, allocate from Free Store in Heap memory, can be help or static area, depends on operator new implementation
  - `new`: call `malloc` to get space, and then call `constructor` to create object
  - `delete`: call `destructor` to clean up resources, and then call `free` to release space
- RAII (Resource Acquisition Is Initialization) principles
  - objects own resources, acquires when initialized and releases when destructed
- smart pointers `std::unique_ptr`, `std::shared_ptr`
  - Smart pointers are designed to be as efficient as possible both in terms of memory and performance
  - For example, the only **data member** in `unique_ptr` is the encapsulated pointer.
  - This means that `unique_ptr` is exactly as the same size as that pointer
  - Accessing the encapsulated pointer by using the smart pointer overloaded `*` and `->` operators is not significantly slower than accessing the `raw pointers` directly.
  - `unique_ptr.reset()`: releases ownership of the pointer, which frees the memory before going out of scope
  - `unique_ptr.get()`: Get the `raw pointer` underlying the smart pointer
  - `unique_ptr`: allows exactly **one owner** of the underlying pointer, default choice, moved to a new owner
  - `shared_ptr`: Reference-counted, multiple owners, 2 data members: pointer and ref-counter, copyable and assignable
  - `weak_ptr`: In conjunction with `shared_ptr`, but not participate in reference counting
  - `make_unique<*>`, `make_shared<*>`: Creation of smart pointers
  - `move()`: Transfer Ownership, change left-value to right-value
```
std::unique_ptr<int> p1 = std::make_unique<int>(10);
std::unique_ptr<int> p2 = std::move(p1); // p1 is now nullptr
```

```
std::shared_ptr<int> p1 = std::make_shared<int>(10);
std::shared_ptr<int> p2 = p1; // Reference count increases
std::weak_ptr<int> p3 = p1; // No ref-count increase
if (auto temp = p3.lock()) { // Use `.lock` to obtain a `shared_ptr`, if still exists
	// Safe to use *temp
}
```

Practice creating and managing objects dynamically

4. Standard Template Library (STL)

Templates: `template <typename T>`
Template specialization: `template<> class Name<type> {}`

- STL containers: `vector`, `list`, `stack`, `queue`, `map`, `set`
  - class templates, handle memory allocation and deallocation automatically
  - Sequential Containers, Container Adapters, Associative Containers, Unordered Containers
- algorithms: `sort`, `copy`, `max_element`, `find`, `for_each`
  - Function overloading to work with different types of input parameters
- `iterators`, how they work with STL containers
  - similar to pointers, pointing to elements
  - `vector<T>::iterator` is a nested type in the class template
  - <iterator>: header file contains iterators definition
- `Functors`: STL Function `Objects`, behave like a function
  - Defined in <functional> header file
  - Due to the overloading of the `()` parenthesis operator
  - `equal_to`, `not_equal_to`, `greater`, `less`, `plus`, `minus`

program to manipulate data using STL
- STL Cheat Sheet: https://www.geeksforgeeks.org/cpp-stl-cheat-sheet/
- Try small problems using STL containers and algorithms
  - https://www.techgig.com/practice/cpp/stl

STD lib:
- pair template, std::make_pair()

5. Modern C++20 Features
One of the most significant updates to the C++ language since C++11
- **Concepts**: Constrained templates, help catch template misuse at compile time
- **Ranges library**: Simplify working with collections of data
- **Coroutines**: For asynchronous programming
- **Modules**: Replace header files for better modularity

Implement small examples to understand these features practically

cheatsheet: https://geanmar.com/posts/cpp-cheat-sheet/

6. File I/O, Error Handling, and Multithreading
- file handling using streams: `ifstream` (Input), `ofstream` (Output), `fstream` (Both)
- exception handling: `try`, `catch`, and `throw`
  - Types of Exceptions to catch:
  - Built-in Types (int, char, double...)
  - Standard exceptions from C++ std (std::exception, std::runtime_error...)
  - Custom exceptions (user-defined classes or structs)
- basic multithreading concepts using the <thread> library
program to read/write files and implement basic multithreading

7. Practice and Build Projects
Consolidate knowlege by working on small projects
- simple bank account management system using OOP
- multithreaded program to calculate prime numbers
- use STL to build a mini text-based game or data processing tool

## `iostream`
In C++, the `iostream` library is a fundamental part of the `standard library` that facilitates input and output (I/O) operations. It provides `classes and objects` for handling data streams, enabling interaction with the `console`, `files`, and `memory` in a structured and effcient manner.

- **cin**: Standard input stream for reading user input
- **cout**: Standard output stream for displaying data
- **cerr**: Standard error stream for unbuffered error messages
- **clog**: Standard error stream for buffered logging

`>>`: **Extraction operator**, used with `cin` to retrieve input from the user or other sources
`<<`: **Insertion operator**, used with `cout` to output data to the console or other dest.
`endl`: **Manipulator**, insert a newline and flush the output buffer
`\n`: newline character, without flushing the buffer

The iostream library operates through a hierarchy of classes:
- **ios_base**: Base class defining common properties of all streams, such as state flags
- **istream**: Handles input operations using `cin` and other input streams
- **ostream**: Handles output operations using `cout` and other output streams
- **iostream**: Combines istream and ostream functionalities for bidirectional I/O
