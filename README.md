# Memory-management-in-Cplusplus

Draft.

## 1. Never pass a pointer when a reference will do
That's actually pretty simple, so on to no. 2.
## 2. As much as possible, use the stack, not the heap
Hum, another obvious one. On to no. 3.
## 3. Utilize STL classes to organize any allocated memory
Once again, pretty straight forward. See how easy this is?
## 4. Only allocate classes, with an exception...
A class may internally allocate memory for basic structures such as char [], but that data structure is to be kept hidden from other classes. Typically STL will make this unnecessary, but there may be special cases.
## 5. Create a class (or classes) who's only job it is is to manage heap memory for a single purpose

I will finish this later
