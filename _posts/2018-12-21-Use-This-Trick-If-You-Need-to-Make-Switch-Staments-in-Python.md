---
layout: post
title:  "Use This Trick If You Need to Make Switch Staments in Python"
categories: python/java/c
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;



&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first language that I  got a decent understanding of was Java. Most of my computer science classes that were in Java and C. Both have similar structures, and after seeing them over and over again, you get used to them. In situations where I have lots of if-else cases my go to is a switch statement.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;


# For Java and C switch statements are the same.
 The syntax is interchangeable. 


{% highlight java %}

switch (i)
	{
    	case 1: // Do something for 1;
        	break;
    	case 2: // Do something for 2;
        	break;
    	default: // Do something for other than 1 and 2
	}
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

# Python Doesn't have Switch Statements, But They Can Be Mimicked.

 I was solving a leetcode problem in python, and I assumed that the Java/C switch statement syntax would work. I was surprised when I learned that python didn't have switch statements.  At first, I thought there was a pythonic way that python handled switch statements. To me, the appeal of python is writing fewer lines of code. It didn't make sense; I didn't want to write line after line of if-elif cases.  I regained my respect for python after finding that switch statements can be mimicked with a dictionary. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

{% highlight python%}

def switcher(op, x, y): 
	return{ 
	'add' : lambda : x + y, 
	'sub' : lambda : x - y, 
	'mul' : lambda : x * y, 
	'div' : lambda : x / y, 
	}.get(op,lambda: None)() 

	
{% endhighlight %}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

If you were doing simple arithmetic like in the example above it's better to use the operator module. Lambda functions were used to make the code generic and easier to see the pattern.  Next time you have a long if-elif block try using a dictionary. 




