# C++ Codeforces Template

Template of C++ that I use in [Codeforces](https://codeforces.com/profile/FrankS "My codeforces profile") contests. 

Debugging in competitive programming (CP) is hard. But there are several attempts have been done to ease this process. 
Some people, including some top CP-ers, have spent their time writing some code, so-called **debugging templates**.
These pieces of code are often used to print out some variables value in the code.

### 1. Lambda function

C++11/14 lambdas do not encourage recursion: there is no way to reference the lambda object from the body of the lambda function.
So it propose adding to the standard library a std::y_combinator function that enables the following fast and clean code, free from the some problems:

```c++
#include <functional>
#include <iostream>

int main() {
    auto gcd = y_combinator([](auto gcd, int a, int b) -> int {
        return b == 0 ? a : gcd(b, a % b);
    });
    cout << gcd(20, 30) << nl;
}
```

The proposal is a pure library extension. It does not require changes to the standard components. The extension can be implemented in C++11 and C++14.

### 2. The printing functions

Not everything can be printed to std::ostream (yet). But lucky for us, with the power of C++, we add overloading functions for printing what every type we like (except what already has that function).

I only add 3 more basic printing functions, which are for `std::pair`, `std::tuple` and general container (`std::vector`, `std::list`, `std::set`, `std::map`, etc. ), except for `std::string` because it already existed.

I think demonstration is better in this case:

```c++
// simple pair
pair<int, string> a = {123, "abc"};
dbg(a);

// simple vector
vector<int> b = {2, 4, 6, 8};
dbg(b);

// vector with pair
vector<pair<int, int>> c = { {1, 2}, {2, 4}, {4, 6} };
dbg(c);

// map
map<string, double> length_unit = {
    {"m", 1},
    {"cm", 0.01},
    {"mm", 0.001},
    {"km", 1000}
};
dbg(length_unit);

// tuple
dbg(make_tuple(1, 2, 3, 'a', 'b', 'c'));
dbg(make_tuple(a, b, c));

// set of vector
set<vector<int>> s = {
    {1, 2, 3, 4, 5, 6},
    {1, 1, 2, 3, 5, 8},
    {1, 4, 9, 16, 25, 64},
};
dbg(s);
```

And the output to stderr:

```
(a): (123, abc)
(b): {2, 4, 6, 8}
(c): {(1, 2), (2, 4), (4, 6)}
(length_unit): {(cm, 0.01), (km, 1000), (m, 1), (mm, 0.001)}
(make_tuple(1, 2, 3, 'a', 'b', 'c')): (1, 2, 3, a, b, c)
(make_tuple(a, b, c)): ((123, abc), {2, 4, 6, 8}, {(1, 2), (2, 4), (4, 6)})
(s): {{1, 1, 2, 3, 5, 8}, {1, 2, 3, 4, 5, 6}, {1, 4, 9, 16, 25, 64}}
```

### 3. Other stuff

Definitions like `ll` for `long long` type, `pi` for `vector<int>` type, and the generic `pqg` for priority queue. How cool are those!

Definitions for `for` loop in containers: `fornm(i,n,m)` describe a for loop from `n` to `m` exclusive

### 4. ... 