# Regular Expressions Questions

---------------------------------------------
## Create a regular expression that accepts alphanumeric characters only. Its length must be six characters long only.'

-	Regex: [\w]{6},	\w{6}, [a-zA-Z0-9]{6}

	System.out.println(Pattern.matches("[a-zA-Z0-9]{6}", "arun32"));//true  
	System.out.println(Pattern.matches("[a-zA-Z0-9]{6}", "kkvarun32"));//false (more than 6 char)  
	System.out.println(Pattern.matches("[a-zA-Z0-9]{6}", "JA2Uk2"));//true  
	System.out.println(Pattern.matches("[a-zA-Z0-9]{6}", "arun$2"));//false ($ is not matched)  


----------------------------------------------
## Create a regular expression that accepts 10 digit numeric characters.starting with 7, 8 or 9 only.

- Regex: [789]\d{9}, [789]{1}[0-9]{9}, [789]{1}\\d{9}


	System.out.println("by character classes and quantifiers ...");  
	System.out.println(Pattern.matches("[789]{1}[0-9]{9}", "9953038949"));//true  
	System.out.println(Pattern.matches("[789][0-9]{9}", "9953038949"));//true  
	  
	System.out.println(Pattern.matches("[789][0-9]{9}", "99530389490"));//false (11 characters)  
	System.out.println(Pattern.matches("[789][0-9]{9}", "6953038949"));//false (starts from 6)  
	System.out.println(Pattern.matches("[789][0-9]{9}", "8853038949"));//true  
	  
	System.out.println("by metacharacters ...");  
	System.out.println(Pattern.matches("[789]{1}\\d{9}", "8853038949"));//true  
	System.out.println(Pattern.matches("[789]{1}\\d{9}", "3853038949"));//false (starts from 3) 

---------------------------------------------- 
## Java Regex Finder Example

	Code Snippet:

		public class RegexExample8{    
			public static void main(String[] args){    
				Scanner sc=new Scanner(System.in);  
				while (true) {    
					System.out.println("Enter regex pattern:");  
					Pattern pattern = Pattern.compile(sc.nextLine());    
					System.out.println("Enter text:");  
					Matcher matcher = pattern.matcher(sc.nextLine());    
					boolean found = false;    
					
					while (matcher.find()) {    // Recursive Find
						
						//	found() --> "group" --> text
						System.out.println("I found the text "+matcher.group()+" starting at index "+    
						matcher.start()+" and ending at index "+matcher.end());    
						found = true;    
					}    
					if(!found){    
						System.out.println("No match found.");    
					}    
				}    
			}    
		}    
		
	Output:

		Enter regex pattern: java
		Enter text: this is java, do you know java
		I found the text java starting at index 8 and ending at index 12
		I found the text java starting at index 26 and ending at index 30	
----------------------------------------------	

## How to extract numbers from a string?

	List<Integer> numbers = new LinkedList<Integer>();
	Pattern p = Pattern.compile("\\d+");
	Matcher m = p.matcher(str); 
	while (m.find()) {
	  numbers.add(Integer.parseInt(m.group()));
	}

----------------------------------------------
## How to split Java String by newlines?

	String lines[] = String.split("\\r?\\n");
	String lines[] = String.split("\\r\\n");//If don’t want empty lines
	String.split(System.getProperty("line.separator"));
----------------------------------------------

## How to escape text for regular expression?

	\\
----------------------------------------------
##  Why does String.split() need pipe delimiter to be escaped?

	A|B means either A or B. 
	Please refer to Alternation with The Vertical Bar or Pipe Symbol for more details.
	Therefore, to use | as a literal, you need to escape it by adding \ in front of it, like \\|.

----------------------------------------------
Write a Regular expression to Repeating characters

	String str = "aaabbbcc fgedaaaacccgg";
	String[] split = str.split("(\\w)\\1+");

	System.out.println(Arrays.toString(split));

----------------------------------------------

## How can we match anbn with Java regex?

	Pattern p = Pattern.compile("(?x)(?:a(?= a*(\\1?+b)))+\\1");
	
	System.out.println(p.matcher("aaabbb").matches());// true
	System.out.println(p.matcher("aaaabbb").matches());// false
	System.out.println(p.matcher("aaabbbb").matches());// false
	System.out.println(p.matcher("caaabbb").matches());// false


----------------------------------------------

## How to replace 2 or more spaces with single space in string and delete leading spaces only?

	String line = "  aa bbbbb   ccc     d  ";
	// " aa bbbbb ccc d "
	System.out.println(line.replaceAll("[\\s]+", " "));

----------------------------------------------

## How to determine if a number is a prime with regex?

	public static void main(String[] args) {
	  System.out.println(prime(1)); // false
	  System.out.println(prime(2)); // true
	  System.out.println(prime(3)); // true
	  System.out.println(prime(5)); // true
	  System.out.println(prime(8)); // false
	  System.out.println(prime(13)); // true
	  System.out.println(prime(14)); // false
	  System.out.println(prime(15)); // false
	}
	 
	public static boolean prime(int n) {
	  return !new String(new char[n]).matches(".?|(..+?)\\1+");
	}

----------------------------------------------










































 
 
 
 
 


	
