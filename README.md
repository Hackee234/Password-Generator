🧾 What is a Password Generator?
A password generator is a tool that automatically creates secure, random passwords based on user-defined criteria such as:

Length of the password

Types of characters (uppercase, lowercase, digits, special symbols)

This ensures that the passwords are hard to guess or crack, making user accounts and data more secure.

🎯 Purpose of the Project
The main goal of this project is to:

Help users create strong and customizable passwords

Avoid weak or easily guessable passwords

Demonstrate Python programming skills like string handling, conditionals, loops, and randomness

⚙️ How It Works (Step-by-Step)
User Input:

The program asks the user for the desired length of the password.

The user chooses which character types to include:

Uppercase letters (A–Z)

Lowercase letters (a–z)

Numbers (0–9)

Special characters (!, @, #, etc.)

Character Pool Creation:

Based on user choices, the program builds a pool of characters using Python’s string module.

Example: If the user selects uppercase + digits, the pool will contain A–Z and 0–9.

Password Generation:

Random characters are selected from the pool using the random.choice() function.

The password is constructed by repeating this selection process for the desired length.

Output:

The final password is displayed to the user.

🧠 Python Concepts Used
Modules:

random for randomness

string for predefined character sets

Functions: For modular design (e.g., get_user_preferences(), generate_password())

Control Structures: If-else conditions, loops

User Input: Using input() to interact with users

