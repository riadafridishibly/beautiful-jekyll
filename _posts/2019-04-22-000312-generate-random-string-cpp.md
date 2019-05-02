---
published: true
title: Generate Random String in C++
layout: post
comments: true
author: Riad Afridi Shibly
tags: [c++]
permalink: '/posts/generate-random-string-c++/'
---

## Start with random number

Random String! Generating random string is important. There is various way to generate random string. I'm going to show you the standard library approach. First of all let's generate some random numbers. 

## C style random number generator

We more or less used this approach to generate random number.

```cpp
#include <cstdio>
#include <ctime>
#include <iostream>

int main() {
    std::srand(std::time(nullptr));
    std::cout << std::rand() << '\n';
}

```

## C++ way is wordy but OK

But in C++11 some wordy syntax was added to confuse people. Let's learn to use that.


```cpp
#include <random>
#include <iostream>

int main() {
    std::random_device rd;
    std::mt19937 generator(rd());

    std::cout << generator() << '\n';
}
```

But what if we need to generate in range $[a, b]$. Simple. But again wordy syntax.


```cpp
#include <random>
#include <iostream>

int main() {
    std::random_device rd;
    std::mt19937 generator(rd());

    std::uniform_int_distribution<> dis(10, 20);
    std::cout << dis(generator) << '\n';
}
```

It'll generate random numbers between 10 and 20. Inclusive. OK, now we can move forward.

## Generate random string

Let's create a function which will accept length of a string as parameter and return a random string.

```c
std::string random_string(std::size_t size) {
    auto gen = []() {
        static const std::string ALLCHARS(
            "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz");
        static std::random_device rd;
        static std::mt19937 generator(rd());
        static std::uniform_int_distribution<> dist(0, std::size(ALLCHARS) - 1);
        return ALLCHARS[dist(generator)];
    };

    std::string res(size, ' ');

    std::generate(std::begin(res), std::end(res), gen);

    return res;
}
```

And that's it. I've used a lambda here. And generate function. It's actually simple to use.
