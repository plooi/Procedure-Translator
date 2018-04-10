*PROCEDURE TRANSLATOR INTRODUCTION

Functions are great. However, they're not perfect. 

For example, take a look at this Java method which takes a string, a start index, and a stop index, and returns the appropriate substring:

public static String substring(String s, int start, int stop){...}

or in Python

def substring(theString, start, stop):
    ...

or in C

char* substring(char* str, int start, int stop){...}

These are all fine method/function headers. However, if I make a call to substring("hello",2,3) it doesn't absolutely jump out at me that this is going to give me the substring of "hello" from index 2 to index 3. It COULD be the substring starting at index 2 with LENGTH of 3. Or it could be the substring of "hello" that is 2 characters long that begins at index 3... It could actually logically mean a LOT of different things! Now, I am fully aware that if one is able to read the documentation, all confusion will be cleared up. However, my ability to read doucmentation still doesn't help when I need to QUICKLY read through a large amount of ambiguous code. Procedures, however, WILL clear up ALL ambiguity.

*PROCEDURE DECLARATIONS

Procedures are exactly the same thing as functions, but they look like english sentences but with "fill in the blanks." Here, let me give an example of a Java procedure header, which is analogous to a method header or function header. This procedure will generate and return the substring of S which begins at B and ends at E:

public static String (`substring of` String S `from` int B `to` int E){...}

We use tick quotations, or `...`, to quote out the parts of the procedure that do not change. In the above example, `substring of` and `from` and `to` are all parts of the procedure that do not change. These parts of the procedure are called the procedure's identifiers.

For the parameters, or for the parts of the procedure where you can "fill in the blank," you declare these in the same way that you would declare parameters for a function in the parent language. In the above example, the parameters are String S, int B, and int E, and they are that way because that is how you declare parameters in Java, because our parent language, in this example, is Java. 

*CALLING PROCEDURES

To call a procedure, first, you must copy the parenthasized part of the procedure header. For the example above, you would copy down 

(`substring of` String S `from` int B `to` int E)

then, you replace all of the parameters with values

(`substring of` "abCdEfgHI" `from` 2 `to` 5)

and this is a valid procedure call. In this case because the procedure does not return void, you could even store it in a variable

String theSubstring = (`substring of` "abCdEfgHI" `from` 2 `to` 5);

and you could treat it just like any other function call. The only difference is that a procedure makes sense and is easy to read, while a function call is slightly more ambiguous.

*EXECUTION AND TRANSLATION

So let's say that I have a Java program written and it is in a file called Test.procjava and the source code is this:
//code starts
public class Test
{
    //This is the main method declared as a normal java method. This will run when the program starts.
    public static void main(String[] args)
    {
        (`print` "Hello World" `on screen` 10 `times`);
    }
    
    //This is a procedure definition. This file is .procjava, not .java, because this part of the code is not TRULY Java code- it's my made up procedure language modification of Java
    public static void (`print` String s `on screen` int n `times`)
    {
        for(int i = 0; i < n; i++)
            System.out.println(s);
    }
    
}
//code ends


This is a correct (proceduresk) Java program that prints "Hello World" 10 times... EXCEPT if we actually run this in the official Java compiler, it will get very mad and yell at us for having unrecognizable characters (mainly the ticks). So, that's why we have to translate this into Java code, and then we run the Java code using the Java compiler. To do this, you will first have to open up the terminal, or command prompt, or whatever outdated-looking command entry device you got, and change directory to the directory that Test.procjava  is in. Assume, for a second, that PT.jar is at "C:\ProcedureTranslator\PT.jar". Now, type these commands

java -jar C:\ProcedureTranslator\PT.jar procjava java
javac Test.java
java Test

...
And BAM! You SHOULD, if neither of us made a mistake, have "Hello World" printed on your screen 10 times. This worked, even though we never actually wrote completely valid Java code, because we translated it to REAL Java with this line here 

java -jar PT.jar procjava java

and then the computer immediately created a bunch of valid Java files with .java extension, then we ran it as usual. 

The actual format for executing PT.jar is:

java -jar PT.jar <custom file extension> <destination file extension(optional***)> <language> AsciiTranslationFile:<translationfile(optional*****)>

*** destination file extension defaults to the default file extensions of the language used. Java -> .java Python -> .py C -> .c etc...
***** translationfile defaults to ascii_translation.txt  -  if you prefer not to use this parameter, do not even write AsciiTranslationFile: at all, but if you do want to use the parameter, you must write AsciiTranslationFile: and then write the name of the ascii translation file directly after.

however, as two of the four parameters here are optional, all you absolutely need to be comfortable with is the two required parameters which are <custom file extension> and <language>. 
    
    
*HOW IT WORKS AND ASCII TRANSLATION FILE

Assume Test.procjava has the text

//code starts
public class Test
{
    public static void main(String[] args)
    {
        (`print` "Hello World" `on screen` 10 `times`);
    }
    public static void (`print` String s `on screen` int n `times`)
    {
        for(int i = 0; i < n; i++) System.out.println(s);
    }
}
//code ends

. If we use PT.jar to translate this .procjava file into real Java code, the resulting Test.java file will have the text

//code starts
public class Test
{
    public static void main(String[] args)
    {
        printonscreentimes("Hello World", 10);
    }
    public static void printonscreentimes(String s, int n)
    {
        for(int i = 0; i < n; i++) System.out.println(s);
    }
}
//code ends

. Notice how the translated method name of our procedure is "printonscreentimes", which is merely a concatenation of all the procedure identifiers `print` `on screen` `times`. It is honestly trivial. However, if instead we had a procedure like this

public static void (String personName `:)`)
{
    System.out.println(personName + " is happy.");
}

WHOA!?? Is that a smiley face as the procedure identifier? You bet! You can use basically any symbols you want in the procedure identifier, and it will come out fine. How? Well, the ascii_translation.txt file specifies many preestablished (yet customizable) translations, including that the sequence ":)" will be replaced with "good". So, the resulting translated .java file will portray this procedure as 

public static void good(String personName)
{
    System.out.println(personName + " is happy.");
}

. If you want to add, remove, change the translations, you can definitely modify ascii_translation.txt to be whatever you like. Note that the backslash separates the sequence before and the sequence after translation. You can also make another file that defines a whole new set of ASCII translations. Just be sure that you specify it when you execute PT.jar.

*WARNINGS AND NOTES

1. Name collision warning
Consider a file which contains these two Python procedures

def (`apply` scalar `to` matrix):...
def (`app` n,m `lyto` ):... #hahaha I know this procedre doesn't make any sense but stay with me here

Try to avoid situations like this, because when the file is translated, you will get two functions like this

def applyto(scalar, matrix):...
def applyto(n, m):...

and this will cause problems. The best solution is to be careful in what you name your procedures, and to understand how the translation process works. If you have read this document thoroughly, then I would say that yes, you DO understand how translation works. 

2. Use with Java, JavaScript, Python, C, CPlusPlus,CSharp

Note that when filling in the <language> parameter, CPlusPlus is spelled "CPlusPlus", not C++, or CPP, or CPlus.
    
3. Unusual Bugs

Do not use \" to indicate a quotation mark. Instead, use \u0034.
Do not create python strings like: ''' this is my string, it has another apostrophe inside -> ' this is bad '''
Nor should you create python string like: """ this is my string and it has a " insdie. this is also bad """


*FINAL THOUGHTS AND DOWNLOAD

To download this, just grab all the files in this repository and copy them to your computer. 

Have fun with procedures guys and girls! My goal for the Procedure Translator is that it will help make programming a process that is more organized, more clear, and less confusing than it is today. I believe that beginner programmers will have a MUCH easier and more fun time understanding "sentences with fill in the blanks" rather than with straight up functions. On the other hand, large software companies will also benefit from using procedures because when software projects grow large, the code becomes very confusing to work with. Using procedures will help so much in this situation because procedures will clear up a lot of the ambiguity in the code, and the programmers will thus be able to focus on solving the main task at hand, instead of having to focus on wading through confusing and ambiguous code someone else wrote.

Thank you,

Peter

For "live" help, execute the PT.jar file with command line argument of "help":

java -jar PT.jar help

