# -NumeralSystemConverterProject
My solution to  JetBrains Academy Numeral System Converter stage 6/6
Task description: 
We’re all quite used to our good old decimal system of numerals. But let’s not forget that there are countless other ways to count! Whether we convert numbers from one system to another just for fun or to store large data more efficiently, a converter would be helpful. In this project you will create a mathematical helper that will help you convert numbers from system M to system N.
import java.util.Scanner;

public class stage6of6MySolution2 {

	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		String[] input = new String[3];
		int count = 0;
		while (count < 3) {
			input[count] = scan.nextLine();
			count++;
		}
		scan.close();
		//check for input error
		checkInput(input);
		
        int sourceRadix = Integer.parseInt(input[0]);
        String sourceNumber = input[1];
        int targetRadix = Integer.parseInt(input[2]);
        String[] parts = sourceNumber.split("\\.");
        
      //convert integer to decimal
        int decimalIntegerPart = 0;
        if (sourceRadix == 1) {
        	decimalIntegerPart = parts[0].length();
        } else {
        	decimalIntegerPart = Integer.parseInt(parts[0], sourceRadix);
        }
        
        //convert integer to new base
        String integerNewBase = "";
        if(targetRadix == 1) {
        	integerNewBase = "1".repeat(decimalIntegerPart);
        } else {
        	integerNewBase = Integer.toString(decimalIntegerPart, targetRadix);
        }
        
        StringBuilder sb = new StringBuilder(integerNewBase);
        
        if (parts.length == 2) {
        	   //convert fractional to decimal
            double fractionalDec = 0;
            char[] fractionalArr = parts[1].toCharArray();
            for (int i = 0; i < fractionalArr.length; i++) {
                char ch = fractionalArr[i];
                double val = Character.getNumericValue(ch);
                fractionalDec += val/Math.pow(sourceRadix, i+1);
            }
            
            //convert fractional to new base
            StringBuilder sbf = new StringBuilder();
            for (int i = 0; i < 5; i++) {
                fractionalDec = fractionalDec * targetRadix;
                int integer = (int) fractionalDec;
                sbf.append(Character.forDigit(integer, targetRadix));
                fractionalDec = fractionalDec % integer;
            }
            sb.append(".");
            sb.append(sbf);
            
        }
		
        System.out.println(sb);
	}
	
	private static void checkInput(String[] input) {
		 if (!input[0].matches("^(([3][0-6])|([1-2][0-9])|([1-9]))") || 
				 !input[1].matches("[\\da-z]+(\\.[\\da-z]+)?") || 
				 !input[2].matches("^(([3][0-6])|([1-2][0-9])|([1-9]))")) {
	            System.out.println("error!");
	            
	           System.exit(0);
	        }
	}

}
