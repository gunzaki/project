import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.util.Scanner;

public class AgeCalc {

    public static int calculateAge(LocalDate birthDate) {
        LocalDate today = LocalDate.now();
        int age = today.getYear() - birthDate.getYear();

        if (today.getDayOfYear() < birthDate.getDayOfYear()) {
            age--;
        }

        return age;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Hello there! Welcome to our Age Calculator System!");

        while (true) {
            
            System.out.print("Please enter your birth date (YYYY-MM-DD): ");
            String birthDateInput = scanner.nextLine();

            if (birthDateInput.equalsIgnoreCase("exit")) {
                System.out.println("Thank you for using our program. Goodbye!");
                break;
            }

            try {

                DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");
                LocalDate birthDate = LocalDate.parse(birthDateInput, formatter);

                int age = calculateAge(birthDate);
                System.out.println("You are " + age + " years old.");

                if (age < 18) {
                    System.out.println("You are a minor.");
                } else {
                    System.out.println("You are in legal age.");
                }

                System.out.print("Do you want to try again? (yes/no): ");
                String tryAgain = scanner.nextLine();
                if (!tryAgain.equalsIgnoreCase("yes")) {
                    System.out.println("Thank you for using our program. Goodbye!");
                    break;
                }

            } catch (DateTimeParseException e) {
                System.out.println("Invalid date format. Please use YYYY-MM-DD.");
            }
        }

        scanner.close();
    }
}