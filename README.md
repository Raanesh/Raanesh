import mysql.connector

myproject = mysql.connector.connect(host= "localhost", user = "DIneshsekar", password = "Dradha@5192", db = "college")
print(myproject)
command_handler = myproject.cursor(buffered=True)


def admin_session():
    print("Login success")
    while True:
        print("")
        print("Admin menu")
        print("""
        1.Register New Student
        2.Register New Teacher
        3.Delete Existing Student
        4.Delete Existing Teacher
        5.Logout
        """)
        user_option = int(input("Option : "))
        if user_option == 1:
            print("/n Regiseter New Student")
            user_name = input("Enter your name : ")
            password = input("Enter student password : ")
            query_val = (user_name, password)
            command_handler.execute("insert into users(id, username, password, privilege) values(Null, %s, %s,'student')", query_val)
            myproject.commit()
            print(user_name , "has been regisetered successfully student")
        elif user_option ==2:
            print("/n Regiseter New Teacher")
            user_name = input("Enter the teacher name : ")
            password = input("Enter the teacher password : ")
            query_val = (user_name, password)
            command_handler.execute("insert into users(id, username, password, privilege) values(Null, %s, %s,'teacher')", query_val)
            myproject.commit()
            print(user_name, "has been regisetered successfully teacher")

        elif user_option ==3:
            print("\n Delete Existing Students Account")
            username = input("student name : ")
            query_val = (username, "student")
            command_handler.execute("DELETE from users WHERE username = %s And privilege = %s", query_val)
            myproject.commit()
            if command_handler.rowcount < 1:
                print("User not found")
            else:
                print(username, "has been deleted")
        elif user_option ==4:
            print("\n Delete Existing Teacher Account")
            username = input("Teacher name : ")
            query_val = (username, "teacher")
            command_handler.execute("DELETE from users WHERE username = %s And privilege = %s", query_val)
            myproject.commit()
            if command_handler.rowcount < 1:
                print("user not found")
            else:
                print(username, "has been deleted")

        elif user_option ==5:
            print("thank you")
            break
        else:
            print("no valid option selected")



def auth_admin():
    print("")
    print("Admin login")
    print("")
    user_name = input("enter the name here : ")
    password = input("enter the password here : ")
    if user_name == "admin":
        if password == "password":
            admin_session()
        else:
            print("incorrect password")
    else:
        print("Login details not recognised : ")

def main():
    while True:
        print("welcome to the college system")
        print("""
        1.Login as student
        2.Login as teacher
        3.Login as admin""")

        user_option = int(input("Option : "))
        if user_option == 1:
            print("Student login")
        elif user_option == 2:
            print("Teacher login :")
        elif user_option ==3:
            auth_admin()
            print("Admin login")
        else:
            print("invalid option selected : ")
main()
