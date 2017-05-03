---
layout: post
title:  "Integer to English Words"
date:   2017-04-10 15:00:00 -0500
categories: programmer algorithm-&-data-structure
tags: c++
---

### Problem
Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 2<sup>31</sup> - 1.

### Solution
As we know, numbers in every 3 digits can be represented as `thousand`, `million`, `billion`, `trillion`, `quadrillion `... According to description, the number is no larger than billions. All remainders are at hundreds level and are easy to represent.

```c++
class Solution {
public:
    string numberToWords(int num) {
        if (num == 0) return "Zero";
        
        stack<string> num_word;        
        vector<string> units = {"Thousand ", "Million ", "Billion "};
        int i = 0;
        num_rem.push(convertHundreds(num%1000));
        
        while(num >= 1000){
            num = num/1000;
            if (num%1000!=0)
            	num_word.push(convertHundreds(num%1000) + units[i]);
            i++;
        }
        
        string res;
        
        while (!num_word.empty()) {
            res += num_word.top();
            num_word.pop();
        }
        
        return res.substr(0, res.length()-1);
    }
    
    string convertHundreds(int num) {
        map<int, string> less20 = {
            {0, ""},
            {1, "One "},
            {2, "Two "},
            {3, "Three "},
            {4, "Four "},
            {5, "Five "},
            {6, "Six "},
            {7, "Seven "},
            {8, "Eight "},
            {9, "Nine "},
            {10, "Ten "},
            {11, "Eleven "},
            {12, "Twelve "},
            {13, "Thirteen "},
            {14, "Fourteen "},
            {15, "Fifteen "},
            {16, "Sixteen "},
            {17, "Seventeen "},
            {18, "Eighteen "},
            {19, "Nineteen "}
        };
        
        map<int, string> over20 = {
            {2, "Twenty "},
            {3, "Thirty "},
            {4, "Forty "},
            {5, "Fifty "},
            {6, "Sixty "},
            {7, "Seventy "},
            {8, "Eighty "},
            {9, "Ninety "},
        };
        
        string res = "";
        int hud=num/100, rem=num%100, ten=rem/10, single=rem%10;
        
        if(hud != 0) res =  less20[hud] + "Hundred ";
        if (rem < 20) {
            res += less20[rem];
        } else {
            res = res + over20[ten] + less20[single];
        }
        return res;
    }
};
```
