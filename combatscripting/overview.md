# Scripting for CTFs - Overview

This originally started as a tutorial series on the Nandy Narwhals
[blog](https://nandynarwhals.org). What follows is the original foreword.

## Foreword

In the interest of developing and improving the scripting skills useful for
Capture the Flag competitions of beginners who are not exactly new to
programming but have no idea how to start doing the On-the-Fly hacks required,
the Nandy Narwhals have decided to begin writing a series of tutorials to
address this need. This is especially directed at students of the [Dip. in
Infocomm Security Management Course at Singapore Polytechnic](http://sp-dism.blogspot.sg/)
who learn the basics of programming basic applications but run into difficulties
dealing with solving problems requiring quick and dirty tricks favouring speed
over robust design.

Now, our usual approach to teaching these students our methodology in tackling
CTF challenges involves forcing them to learn a language we prefer over one they
already know (i.e. Python) before actually getting into the gritty and useful
content. So, we've decided to swap out this approach for something that might
work better: introducing an objective (such as "opening a TCP socket and
receiving data") at the high level and then demonstrating the implementation in
multiple languages such as Java and C which should be more familiar to DISM
students to make making the connection easier.

To benefit from these tutorials, we recommend that you are familiar with at
least one of the languages. Do note that we will be primarily using Python 2,
unless otherwise stated.

Let's demonstrate this.

## Hello World!

A simple Hello, World! program done in Python, Java, C, Perl, and Ruby. Output
should look something like this:

```shell
$ python helloworld.py
Hello, World!
```

### Python

```python
print("Hello, World!")
```

### Java

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Perl

```perl
use strict;
use warnings;

print "Hello, World!\n";
```

### C

```c
#include <stdio.h>

int main()
{
    printf("Hello, World!\n");
}
```

### Ruby

```ruby
puts 'Hello, World!'
```
