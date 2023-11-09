---
layout: post
title: Coding a palindrome checker in C
description: As a C++ newbie, I try my hands at coding a palindrome checker in C, exploring different approaches with computational thinking.
date: 2023/10/28 17:56
author: alice
image: "https://cdn.midjourney.com/4ce62b6e-b0de-4efd-97b7-ebb39db54fee/0_3.webp"
tags: [coding, C++]
tags_color: "#d46827"
featured: true
---

As I might have told you, I am a C++ newbie and more generally a superstar coding noob 👑. While I enjoy the title, I know that I really need to get better if I want my video game to ever see the light of day. So lately, I decided to open my JavaScript homework books to apply them to C++. I already went through learning basic data types, if/else statements and loops, and I am now working on the “while loop” exercise.

Suffice to say, that little brain of mine was hesitant to even try. I knew that I was able to solve this exercise since I’ve done it before with JavaScript, but I couldn’t remember how I did it the first time. It was a fun exercise though, and I thought I’d share my solution on this worldwide newsfeed.

## The instruction

- Using a while loop, the program must determine whether or not the word is a palindrome, i.e. whether it reads the same forwards and backwards. An example of a palindrome is the word “racecar”.
- Output the given word and whether or not it is a palindrome, e.g. “racecar is a palindrome”

## My approach

Solving this problem had me go through different phases and explore two possibilities.

### Checking character by character

First, I tried to compare each character from the start and end, so that while we go through every character, we check if they are different or not. If we find a case where characters don’t match, then it is not a palindrome. We have to assign “isPalindrome = false” and break the while loop and progression.

```cpp
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

int main() {
    const char *inputWord = "racecar";
    int length = strlen(inputWord);
    bool isPalindrome = true;

    int start = 0;
    int end = length - 1;

    while (start < end) {
        if (inputWord[start] != inputWord[end]) {
            isPalindrome = false;
            break;
        }
        start++;
        end--;
    }

    if (isPalindrome) {
        printf("%s is a palindrome\n", inputWord);
    } else {
        printf("%s is not a palindrome\n", inputWord);
    }

    return 0;
}
```

### But… let’s do some computational thinking

I just think it is so interesting how computational thinking aids in selecting from various problem-solving approaches. At first, I just tried to answer the problem literally but something felt off. I didn’t really liked the `break`, since the point of the `while` loop is to end things for us when a condition isn’t met. Also, creating a boolean to check the status of the word meant that… there should be a function somewhere!! The `isPalindrome` boolean didn’t seems so right. So I started to take some other steps.

1. **Problem Decomposition**: In how many steps can I break down the problem? Breaking a problem into smaller manageable steps can help, even problems as trivial as this one. It allows me to organize my thoughts and provides an overview of the steps needed to reach a solution. Like when you read a recipe in its entirety, you can see when something isn’t right - a step may be overlooked or unnecessary.
2. **Pattern Recognition:** It may seem simplistic, but for people like me, it's not immediately clear. The solution to this problem involves recognising the pattern of a palindrome. This requires comparing characters at **mirrored** positions within the string, starting from the outside and working inwards. It's important to note the distinction between **mirrored** and **reversed**. When something is mirrored, there's a central point reflecting what's on the outside. In contrast, something reversed is read backwards in a linear manner. If I misconstrue the problem by being too literal and think a palindrome should read in reverse, I would miss the pattern - which I did at first.
3. **Pattern Abstraction:** After identifying the pattern, I realised a portion of the code could be abstracted into a function. Isolating the `isPalindrome` section enhances clarity and modularity, separating it from the output, which is an independent functional requirement.
4. **Algorithm Design:** How can we improve algorithm design? Different solutions exist for the same problem, but it's our job to determine which solution is more elegant or efficient. Design decisions can improve coherence and readability in larger codebases. For example, a `break` in the middle of a `while` loop might not appear optimal to me, but it could be in a different context. In this case, the results of my two solutions will be as efficient, since the output will be the same. But my own readability is priority here since I am the only one working on this code and that I can easily get confused 😅.

### Progressing to the middle

So I rewrote the program as so:

Here, we progress through the string and ask the while loop to stop as soon as compared letters aren’t the same. Then we only have to check the progression: did we reach the center of the string or did the program end before? That would be our truthy / falsy check, making isPalindrome a functional checking function! 😋

```cpp
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

bool isPalindrome(const char *word) {
		// We start with similar indexes
    int32_t endIndex = strlen(word);
    int32_t startIndex = 0;

		// But we ask the while loop to end things before they get ugly
    while (startIndex < endIndex && word[startIndex] == word[endIndex - 1]) {
        startIndex++;
        endIndex--;
    }

		// Which allow us to compare indexes and return a boolean statement
    return startIndex >= endIndex;
}

int main() {
    const char inputWord[] = "racecar";

		// Then we call our super Palindrome checker!
    if (isPalindrome(inputWord)) {
        printf("%s is a palindrome\n", inputWord);
    } else {
        printf("%s is not a palindrome\n", inputWord);
    }

    return 0;
}
```

## Tadaa!

In conclusion, I want to reiterate that I am just a newbie in the world of coding and C++. There are many ways to solve this palindrome problem, and certainly more efficient and complete methods than the ones I have shown here. This article is simply a reflection of my own experiences and the way I approach coding problems at this early stage of my learning journey. As I continue on this path, I remain open to feedback and eager to learn new techniques. I will probably come back later to this code and think “what did I even write that?!” 😁 but hey, this is a learning process, so don’t forget to keep it fun ✨
