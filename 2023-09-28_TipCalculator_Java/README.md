# cp132-homework3-kcraycraft45
cp132-homework3-kcraycraft45 created by GitHub Classroom
import java.text.DecimalFormat;
import java.util.Scanner;
/*Kaci Craycraft - kcraycraft45
    Homework3*/

public class Main
{
    public static void main(String[] args)
    {
        Scanner input = new Scanner(System.in);//import your scanner
        DecimalFormat money = new DecimalFormat("#0.00");//Declaring my decimal formatting to match money's standard format
        final double TIP_THRESH = 50;//TIP_THRESH is the threshold for when your cumulative tips stop going to you
        final double TIP_PERCENT = 0.15;//15% of bill is the tip

        int ticker = 1;//initializing variables I need for my user prompt to be accurate
        int tableCount = 1;
        int hundreds = 1;

        System.out.print("How much was your " + ticker + "st table's bill? (type 0 when finished): $");//priming input
        double bill = input.nextDouble();
        double cumTips = 0;//initializing variables for my calculations
        double salesTotal = 0;
        double tips = 0;
        double replacement = 0;

        while(bill != 0)//will loop until user ends the prompt
        {

            tips = bill * TIP_PERCENT;//calculating tip depending on the bill
            cumTips = cumTips + tips;//cum = cumulative, sorry.  Adding the tip input to the tip total every loop
            salesTotal = bill + salesTotal; //adding the bill input to the sales total every loop

            if(cumTips > TIP_THRESH)//if tips are greater than $50, they only receive $50
            {
                replacement = cumTips;//needed a holder value for total tips earned to distinguish from tips received.
                cumTips = TIP_THRESH;
                System.out.println("For a bill of $" + money.format(bill) + " you earned $" + money.format(tips) + " in tips, totaling $" + money.format(replacement));

            }
            else//otherwise they receive their total tips
            {
                System.out.println("For a bill of $" + money.format(bill) + " you earned $" + money.format(tips) + " in tips, totaling $" + money.format(cumTips) + ".");
            }

            ticker++;//adding one to my ticker (how many times the user has been prompted)
            tableCount = ticker % 10;//reducing this ticker value to just the ones integer, removing the tens, hundreds, thousands, etc. value
            hundreds = ticker % 100;//reducing the ticker to just the tens and ones integers, removing the hundreds, thousands, and so on

            /*the rules for when you use "st", "nd", "rd", and "th" after an integer are as follows
             * If the number ends in 1, 2, and 3, excluding numbers ending in 11, 12 and 13
             *   then, the integer is appended by "st", "nd" and "rd" respectively.
             *   Otherwise, the number is appended by "th"
             *
             * I really wanted to include this in my code as a personal challenge to myself.
             *
             * In a 24 hour day, assuming a server receives payment from 1 table a second,
             *   they will account for the bills of 86,400 tables.
             *   (I know this is unrealistic, but I needed an absolute maximum the program will never conceivably reach)
             *   Thus, I tested the code for 100,000; 100,001; 100,002; 100,003; 100,011; 100,0012; and 100,013.
             *
             * It works.
             * However, there is a flaw in the program, being that you can only set your ticker to certain values when initializing.*/
            if(tableCount == 1 && hundreds != 11)
            {
                System.out.print("How much was your " + ticker + "st table's bill? (type 0 when finished): $");

            }
            else if(tableCount == 2 && hundreds != 12)
            {
                System.out.print("How much was your " + ticker + "nd table's bill? (type 0 when finished): $");
            }
            else if(tableCount == 3 && hundreds != 13)
            {
                System.out.print("How much was your " + ticker + "rd table's bill? (type 0 when finished): $");
            }
            else
            {
                System.out.print("How much was your " + ticker + "th table's bill? (type 0 when finished): $");

            }
            bill = input.nextDouble();//receiving the next input from the user for bill amount


        }
        input.close();//outside the while loop, we stop processing bill values
        System.out.println("For a sales total of $" + money.format(salesTotal) + " you will leave with $" + money.format(cumTips) + " in tips for today.");
        // ^^informing the server of the total tips they will leave with
        System.out.println("Thank you!");

    }
}
