# 🔐 Password Manager

This Password Manager is a GUI application built with Python's `tkinter` library. It allows users to generate secure passwords, store them alongside website names and emails, and retrieve passwords when needed. 

## 📂 Project Structure

- **Password Generator**: Generates a random password with a mix of letters, symbols, and numbers.
- **Data Storage**: Saves each website, email, and password combination to a `data.txt` file.
- **User Interface**: Simple interface for easy input, generation, and storage of login information.

---

## 🔧 Code Explanation

### 1. Password Generator
```python
def generate_password():
    letters = [...]
    numbers = [...]
    symbols = [...]

    password_letters = [choice(letters) for _ in range(randint(8, 10))]
    password_symbols = [choice(symbols) for _ in range(randint(2, 4))]
    password_numbers = [choice(numbers) for _ in range(randint(2, 4))]

    password_list = password_letters + password_symbols + password_numbers
    shuffle(password_list)

    password = "".join(password_list)
    password_entry.insert(0, password)
    pyperclip.copy(password)
```
- generate_password: Creates a secure password by combining random letters, numbers, and symbols. The password is automatically copied to the clipboard using pyperclip.

### 2. Save Password
```python
def save():
    website = website_entry.get()
    email = email_entry.get()
    password = password_entry.get()

    if len(website) == 0 or len(password) == 0:
        messagebox.showinfo(title="Oops", message="Please make sure you haven't left any fields empty.")
    else:
        is_ok = messagebox.askokcancel(title=website, message=f"These are the details entered: \nEmail: {email} "
                                                      f"\nPassword: {password} \nIs it ok to save?")
        if is_ok:
            with open("data.txt", "a") as data_file:
                data_file.write(f"{website} | {email} | {password}\n")
                website_entry.delete(0, END)
                password_entry.delete(0, END)
```
- save: Saves the website, email, and password into data.txt after confirming with the user. The fields are cleared after saving.

### 3. UI Setup
```python
window = Tk()
window.title("Password Manager")
window.config(padx=50, pady=50)

canvas = Canvas(height=200, width=200)
logo_img = PhotoImage(file="logo.png")
canvas.create_image(100, 100, image=logo_img)
canvas.grid(row=0, column=1)

# Labels and Entries setup for input fields
website_entry = Entry(width=35)
website_entry.grid(row=1, column=1, columnspan=2)
website_entry.focus()
email_entry = Entry(width=35)
email_entry.grid(row=2, column=1, columnspan=2)
email_entry.insert(0, "your_email@example.com")
password_entry = Entry(width=21)
password_entry.grid(row=3, column=1)

# Buttons
generate_password_button = Button(text="Generate Password", command=generate_password)
generate_password_button.grid(row=3, column=2)
add_button = Button(text="Add", width=36, command=save)
add_button.grid(row=4, column=1, columnspan=2)
```
- Window Configuration: Creates a Tkinter window with a title and padding.
- Logo Display: Displays a logo image using canvas.
- Labels and Entries: Labels and entry fields for user inputs like website, email, and password.
- Buttons: A button to generate a password and another to save the information.

## 🚀 How to Run
1. Make sure to install required libraries:
```bash
pip install pyperclip
```
2. Save an image file named logo.png in the same directory as the script.
3. Run the application:
```bash
python script_name.py
```
4. Enter a website, email, and either generate a password or enter your own. Click "Add" to save.

## 📝 Notes
- Password Generation: The password generator provides random and secure passwords by mixing letters, numbers, and symbols.
- Clipboard Copying: Generated passwords are automatically copied to the clipboard for convenience.
- Storage: The data.txt file in the directory will contain all saved login details.

## 🔗 Additional Resources
- tkinter Documentation
- pyperclip Documentation
- Password Strength Best Practices
