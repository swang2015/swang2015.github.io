---
layout: post
title:  "Regular Expression in C++11"
date:   2017-03-06 19:00:00 -0500
category: programmer
tags: c++
---

Regular expression, sometimes abbreviated to Regex, is a sequence of characters that describes a search pattern in text. As a simple example, you want to list all the PNG images in a folder and the regular expression would be as easy as `.+\\.png`. Here `.` represent any character and `+` means 1 or more of them. We'll discuss other marks in detail.

## Regular expression syntax

**Special pattern characters** have special meaning in regular expression, just like `.` and `+`. They represent a category of characters. Characters with special meaning and used in original form (`^$\.*+?()[]{}|`) should be escaped (`\`) to represent their real meaning.

| Characters | Description |
| --- | --- |
| `.` | any characters except line terminators |
| `\d` | digit |
| `\s` | whitespace |
| `\w` | word, an alphanumeric or underscore character |

**Quantifiers** follow a special pattern character to represent the amount of repetitions of this special character.

| Characters | Description |
| --- | --- |
| `*` | 0 or more times |
| `+` | 1 or more times |
| `?` | 0 or 1 time |
| `{n}` | exactly n times |
| `{n, }` | n or more times |
| `{n, m}` | n to m times |

`[...]` and `(...)` describe subclass and subpattern respectively, `[^...]` represents class without some characters, and `|` is used for alternation. Now, we are ready to write our own regular expressions. 

Taking email address as an example, the regular expression is `(\\w+[\\.\\w]*)(@)(\\w+\\.[a-zA-Z]{2,})`, here's how it's composed:

- 1st subpattern: `(\\w+[\\.\\w]*)`
    - `\\w+` means one or more occurrences of any word.
    - `[\\.\\w]*` means dot or words occur for any times.
- 2nd subpattern: `@`
- 3rd subpattern: `(\\w+\\.[a-zA-Z]{2,})`
    - `\\w+`
    - `\\.` is a dot.
    - `[a-zA-Z]{2,}` means letters appear twice or more.

## C++ Examples

Regular expression is a useful string processing utility, but not until C++11 has it added regular expressions to the standard library, so we are lucky generation. Now C++ \<regex\> header supports _match, search, replace_ operations on target sequence and much more, let's take a look.

```cpp

    vector<string> strs = {
        "My email is test@gmail.com",
        "john.smith@msn.com",
        "Many emails: 123@abc.com, abc@123.com"
    };
    regex e("(\\w+[\\.\\w]*)(@)(\\w+\\.[a-zA-Z]{2,})");

    cout << "Example of regex_match:" << endl;       // output:
    for(auto s:strs){                                // Example of regex_match:
        if(regex_match(s,e))                         // john.smith@msn.com
            cout << s << endl;
    }
    cout << endl;

    cout << "Example of regex_search:" << endl;      // output:
    smatch m;                                        // Example of regex_search:
    for(auto s:strs){                                // test@gmail.com
        while(regex_search(s,m,e)){                  // john.smith@msn.com
            cout << m.str() << endl;                 // 123@abc.com
            s = m.suffix().str();                    // abc@123.com
        }
    }
    cout << endl;

    cout << "Example of regex_replace:" << endl;     // output:
    string format = "$1#$3";                         // Example of regex_replace:
    for(auto s:strs){                                // My email is test#gmail.com
        cout << regex_replace(s,e,format) << endl;   // john.smith#msn.com
    }                                                // Many emails: 123#abc.com, abc#123.com
    cout << endl;

```

**Extensive readings:**

- [Regular-Expressions.info](http://www.regular-expressions.info/), a very detailed tutorial website about regular expressions.
- [C++ regex reference](http://www.cplusplus.com/reference/regex/), complete descriptions on C++ regex functions, basic classes and ECMAScript grammar.
