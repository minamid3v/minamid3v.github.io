---
layout: post
title: Nth character in Concatenated Decimal String
categories: [algorithm, python]
tags: [nth, character, python]
description: If all decimal numbers are concatenated in a string then we will get a string which looks like string P as shown below. We need to tell Nth character of this string. P = “12345678910111213141516171819202122232425262728293031….”
---
If all decimal numbers are concatenated in a string then we will get a string which looks like string P as shown below. We need to tell Nth character of this string.  
P = “12345678910111213141516171819202122232425262728293031….”  
Examples:  
    N= 10    10th character is 1  
    N = 11    11th character is 0  
    N = 50    50th character is 3  
    N = 190    190th character is 1  

{% highlight python %}
import math

def find(n):
    i = 0
    while n>0:
        i+=1
        n-= math.floor(math.log10(i))+1
    return str(i)[n-1]

print(find(1000))
{% endhighlight %}
