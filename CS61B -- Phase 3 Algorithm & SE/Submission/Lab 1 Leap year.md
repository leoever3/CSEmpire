### Codes:

```java
/** Class that determines whether or not a year is a leap year.
 *  @author MorningStar
 */
public class LeapYear {

    /** Calls isLeapYear to print correct statement.
     *  @param  year to be analyzed
     */
    private static void checkLeapYear(int year) {
        if (isLeapYear(year)) {
            System.out.printf("%d is a leap year.\n", year);
        } else {
            System.out.printf("%d is not a leap year.\n", year);
        }
    }
    /** Determines whether the year is leap year */
    public static boolean isLeapYear(int year){
        boolean isLeapYear = false;
        if(year % 400 == 0){
            isLeapYear = true;
        }
        else if (year % 4 == 0 && year % 100 != 0){
            isLeapYear = true;
        }
        return isLeapYear;
    }

    /** Must be provided an integer as a command line argument ARGS. */
    public static void main(String[] args) {
        if (args.length < 1) {
            System.out.println("Please enter command line arguments.");
            System.out.println("e.g. java Year 2000");
        }
        for (int i = 0; i < args.length; i++) {
            try {
                int year = Integer.parseInt(args[i]);
                checkLeapYear(year);
            } catch (NumberFormatException e) {
                System.out.printf("%s is not a valid number.\n", args[i]);
            }
        }
    }
}

```

### How to run .java in a Terminal:

1. ```
   Subl <javaname.java>
   ```

2. ```
   $ ls    --to see whether we have the correct .java document
   ```

3. after writing the codes

```
$ javac LeapYear.java

$ javac is java compiler. --to create LeapYear.class

& java LeapYear --Run the program!
```

### Tips:

* If we want to add comment line arguments, we just put them after java LeapYear ________
* Save before compile.
* When we modify the code, we need to compile(javac) again.