# 🔹 Subset 1: Import Required Modules
import string
import random

try:
    import pyperclip  # Optional module to copy password to clipboard
    CLIPBOARD_AVAILABLE = True
except ImportError:
    CLIPBOARD_AVAILABLE = False


# 🔹 Subset 2: Get User Preferences
def get_user_preferences():
    """
    Get the password length and character type preferences from the user.
    Ensures input validation.
    """
    print("🔐 Welcome to the Advanced Password Generator\n")

    # Password length input
    while True:
        try:
            length = int(input("Enter the desired password length (min 4): "))
            if length < 4:
                print("❗ Password should be at least 4 characters long for security.")
                continue
            break
        except ValueError:
            print("❗ Please enter a valid integer.")

    # Character type inputs
    print("\nSelect character types to include in the password:")
    use_upper = input("Include UPPERCASE letters (A-Z)? (y/n): ").strip().lower() == 'y'
    use_lower = input("Include lowercase letters (a-z)? (y/n): ").strip().lower() == 'y'
    use_digits = input("Include digits (0-9)? (y/n): ").strip().lower() == 'y'
    use_special = input("Include special characters (!, @, #, etc.)? (y/n): ").strip().lower() == 'y'

    if not (use_upper or use_lower or use_digits or use_special):
        print("❌ At least one character type must be selected.")
        return get_user_preferences()

    return length, use_upper, use_lower, use_digits, use_special


# 🔹 Subset 3: Build Character Pool and Assure Minimum Inclusion
def build_character_pool(use_upper, use_lower, use_digits, use_special):
    """
    Builds the character pool and guarantees inclusion of at least
    one character from each selected type.
    Returns: (pool, required_chars)
    """
    pool = ""
    required_chars = []

    if use_upper:
        pool += string.ascii_uppercase
        required_chars.append(random.choice(string.ascii_uppercase))

    if use_lower:
        pool += string.ascii_lowercase
        required_chars.append(random.choice(string.ascii_lowercase))

    if use_digits:
        pool += string.digits
        required_chars.append(random.choice(string.digits))

    if use_special:
        pool += string.punctuation
        required_chars.append(random.choice(string.punctuation))

    return pool, required_chars


# 🔹 Subset 4: Generate Password with Inclusion Guarantee
def generate_password(length, pool, required_chars):
    """
    Generate a secure password of given length using the pool and
    ensure required characters are included at least once.
    """
    if len(pool) == 0:
        return "❗ Error: No characters available to generate password."

    # Fill the rest of the password length with random choices
    remaining_length = length - len(required_chars)
    password = required_chars + [random.choice(pool) for _ in range(remaining_length)]

    # Shuffle to randomize required character positions
    random.shuffle(password)

    return ''.join(password)


# 🔹 Subset 5: Copy to Clipboard (Optional)
def copy_to_clipboard(password):
    """
    Copies the generated password to the clipboard if pyperclip is installed.
    """
    if CLIPBOARD_AVAILABLE:
        pyperclip.copy(password)
        print("📋 Password copied to clipboard!")
    else:
        print("⚠️ pyperclip not installed. Install with 'pip install pyperclip' to enable clipboard copying.")


# 🔹 Subset 6: Main Program Loop
def main():
    """
    Main function to coordinate user input, generation, and output.
    """
    while True:
        # Step 1: Get user preferences
        length, upper, lower, digits, special = get_user_preferences()

        # Step 2: Build character pool and required characters
        pool, required = build_character_pool(upper, lower, digits, special)

        # Step 3: Generate the password
        password = generate_password(length, pool, required)

        # Step 4: Show the password
        print("\n✅ Your Secure Password:")
        print(password)

        # Step 5: Optional clipboard copy
        if input("Copy password to clipboard? (y/n): ").strip().lower() == 'y':
            copy_to_clipboard(password)

        # Step 6: Option to generate another
        again = input("\nGenerate another password? (y/n): ").strip().lower()
        if again != 'y':
            print("🔒 Thank you for using the Password Generator!")
            break


# 🔹 Entry Point
if __name__ == "__main__":
    main()

