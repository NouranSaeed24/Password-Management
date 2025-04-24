# Password Management
# 🔐 User Management System with SQLite & bcrypt

This is a simple user management system built with Python. It allows users to register, log in, update passwords, and reset forgotten passwords using secure bcrypt hashing and an SQLite database.

## 📦 Features

- ✅ User registration with unique usernames
- 🔒 Password hashing with bcrypt
- 🔐 Secure login authentication
- ♻️ Password update with old password verification
- 🛠️ Password reset with randomly generated strong passwords

## 💡 Technologies Used

- Python 3
- SQLite (built-in database)
- bcrypt for secure password hashing

## ⚙️ How to Run

1. **Install dependencies**  
   Run the following command to install `bcrypt`:
   ```bash
   pip install bcrypt
##Sample Menu Interface

1️⃣ Register a new user
2️⃣ Log in
3️⃣ Update password
4️⃣ Reset password
5️⃣ Exit

##Notes

-Passwords are securely hashed using bcrypt before storing them in the database.
-Temporary passwords are randomly generated using letters and digits.
-This project is for educational/demo purposes. For production-grade applications, always follow the latest security standards.
