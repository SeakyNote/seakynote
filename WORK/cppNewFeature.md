## Often

- long long
- list initialization
  - int num{1};
  - vector<int> vec{1,2,3};
- nullptr
- alias declaration
  - using AA = BB;
- auto
- range for
- emplace/emplace_front/emplace_back
- to_string/stoi/stod
- lambda expression
- unordered_map/unordered_set
- shared_ptr/unique_ptr/weak_ptr
- =delete
- explicit
- override
- final
- enum class
- Forward Declarations for Enumerations

## Normal

- constexpr & constexpr function
- decltype
- in-class initializer
  - https://blog.csdn.net/m0_57168310/article/details/126746229
- cbegin/cend
- iterator begin/end (get begin&end for array)
- sizeof XXXCls::member
- initializer_list
- `int (*func(int i))[10];` equals `auto func(int i)->int(*)[10];`
- = default
- delegating constructor
- constexpr constructor
- array/forward_list
- std::swap
- shrink_to_fit
- bind
- std::move
- rvalue reference
- tuple
- bitset

## Rare

- move constructor/move-assignment operator
- move iterator
- reference qualifier &/&&
- function<T>
- inherited constructor(using Base::Base)
- extern template
- Reference Collapsing
- std::forward
- variadic template
- sizeof...
- regex
- default_random_engine
- hexfloat/defaultfloat
- noexcept
- inline namespace
- enum XXX:type
- mem_fn