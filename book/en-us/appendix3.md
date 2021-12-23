# 31 nooby C++ habits you need to ditch
https://youtu.be/i_wDa2AS_8w

1. `using namespace std;`
	1. don't do it in the header file
	2. `using std::string, std::cout`;
2. use `std::endl` in a loop
	1. it flushes the buffer. thus should use `"\n"`
3. iterate using index
	1. use `for(const auto& x: vec)`
4. rewriting std algo
	1. find positive: 
	2. `std::find_if(data.cbegin(), data.cend(), [](const auto& x){return x  > 0;});`
5. use c style array
	1. `template <std::size_t size>`
	2. `void f_arr(std::array<int, size> &arr)`
6. any use of `reinterpret_cast`
	1. the only we allowed to do with the result is to `reinterpret_cast` back
	2. use `static_cast` instead
7. cast away const using `const_cast`
	1. instead, for `std::map`, don't use `m[x]` but use const access `m.at(x)`
8. not knowing map bracket inserts element
9. ignoring const-correctness
	1. mark parameter as const whenever it should be
10. not knowing string literal lifetime
	1. entire life time lvalue
11. not using structured bindings
	1. `for(const auto&[name, hex]: mcolor)`
12. out-params instead of returning a struct
13. not using `constexpr`
	1. use it in function return type for compile time calculations
14. forgetting to mark destructor virtual: it will only call base destructor
15. thinking class members init in order of init list
	1. they actually in order of class member declarations
16. not knowing about default vs value initialization
	1. default initialization: using default constructor, may contain garbages
		1. `int x;`
		2. `int *x = new int`
	2. value initialization:
		1. `int y{};`
		2. `int* y = new int{}`
		3. `int* y = new int()`
17. MAGIC NUMBERS
	1.  use `constexpr` with good name
18. modifying a container while looping over it
	1.  `auto x: v` will use the `end()`, which may change when adding new elements
	2.  use index instead
19. returning `std::move` of a local
	1. compiler will always do return value optimization for local variables
20. thinking `std::move` moves something
	1.  it just cast to rvalue reference
21. thinking evaluation order is left to right
22. unnecessary heap allocations
	1. stack may be enough
23. not using `std::unique_ptr` and `std::shared_ptr`
24. not using `std::make_unique` and `std::make_shared`
25. any use of `new` or `delete`
26. any manual resource management
	1. use `std::ifstream` instead of `FILE`
	2. RAII: Resource Acquisition Is Initialization
27. thinking raw pointers are bad
	1. if the ownership is not a concern of the function, just use raw pointers
	2. if the pointer is coming from some c function, use self-defined Deleter
		1. `std::unique_ptr<int, CustomFreeDeleter>(some_c_function())`
28. using shared ptr when unique ptr would do
	1. `unique_ptr` can be easily moved to `shared_ptr` or just assign to it.
29. thinking shared ptr is thread-safe
	1. only reference counting is atomic and thus thread-safe
30. mixing up const ptr vs ptr to const
	1. const applies to right, unless no right identifier
31. ignoring compiler warnings
