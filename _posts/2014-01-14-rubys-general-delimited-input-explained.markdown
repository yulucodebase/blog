---
layout: post
title: "Ruby's General Delimited Input Explained"
date: 2014-01-14 23:22:18 +0000
comments: true
publish: true
categories: Ruby Basics
excerpt: Explains what is 'General Delimited Input' and the where it should be used.
---
I came across a "strange" syntax during the first week of my Introduction to Ruby course.

{% highlight ruby %}
	arr = %w{ a b c d } # creates an array of strings
{% endhighlight %}

It appears many times in Ruby's official API document of the Array class. It is strange, from a Java programmer's perspective (or maybe just me?), in that `a b c d` on the right hand doesn't look like string literals but maybe variables defined somewhere else. However, there are no operators or commas separating these "variables" which makes it a bit confusing to me. 

After consulting on the course forum, it turns out this is just an alternative syntax of defining an Array of strings. The above example creates the following array (there are always more than one way to do things in Ruby, remember?):

{% highlight ruby %}
	["a","b","c","d"]
{% endhighlight %}

It saves time from having to type the pair of (single/double) quotes around every string, especially if the array has many of these strings. Besides, this improves the readability of the Array definition as well, given that you recognize this syntax of course.

I like to dig a bit deeper when it's easier to learn things by having a better understanding of the rationals behind the scene. This syntax is called **"General Delimited Input"** in Ruby and it turns out it's not just used to create arrays of strings but also has other use cases, such as creating regular expressions or plain string literals. **It's basically the alternative way to create different literals**. 

The following table (copied from the book "[Programming Ruby](http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0)") gives an overall picture of what can be created with this syntax.

![Summary of Ruby's General Delimited Input Syntax]({{ site.url }}/assets/images/ruby_general_delimited_input.png)

It starts with a `%` sign and a pair of "beginning" and "ending" characters (the delimiters) which can be any non-alphanumeric and or non-multibyte characters. For example, `%{hello world}` is equivalent to `"hello world"`. 

It may not make too much sense to create such a simple string in an obviously "bloated" way but it comes in handy when some of the characters of the strings need to be escaped, for example, "I thought John's dog was called \"Spot,\" not \"Fido.\"" can be rewritten as `%{I thought John's dog was called "Spot," not "Fido."}` in general delimited format. 

The `%` sign can be followed by a "type" character which identifies the type of the input. Valid "type" characters are shown in the above picture and `%{}` is basically the shorthand for `%Q{}`. The difference between the upper-case version and lower-case version of the type character is that the upper-case version supports **interpolation** of expressions, for example:

{% highlight ruby %}
name = "Luke"
puts %Q{Hello, #{name}!} # "hello, Luke!"
{% endhighlight %}

Here are a couple of good references ([Ruby Programming from Linuxtopia](http://www.linuxtopia.org/online_books/programming_books/ruby_tutorial/The_Ruby_Language_General_Delimited_Input.html) and of course our [mighty StackOverflow](http://stackoverflow.com/questions/2260221/what-are-the-pros-and-cons-of-rubys-general-delimited-input-percent-syntax)) which helped me to understand its syntax.

