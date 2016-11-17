# Memory Management in C++

Memory leaks can be a big problem, they are one of the main reasons people fear and avoid C++. Follow these simple rules and you might just never have a memory leak in your C++ code ever again. Or if you do, is will be easy to find.

## 1. Never pass a pointer when a reference will do
That's actually pretty simple, so on to no. 2.
## 2. As much as possible, use the stack, not the heap
Another obvious one, keep reading.
## 3. Make use of the Standard Template Libary to store anything you allocate
If you allocate it, manage it utilizing an STL class.
## 4. Generally only allocate classes, not basic data types
If you find you need to make use of basic data types (for example double[]) then encapsulate it in a class and keep it away from prying eyes. And stick to the next rule.
## 5. Create classes who's individual jobs are to manage heap memory for specific purposes
An example to demonstrate.

Imagine you need to manage the real-time state of some game players, and this code needs to be super fast, so the decision has been made to keep this data in memory. Let's say we have two classes, one called User and another called UserManagement. Only one instance of UserManagement will be instantiated and it will most likely be around for the life of the program. 

Only UserManagement is allowed to create, and destroy User objects. Let's call UserManagement UM for short. Only UM is allowed to keep a non-stack reference to a User object. When UM goes away, so do all User objects. UM will (probably) use of a list or map to store User objects, with a mutex to protect access (to the list or map).

What about updates to User objects, or bits of the program that want to pass User objects to other bits of the program? It depends on overall design and such, but let's consider some general strategies.

UM could manage updates, that way UM can insure thread safe access to the User objects. Or perhaps another class working closely with UM could take on the task of updating the User objects.

So what happens when various functions starts passing User objects around. These functions must honor the rules for updates, and they must not attempt to somehow store references (to Users) past the functions own lifetime.

Best would be to make use of copies. When asking for a user data, the caller could pass in a reference to a (stack-allocated) User object that UM would then fill-out and return.

[I'm not saying copy this exact design for your game: it's just an illustration. Caveat emptor.]

Well, there you have it. Follow these rules and you can tell your (programming) friends "Real programmers don't need garbage collectors!"
