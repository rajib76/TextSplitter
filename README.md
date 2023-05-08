# TextSplitter
This piece of code has been taken from the LangChain framework. This is the logic for CharacterTextSplitter.
I stripped the required piece of logic from the framework to run it stand-alone and understand the behavior

# How it works

So, lets say I have a text similar to the content in exampletext02.txt which looks as bleow

<pre><code> 
I am honored to be with you.

I dropped out.

It started before I was born. My biological mother was a young, unwed college graduate student, and she decided.
</code></pre>

Each line is seperated by \n\n. So the logic first strips the content
by the default seperator which is \n\n. Then it counts the character of
each chunk and tries to merge them into chunks that adheres to the specified
chunk size.

So, if i specify a chunk size of 44. The chunks will be calculated
as below

The number of character in the first line is 28. Next count the number
of characters in the next line which is 14, add 2(length of the seperator)
which makes it 16. 16+28 = 44. Since, it is equal to specified chunk size that 
becomes our chunk#1. The next line is 113 characters long. This will not be
split into chunk size of 44, it will be taken as a whole as this is the 
first level of split(which is by the seperator). So, it will become chunk#2
which is much bigger then 44 characters.

<pre><code> 
Chunk No :1
I am honored to be with you.

I dropped out.
Chunk No :2
It started before I was born. My biological mother was a young, unwed college graduate student, and she decided.
</code></pre>

So, this method of splitting does not help if all my sentences seperated 
by the seperator are more than the specified chunk size