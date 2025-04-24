import sqlite3
import bcrypt
import random
import string

def create_database():
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    cursor.execute('''
        CREATE TABLE IF NOT EXISTS users (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            username TEXT UNIQUE NOT NULL,
            password TEXT NOT NULL
        )
    ''')
    conn.commit()
    conn.close()
def hash_password(password):
    salt = bcrypt.gensalt()
    hashed = bcrypt.hashpw(password.encode(), salt)
    return hashed.decode()  # نحولها من bytes إلى string

def add_user(username, password):
    try:
        conn = sqlite3.connect("users.db")
        cursor = conn.cursor()
        hashed_password = hash_password(password)  # تشفير كلمة المرور
        cursor.execute("INSERT INTO users (username, password) VALUES (?, ?)", (username, hashed_password))
        conn.commit()
        conn.close()
        print("✅ تم إنشاء الحساب بنجاح!")
    except sqlite3.IntegrityError:

        print("❌ اسم المستخدم موجود بالفعل، حاول باسم آخر.")

def check_password(username, password):
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    cursor.execute("SELECT password FROM users WHERE username = ?", (username,))
    user = cursor.fetchone()
    conn.close()

    if user and bcrypt.checkpw(password.encode(), user[0].encode()):
        return "✅ تم تسجيل الدخول بنجاح!"
    else:
        return "❌ اسم المستخدم أو كلمة المرور غير صحيحة."
def update_password(username, old_password, new_password):
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    cursor.execute("SELECT password FROM users WHERE username = ?", (username,))
    user = cursor.fetchone()

    if user and bcrypt.checkpw(old_password.encode(), user[0].encode()):
        hashed_new_password = hash_password(new_password)
        cursor.execute("UPDATE users SET password = ? WHERE username = ?", (hashed_new_password, username))
        conn.commit()
        conn.close()
        return "✅ تم تحديث كلمة المرور بنجاح!"
    else:
        conn.close()
        return "❌ كلمة المرور القديمة غير صحيحة أو اسم المستخدم غير موجود."
# دالة لإنشاء كلمة مرور عشوائية جديدة عند نسيانها
def generate_temporary_password():
    characters = string.ascii_letters + string.digits
    return ''.join(random.choice(characters) for i in range(10))

# دالة لاسترجاع كلمة المرور عند نسيانها (إعادة تعيينها)
def reset_password(username):
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM users WHERE username = ?", (username,))
    user = cursor.fetchone()

    if user:
        new_password = generate_temporary_password()
        hashed_new_password = hash_password(new_password)
        cursor.execute("UPDATE users SET password = ? WHERE username = ?", (hashed_new_password, username))
        conn.commit()
        conn.close()
        return f"✅ تم إعادة تعيين كلمة المرور، كلمة المرور الجديدة: {new_password}"
    else:
        conn.close()
        return "❌ اسم المستخدم غير موجود."

# تشغيل الكود
if __name__ == "__main__":
    create_database()  # إنشاء قاعدة البيانات

    while True:
        print("\n1️⃣ تسجيل مستخدم جديد")
        print("2️⃣ تسجيل الدخول")
        print("3️⃣ تحديث كلمة المرور")
        print("4️⃣ تعيين كلمة مرور قويه")
        print("5️⃣ خروج")
        choice = input("👉 اختر خيارًا: ")

        if choice == "1":
            username = input("📝 أدخل اسم المستخدم: ")
            password = input("🔒 أدخل كلمة المرور: ")
            add_user(username, password)

        elif choice == "2":
            username = input("📝 أدخل اسم المستخدم: ")
            password = input("🔑 أدخل كلمة المرور: ")
            print(check_password(username, password))

        elif choice == "3":
            username = input("📝 أدخل اسم المستخدم: ")
            old_password = input("🔑 أدخل كلمة المرور القديمة: ")
            new_password = input("🆕 أدخل كلمة المرور الجديدة: ")
            print(update_password(username, old_password, new_password))

        elif choice == "4":
            username = input("📝 أدخل اسم المستخدم لتعيين كلمة المرور: ")
            print(reset_password(username))

        elif choice == "5":
            print("👋 وداعًا!")
            break

        else:
            print("⚠️ خيار غير صحيح، حاول مرة أخرى.")
