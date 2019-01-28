# Java-Regular-Expressions

-	Regular expressions are used for defining String patterns 
-	That can be used for searching, manipulating and editing a text
-	java.util.regex
-	Pattern, Matcher, PatternSyntaxException
-	metacharacter, classes, Character Classes,Predefined Character Classes – Metacharacters, Boundary Matchers


-------------------------------------
## Pattern.split() Examples


class RegexExample2{  
	public static void main(String args[]){  
		String text = "ThisIsChaitanya.ItISMyWebsite"; // String
		// Pattern for delimiter
		String patternString = "is"; // Pattern  <===========
		Pattern pattern = Pattern.compile(patternString, Pattern.CASE_INSENSITIVE); // Case Insensitive  <===========
		String[] myStrings = pattern.split(text); // Split  <===========
		for(String temp: myStrings){
			System.out.println(temp);
		}
		System.out.println("Number of split strings: "+myStrings.length);
	}
}

--------------------------------------
## Methods :


### Matcher Class:

-	boolean matches()
	-	test whether the regular expression matches the pattern

-	lookingAt(): Similar to matches() method 
	-	except that it matches the regular expression only against the beginning of the text
	-	while matches() search in the whole text

-	find(): Searches the occurrences of of the regular expressions in the text
	-	Mainly used when we are searching for multiple occurrences
	
-	boolean find(int start)	
	-	finds the next expression that matches the pattern from the given start number

-	start() and end(): Both these methods are generally used along with the find() method
	-	They are used for getting the start and end indexes of a match that is being found using find() method

-   String group()	
	-	returns the matched subsequence

-   int groupCount()	
	-	returns the total number of the matched subsequence
	
	
### Pattern Class:	

-	Pattern compile(String regex)
-	Matcher matcher(CharSequence input)
-	static boolean matches(String regex, CharSequence input)
-	String[] split(CharSequence input)
-	String pattern()
	
--------------------------------------
## String Literals

Pattern.matches("abc", "abc");

## Character Classes

- OR Class
	-	[bcr]at", "bat cat rat"

-	NOR Class
	-	"[^abc]", "g"
	
-	Range Class
	-	"[A-Z]", "Two Uppercase alphabets 34 overall"

-  Union Class	
	-	"[1-3[7-9]]", "123456789"
	
-	Intersection Class
	-	"[1-6&&[3-9]]", "123456789"
	
-	 Subtraction Class
	-	"[0-9&&[^2468]]", "123456789"


Pattern.matches("[pqr]", "abcd"); // false
Pattern.matches("[pqr]", "r"); // false
Pattern.matches("[pqr]", "pq"); // false

## Regex Character classes

1	[abc]			: a, b, or c (simple class)
2	[^abc]			: Any character except a, b, or c (negation)
3	[a-zA-Z]		: a through z or A through Z, inclusive (range)
4	[a-d[m-p]]		: a through d, or m through p: [a-dm-p] (union)
5	[a-z&&[def]]	: d, e, or f (intersection)
6	[a-z&&[^bc]]	: a through z, except for b and c: [ad-z] (subtraction)
7	[a-z&&[^m-p]]	: a through z, and not m through p: [a-lq-z](subtraction)

--------------------------------------

## Predefined Character Classes – Metacharacters

.   ->	Any character (may or may not match line terminators)
\d  ->	A digit: [0-9]
\D  ->	A non-digit: [^0-9]
\s  ->	A whitespace character: [ \t\n\x0B\f\r]
\S  ->	A non-whitespace character: [^\s]
\w  ->	A word character: [a-zA-Z_0-9]
\W  ->	A non-word character: [^\w]

For e.g.
Pattern.matches("\\d", "1"); would return true
Pattern.matches("\\D", "z"); return true
Pattern.matches(".p", "qp"); return true, dot(.) represent any character

--------------------------------------
## Boundary Matchers

^	Matches the beginning of a line.
$	Matches then end of a line.
\b	Matches a word boundary.
\B	Matches a non-word boundary.
\A	Matches the beginning of the input text.
\G	Matches the end of the previous match
\Z	Matches the end of the input text except the final terminator if any.
\z	Matches the end of the input text.

Pattern.matches("^Hello$", "Hello"): return true, Begins and ends with Hello
Pattern.matches("^Hello$", "Namaste! Hello"): return false, does not begin with Hello
Pattern.matches("^Hello$", "Hello Namaste!"): return false, Does not end with Hello
--------------------------------------

## Quantifiers

Greedy	   : Matches

X?		   : Matches X once, or not at all (0 or 1 time)
X*		   : Matches X zero or more times
X+		   : Matches X one or more times
X{n}? 	   : Matches X exactly n times
X{n,} 	   : Matches X at least n times
X{n, m)	   : Matches X at least n time, but at most m times

--------------------------------------
## 	Look-ahead and Look-behind (?=) and (?<=)

-	d(?=r)      
	-	matches a d only if is followed by r,
	-	but r will not be part of the overall regex match

-	(?<=r)d    	
	
	-	matches a d only if is preceded by an r
	-	but r will not be part of the overall regex

-	d(?!r)
		
	-	matches a d only if is not followed by r
	-	but r will not be part of the overall regex	
	
-	(?<!r)d

	-	matches a d only if is not preceded by an r
	-   but r will not be part of the overall regex	
	
--------------------------------------

## PatternSyntaxException Class 

-	A PatternSyntaxException is an unchecked(RuntimeException) exception
-	That indicates a syntax error in a regular expression pattern

### Methods:

	public String getDescription() : Retrieves the description of the error
	public int getIndex() : Retrieves the error index
	public String getPattern() : Retrieves the erroneous regular expression pattern
	public String getMessage()

--------------------------------------
## 	Capturing Groups

-	Groups allows us to treat multiple characters as a single unit through capturing groups
-	It will attach numbers to the capturing groups and allow back referencing using these numbers

### Examples:

	"(\\d\\d)", "12" : true
	"(\\d\\d)", "1212" :
	"(\\d\\d)\\1", "1212" : true
	"(\\d\\d)(\\d\\d)", "1212" : true
	"(\\d\\d)\\1\\1\\1", "12121212" : true
	"(\\d\\d)\\1", "1213": false
	
--------------------------------------
## Examples Set 1:

	System.out.println(Pattern.matches("tom", "Tom")); //False
	System.out.println(Pattern.matches("[Tt]om", "Tom")); //True
    System.out.println(Pattern.matches("[Tt]om", "Tom")); //True
   
    System.out.println(Pattern.matches("[tT]im|[jJ]in", "Tim"));//True
    System.out.println(Pattern.matches("[tT]im|[jJ]in", "jin"));//True
   
    System.out.println(Pattern.matches(".*abc.*", "deabcpq"));//True
	System.out.println(Pattern.matches("^[^\\d].*", "123abc")); //False
	System.out.println(Pattern.matches("^[^\\d].*", "abc123")); //True
	
	
	System.out.println(Pattern.matches("[a-zA-Z][a-zA-Z][a-zA-Z]", "aPz"));//True
	System.out.println(Pattern.matches("[a-zA-Z][a-zA-Z][a-zA-Z]", "aAA"));//True
	System.out.println(Pattern.matches("[a-zA-Z][a-zA-Z][a-zA-Z]", "apZx"));//False
	
	System.out.println(Pattern.matches("\\D*", "abcde")); //True
	System.out.println(Pattern.matches("\\D*", "abcde123")); //False
	
	System.out.println(Pattern.matches("^This$", "This is Chaitanya")); //False
	System.out.println(Pattern.matches("^This$", "This")); //True
	System.out.println(Pattern.matches("^This$", "Is This Chaitanya")); //False

	
	//In the below example, the regular expression .*book.* 
	//is used for searching the occurrence of string “book” in the text
	String content = "This is Chaitanya from Beginnersbook.com.";
	String pattern = ".*book.*";
	Pattern.matches(pattern, content);
	
	
	//. Examples
	System.out.println(Pattern.matches(".s", "as"));//true (2nd char is s)  
	System.out.println(Pattern.matches(".s", "mk"));//false (2nd char is not s)  
	System.out.println(Pattern.matches(".s", "mst"));//false (has more than 2 char)  
	System.out.println(Pattern.matches(".s", "amms"));//false (has more than 2 char)  
	System.out.println(Pattern.matches("..s", "mas"));//true (3rd char is s)  
	
	//Character Classes
	System.out.println(Pattern.matches("[amn]", "abcd"));//false (not a or m or n)  
	System.out.println(Pattern.matches("[amn]", "a"));//true (among a or m or n)  
	System.out.println(Pattern.matches("[amn]", "ammmna"));//false (m and a comes more than once)
	
	// Quantifiers	
	System.out.println(Pattern.matches("[amn]?", "a"));//true (a or m or n comes one time)  
	System.out.println(Pattern.matches("[amn]?", "aaa"));//false (a comes more than one time)  
	System.out.println(Pattern.matches("[amn]?", "aammmnn"));//false (a m and n comes more than one time)  
	System.out.println(Pattern.matches("[amn]?", "aazzta"));//false (a comes more than one time)  
	System.out.println(Pattern.matches("[amn]?", "am"));//false (a or m or n must come one time)  

	
	System.out.println(Pattern.matches("[amn]+", "a"));//true (a or m or n once or more times)  
	System.out.println(Pattern.matches("[amn]+", "aaa"));//true (a comes more than one time)  
	System.out.println(Pattern.matches("[amn]+", "aammmnn"));//true (a or m or n comes more than once)  
	System.out.println(Pattern.matches("[amn]+", "aazzta"));//false (z and t are not matching pattern)  

	// Metacharacters
	
	System.out.println(Pattern.matches("\\d", "abc"));//false (non-digit)  
	System.out.println(Pattern.matches("\\d", "1"));//true (digit and comes once)  
	System.out.println(Pattern.matches("\\d", "4443"));//false (digit but comes more than once)  
	System.out.println(Pattern.matches("\\d", "323abc"));//false (digit and char) 
	
	System.out.println(Pattern.matches("\\D", "abc"));//false (non-digit but comes more than once)  
	System.out.println(Pattern.matches("\\D", "1"));//false (digit)  
	System.out.println(Pattern.matches("\\D", "4443"));//false (digit)  
	System.out.println(Pattern.matches("\\D", "323abc"));//false (digit and char)  
	System.out.println(Pattern.matches("\\D", "m"));//true (non-digit and comes once)  
		
--------------------------------------
## Examples Set 2:
	
	// Common:
	 Pattern p = Pattern.compile(REGEX);
     Matcher m = p.matcher(INPUT);   // get a matcher object
	
	
##	Start and End Methods:
	
	
	Code Snippet:
	
	
	   private static final String REGEX = "\\bcat\\b";
	   private static final String INPUT = "cat cat cat cattie cat";
		
		while(m.find()) {
		 count++;
		 System.out.println("Match number "+count);
		 System.out.println("start(): "+m.start());
		 System.out.println("end(): "+m.end());
		}	
	
	
	Output:
	
		Match number 1
		start(): 0
		end(): 3
		Match number 2
		start(): 4
		end(): 7
		Match number 3
		start(): 8
		end(): 11
		Match number 4
		start(): 19
		end(): 22
  
## Matches and LookingAt Methods:

-	The matches and lookingAt methods both attempt to match an input sequence against a pattern
-	The difference, however, is that matches requires the entire input sequence to be matched, while lookingAt does not
	
	
	Code Snippet:
	
		private static final String REGEX = "foo";
		private static final String INPUT = "fooooooooooooooooo";

		System.out.println("lookingAt(): "+matcher.lookingAt());
		System.out.println("matches(): "+matcher.matches());
		 
	 
	Output:

		Current REGEX is: foo
		Current INPUT is: fooooooooooooooooo
		lookingAt(): true
		matches(): false
		
##	Replace and ReplaceFirst Methods:


-	The replaceFirst and replaceAll methods replace the text that matches a given regular expression
-	replaceFirst replaces the first occurrence
-	replaceAll replaces all occurrences

	
	Code Snippet:
		
	   private static String REGEX = "dog";
	   private static String INPUT = "The dog says meow. All dogs say meow.";
	   private static String REPLACE = "cat";
	   
	   Pattern p = Pattern.compile(REGEX);
	   Matcher m = p.matcher(INPUT); 
	   INPUT = m.replaceAll(REPLACE);
	   
	   
##	AppendReplacement and AppendTail Methods

-	Matcher class also provides appendReplacement and appendTail methods for text replacement


	private static String REGEX = "a*b";
	private static String INPUT = "aabfooaabfooabfoob";
	private static String REPLACE = "-";
   
   // get a matcher object
      Matcher m = p.matcher(INPUT);
      StringBuffer sb = new StringBuffer();
      while(m.find()) {
         m.appendReplacement(sb, REPLACE);
      }
      m.appendTail(sb);
      System.out.println(sb.toString());

--------------------------------------------------

Example Set 3: 


	// Removes whitespace between a word character and . or ,
	String pattern = "(\\w)(\\s+)([\\.,])";
	System.out.println(EXAMPLE_TEST.replaceAll(pattern, "$1$3"));
	
	public class StringMatcher {
		// returns true if the string matches exactly "true"
		public boolean isTrue(String s){
			return s.matches("true");
		}
		// returns true if the string matches exactly "true" or "True"
		public boolean isTrueVersion2(String s){
			return s.matches("[tT]rue");
		}

		// returns true if the string matches exactly "true" or "True"
		// or "yes" or "Yes"
		public boolean isTrueOrYes(String s){
			return s.matches("[tT]rue|[yY]es");
		}

		// returns true if the string contains exactly "true"
		public boolean containsTrue(String s){
			return s.matches(".*true.*");
		}


		// returns true if the string contains of three letters
		public boolean isThreeLetters(String s){
			return s.matches("[a-zA-Z]{3}");
			// simpler from for
	//      return s.matches("[a-Z][a-Z][a-Z]");
		}



		// returns true if the string does not have a number at the beginning
		public boolean isNoNumberAtBeginning(String s){
			return s.matches("^[^\\d].*");
		}
		// returns true if the string contains a arbitrary number of characters except b
		public boolean isIntersection(String s){
			return s.matches("([\\w&&[^b]])*");
		}
		// returns true if the string contains a number less than 300
		public boolean isLessThenThreeHundred(String s){
			return s.matches("[^0-9]*[12]?[0-9]{1,2}[^0-9]*");
		}

	}
 
--------------------------------------------------







