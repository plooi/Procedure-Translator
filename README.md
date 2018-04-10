#Procedure Translator Introduction

Functions are great. However, they're not perfect. 

For example, take a look at this Java method which takes a string, a start index, and a stop index, and returns the appropriate substring:

public static String substring(String s, int start, int stop){...}

or in Python

def substring(theString, start, stop):
    ...

or in C

char* substring(char* str, int start, int stop){...}

These are all fine method/function headers. However, if I make a call to substring("hello",2,3) it doesn't absolutely jump out at me that this is the substring of "hello" from index 2 to index 3. It COULD be the substring starting at index 2 with LENGTH of 3. Or it could be the substring of "hello" that is 2 characters long that begins at index 3... It could actually logically mean a LOT of things! Now, I am fully aware that if one is able to read the documentation, all confusion will be cleared up. However, my ability to read doucmentation still doesn't help when looking at a massive amount of AMBIGUOUS code. Procedures, however, WILL help.

#Procedure Declarations

Procedures are exactly the same thing as functions, but they look like english sentences but with "fill in the blanks." Here, let me give an example of a Java procedure header, which is analogous to a method header or function header. This procedure will generate and return the substring of S which begins at B and ends at E:

public static String (`substring of` String S `from` int B `to` int E){...}

We use tick quotations, or `...`, to quote out the parts of the procedure that do not change. In the above example, `substring of` and `from` and `to` are all parts of the procedure that do not change. These parts of the procedure are called the procedure's identifiers.

For the parameters, or for the parts of the procedure where you can "fill in the blank," you declare these in the same way that you would declare parameters for a function in the parent language. In the above example, the parameters are String S, int B, and int E, and they are declared correctly for Java, because our parent language, in this example, is Java. 

#Calling Procedures

To call a procedure, first, you must copy the parenthasized part of the procedure header. For the example above, you would copy down 

(`substring of` String S `from` int B `to` int E)

then, you replace all of the parameters with values

(`substring of` "abCdEfgHI" `from` 2 `to` 5)

and this is a valid procedure call. In this case because the procedure does not return void, you could even store it in a variable

String theSubstring = (`substring of` "abCdEfgHI" `from` 2 `to` 5);

and you could treat it just like any other function call. The only difference is that a procedure makes sense and is easy to read, while a function call is slightly more ambiguous.



For "live" help, execute the PT.jar file with command line argument of "help":

java -jar PT.jar help

