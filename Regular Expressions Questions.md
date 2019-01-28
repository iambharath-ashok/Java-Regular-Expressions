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
## Write a Regular expression to Repeating characters

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
## rite a regex to validate a new username. Criteria for a valid username is as follows:

	It should start with an English alphabet followed by alphanumeric characters.
	No special characters allowed
	Username length should be at least 3 and should not exceed 20.

	^[A-Za-z][A-Za-z0-9]{2,19}
----------------------------------------------
## How can we validate a given String that denotes an IPv4 IPAddress?

	\b((25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d?)\.){3}(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d?)\b
----------------------------------------------
## Given an input string with alphanumeric characters, extract the integers into a list and print them out in the order of occurrence.

	public class ExtractNumFromString {
	 
	 public static void main(String[] args) {
	  String numPattern = "-?\d+";
	  String numStr = "12arr909oposdf435rr-453";
	  Pattern p5 = Pattern.compile(numPattern);
	  Matcher m = p5.matcher(numStr);
	  List list = new ArrayList();
	  while(m.find()){
	   list.add(m.group());
	  }
	  System.out.println(list);
	 
	 }
	 
	}

----------------------------------------------
## For a given input string, how can you programmatically correct the number of spaces between words? We should essentially replace double or triple spacing with a single space character.


	public static void main(String[] args) {
 
	  String input = " This    is    a sentence.    ";
	  String output = input.trim().replaceAll("\\s+", " ");
	  System.out.println(output);
	 }
----------------------------------------------
## Given an input string, describe how you can find the number of words in the string.

	String[] words = input.split("\\s+");
	System.out.println(" Number of words = " + words.length);
	
----------------------------------------------
## Write a Regex that Verifies whether String ends with two digits

	Pattern ptn = Pattern.compile("\\d{2}$");


----------------------------------------------
## How to match regex with case insensitive?

	Pattern ptn = Pattern.compile("java", Pattern.CASE_INSENSITIVE);
	
----------------------------------------------	
## How to validate IP address using regular expression?
	
	 public class MyIpMatch {
 
		public static boolean isValidIP(String ipAddr){
			 
			Pattern ptn = Pattern.compile("^(\\d{1,3})\\.(\\d{1,3})\\.(\\d{1,3})\\.(\\d{1,3})$");
			Matcher mtch = ptn.matcher(ipAddr);
			return mtch.find();
		}
	 
		public static void main(String a[]){
			System.out.println("10.23.45.12 is valid? "+MyIpMatch.isValidIP("10.23.45.12"));
			System.out.println("10.2a.56.32 is valid? "+MyIpMatch.isValidIP("10.2a.56.32"));
			System.out.println("10.23.45 is valid? "+MyIpMatch.isValidIP("10.23.45"));
		}
	}

----------------------------------------------
## Program: How to validate user name using regular expression?
	
	The below given example shows how to validate a user name. The regular expression pattern allows lower case alphanumeric characters, allows '-', '_'. Incase if you want to support uppercase characters then regular expression should be ^[a-zA-Z0-9_-]{6,14}$

	public class MyUsernameValidate {
 
		private static Pattern usrNamePtrn = Pattern.compile("^[a-z0-9_-]{6,14}$");
		 
		public static boolean validateUserName(String userName){
			 
			Matcher mtch = usrNamePtrn.matcher(userName);
			if(mtch.matches()){
				return true;
			}
			return false;
		}
		 
		public static void main(String a[]){
			System.out.println("Is 'java2novice' a valid user name? "
							+validateUserName("java2novice"));
			System.out.println("Is 'cric' a valid user name? "
							+validateUserName("cric"));
			System.out.println("Is 'JAVA2NOVICE' a valid user name? "
							+validateUserName("JAVA2NOVICE"));
			System.out.println("Is 'java.2.novice' a valid user name? "
							+validateUserName("java.2.novice"));
			System.out.println("Is 'java_2-novice' a valid user name? "
							+validateUserName("java_2-novice"));
		}
	}
----------------------------------------------
## How to validate email address using regular expression?

	public class MyEmailValidate {
 
		private static Pattern emailNamePtrn = Pattern.compile(
		"^[_A-Za-z0-9-]+(\\.[_A-Za-z0-9-]+)*@[A-Za-z0-9]+(\\.[A-Za-z0-9]+)*(\\.[A-Za-z]{2,})$");
		 
		public static boolean validateEmailAddress(String userName){
			 
			Matcher mtch = emailNamePtrn.matcher(userName);
			if(mtch.matches()){
				return true;
			}
			return false;
		}
		 
		public static void main(String a[]){
			System.out.println("Is 'java2novice@gmail.com' a valid email address? "
										+validateEmailAddress("java2novice@gmail.com"));
			System.out.println("Is 'cric*7*&@yahoo.com' a valid email address? "
										+validateEmailAddress("cric*7*&@yahoo.com"));
			System.out.println("Is 'JAVA2NOVICE.gmail.com' a valid email address? "
										+validateEmailAddress("JAVA2NOVICE.gmail.com"));
		}
	}

----------------------------------------------
## How to validate password using regular expression?
	
	The below given example shows how to validate a password using regular expression. Here this regular expression allows must contain one digit, one lower case char, one upper case char, some special chars, length should be within 6 to 15 chars.

	public class MyPasswordValidate {
 
		private static Pattern pswNamePtrn = 
				Pattern.compile("((?=.*\\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%]).{6,15})");
			 
			public static boolean validatePassword(String userName){
				 
				Matcher mtch = pswNamePtrn.matcher(userName);
				if(mtch.matches()){
					return true;
				}
				return false;
			}
			 
			public static void main(String a[]){
				System.out.println("Is 'java2novice' a valid password? "
									+validatePassword("java2novice"));
				System.out.println("Is 'gabbarsingh' a valid password? "
									+validatePassword("gabbarsingh"));
				System.out.println("Is 'Java2NOVICE$' a valid password? "
									+validatePassword("Java2NOVICE$"));
				System.out.println("Is '234aBc#' a valid password? "
									+validatePassword("234aBc#"));
			}
		}


----------------------------------------------
## How to validate file extensions using regular expression in java?

	The below given example shows how to validate a file extensions using regular expression. The regular expression allows txt, doc, csv, and pdf file extensions only.
	
	
	public class MyFileExtenValidation {
 
		private static Pattern fileExtnPtrn = Pattern.compile("([^\\s]+(\\.(?i)(txt|doc|csv|pdf))$)");
			 
			public static boolean validateFileExtn(String userName){
				 
				Matcher mtch = fileExtnPtrn.matcher(userName);
				if(mtch.matches()){
					return true;
				}
				return false;
			}
			 
			public static void main(String a[]){
				System.out.println("Is 'java2novice.pdf' allowed file? "
								+validateFileExtn("java2novice.pdf"));
				System.out.println("Is 'cric.doc' allowed file? "
								+validateFileExtn("cric.doc"));
				System.out.println("Is 'java.gif' allowed file? "
								+validateFileExtn("java.gif"));
				System.out.println("Is 'novice.mp3' allowed file? "
								+validateFileExtn("novice.mp3"));
				System.out.println("Is 'java_2.jpeg' allowed file? "
								+validateFileExtn("java_2.jpeg"));
			}
		}

----------------------------------------------
## How to validate date format using regular expression in java?



	public class MyDateFormat {
 
		private static Pattern dateFrmtPtrn = 
				Pattern.compile("(0?[1-9]|[12][0-9]|3[01])/(0?[1-9]|1[012])/((19|20)\\d\\d)");
		 
		public static boolean validateDateFormat(String userName){
			 
			Matcher mtch = dateFrmtPtrn.matcher(userName);
			if(mtch.matches()){
				return true;
			}
			return false;
		}
		 
		public static void main(String a[]){
			System.out.println("Is '03/04/2012' a valid date format? "
							+validateDateFormat("03/04/2012"));
			System.out.println("Is '12/23/2012' a valid date format? "
							+validateDateFormat("12/23/2012"));
			System.out.println("Is '12/12/12' a valid date format? "
							+validateDateFormat("12/12/12"));
			System.out.println("Is '3/4/2012' a valid date format? "
							+validateDateFormat("3/4/2012"));
		}
	}
----------------------------------------------	
## How to capture or extract a value(s) from text using regular expression in java?


	public class MyGroupRegex {
 
		private static Pattern ptn = 
				Pattern.compile("(\\d{1,3})\\.(\\d{1,3})\\.(\\d{1,3})\\.(\\d{1,3})");
		 
		public static List<String> captureValues(String largeText){
			Matcher mtch = ptn.matcher(largeText);
			List<String> ips = new ArrayList<String>();
			while(mtch.find()){
				ips.add(mtch.group());
			}
			return ips;
		}
		 
		public static void main(String a[]){
			String str = "Hi my machine IP is 10.20.30.40 and i would like "+
				"to access port 80 from the host 23.12.56.34, which internally"+
				"connects to 3.90.23.65. Please process the request";
			System.out.println(captureValues(str));
		}
	}
----------------------------------------------	
## How to split a string using regular expression?

	public class MyTokens {
 
		public static void main(String a[]){
			 
			String str = "I have a cat. I play cricket with bat. I dont like rat,"+
				"i hate mats, now break it";
			Pattern ptn = Pattern.compile("(cat|rat|mat|bat)");
			String[] parts = ptn.split(str);
			for(String p:parts){
				System.out.println(p);
			}
		}
	}
	
----------------------------------------------
## How to replace all non-alphanumeric characters with empty strings?
 
	replaceAll("[^A-Za-z0-9]", "");

----------------------------------------------
## How to replace 2 or more spaces with single space in string and delete leading and trailing spaces?
	replaceAll("\\s{2,}", " ").trim();

Create a regular expression that accepts alphanumeric characters only. Its length must be five characters 
		
		public class RegexTutorial {
			public static void main(String args[]) {
				System.out.println(Pattern.matches("[a-zA-Z0-9]{5}", "java1"));
				System.out.println(Pattern.matches("[a-zA-Z0-9]{5}", "java12"));
				System.out.println(Pattern.matches("[a-zA-Z0-9]{5}", "JA1Va"));
				System.out.println(Pattern.matches("[a-zA-Z0-9]{5}", "Java$"));
			}
		}  
----------------------------------------------		
## Create a regular expression that accepts 10 digit numeric characters starting with 1, 2 or 3 only.	

	public class RegexTutorial{

		public static void main(String args[]) {
			System.out.println("Regex Using character classes and quantifiers");

			System.out.println(Pattern.matches("[123]{1}[0-9]{9}", "1953038949"));
			System.out.println(Pattern.matches("[123][0-9]{9}", "1993038949"));

			System.out.println(Pattern.matches("[123][0-9]{9}", "9950389490"));
			System.out.println(Pattern.matches("[123][0-9]{9}", "695338949"));
			System.out.println(Pattern.matches("[123][0-9]{9}", "885338949"));

			System.out.println("Regex Using Metacharacters");
			System.out.println(Pattern.matches("[123]{1}\\d{9}", "2885338949"));
			System.out.println(Pattern.matches("[123]{1}\\d{9}", "685308949"));

		}
	}
	
----------------------------------------------	
## https://www.youtube.com/watch?v=sa-TUpSx1JA
