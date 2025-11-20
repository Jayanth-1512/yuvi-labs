
import java.util.Random;
import java.util.Scanner;

public class NumericGridHighlighter {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Random random = new Random();

        int n = readGridSize(sc);         
        int[][] grid = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
  
                grid[i][j] = 2 + 2 * random.nextInt(10);
            }
        }

        System.out.println();
        System.out.println("Generated 2D array:");
        printGrid(grid, -1);             

       
        int x = readHighlightNumber(sc);

        System.out.println();
        System.out.println("Array with " + x + " highlighted:");
        int count = printGrid(grid, x);  
        System.out.println();
        System.out.println("Number " + x + " appeared " + count + " time(s)");

        sc.close();
    }

  
    private static int readGridSize(Scanner sc) {
        int n;
        while (true) {
            System.out.print("Enter array size (for NxN array): ");
            if (!sc.hasNextInt()) {
                System.out.println("Invalid input. Please enter a whole number.");
                sc.next();
                continue;
            }
            n = sc.nextInt();
            if (n <= 0) {
                System.out.println("Size must be a positive number.");
            } else {
                break;
            }
        }
        return n;
    }


    private static int readHighlightNumber(Scanner sc) {
        int x;
        while (true) {
            System.out.print("Enter a number to highlight (even number 2–20): ");
            if (!sc.hasNextInt()) {
                System.out.println("Invalid input. Please enter a number.");
                sc.next();
                continue;
            }
            x = sc.nextInt();
            if (x < 2 || x > 20 || x % 2 != 0) {
                System.out.println("Number must be EVEN and between 2 and 20.");
            } else {
                break;
            }
        }
        return x;
    }

    
    private static int printGrid(int[][] grid, int highlightVal) {
        int n = grid.length;
        int count = 0;
        System.out.print("   "); 
        for (int j = 0; j < n; j++) {
            System.out.printf(" %02d ", j);
        }
        System.out.println();

     
        printBorderLine(n);
        for (int i = 0; i < n; i++) {
            System.out.printf("%02d ", i);  
            System.out.print("|");
            for (int j = 0; j < n; j++) {
                int val = grid[i][j];
                if (val == highlightVal) {
                   
                    System.out.printf("[%2d]|", val);
                    count++;
                } else {
                    System.out.printf(" %2d |", val);
                }
            }
            System.out.println();
            printBorderLine(n);
        }
        return count;
    }
    private static void printBorderLine(int n) {
        System.out.print("   "); 
        for (int j = 0; j < n; j++) {
            System.out.print("+---");
        }
        System.out.println("+");
    }
}
