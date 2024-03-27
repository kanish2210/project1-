# project1-
student management system

import mysql.connector

class Database:
    def _init_(self):
        self.connection = mysql.connector.connect(
            host="localhost",
            user="root",
            password="Kanish@22",
            database="student_management"
        )
        self.cursor = self.connection.cursor()

    def execute_query(self, query, data=None):
        if data:
            self.cursor.execute(query, data)
        else:
            self.cursor.execute(query)
        self.connection.commit()

    def fetch_data(self, query):
        self.cursor.execute(query)
        return self.cursor.fetchall()

    def _del_(self):
        self.connection.close()

class Admin:
    def _init_(self, admin_id, password):
        self.admin_id = admin_id
        self.password = password

    def login(self):
        
        pass

    def update_data(self, table, id, field, new_value):
        query = f"UPDATE {table} SET {field} = %s WHERE id = %s"
        db.execute_query(query, (new_value, id))

    def delete_data(self, table, id):
        query = f"DELETE FROM {table} WHERE id = %s"
        db.execute_query(query, (id,))

    def insert_data(self, table, data):
        columns = ', '.join(data.keys())
        placeholders = ', '.join(['%s'] * len(data))
        query = f"INSERT INTO {table} ({columns}) VALUES ({placeholders})"
        db.execute_query(query, tuple(data.values()))

class Student:
    def _init_(self, student_id, name, age, sex, mark, class_teacher_id):
        self.id = student_id
        self.name = name
        self.age = age
        self.sex = sex
        self.mark = mark
        self.class_teacher_id = class_teacher_id

class Teacher:
    def _init_(self, teacher_id, name, age, sex, salary):
        self.id = teacher_id
        self.name = name
        self.age = age
        self.sex = sex
        self.salary = salary

class Principal:
    def _init_(self, principal_id, name, age, salary):
        self.id = principal_id
        self.name = name
        self.age = age
        self.salary = salary

def select_option():
    print("Select an option:")
    print("1. Student")
    print("2. Teacher")
    print("3. Principal")
    choice = input("Enter your choice: ")
    return choice

def perform_operation(option):
    admin = Admin(1, "password") 
    if option == '1':
        perform_student_operation(admin)
    elif option == '2':
        perform_teacher_operation(admin)
    elif option == '3':
        perform_principal_operation(admin)
    else:
        print("Invalid option")

def perform_student_operation(admin):
    print("Student Operations:")
    print("1. Update")
    print("2. Delete")
    print("3. Insert")
    operation = input("Enter operation number: ")
    if operation == '1':
        student_id = input("Enter student ID: ")
        field = input("Enter field to update: ")
        new_value = input("Enter new value: ")
        admin.update_data('student', student_id, field, new_value)
    elif operation == '2':
        student_id = input("Enter student ID to delete: ")
        admin.delete_data('student', student_id)
    elif operation == '3':
        name = input("Enter student name: ")
        age = input("Enter student age: ")
        sex = input("Enter student sex: ")
        mark = input("Enter student mark: ")
        class_teacher_id = input("Enter class teacher ID: ")
        data = {'name': name, 'age': age, 'sex': sex, 'mark': mark, 'class_teacher_id': class_teacher_id}
        admin.insert_data('student', data)
    else:
        print("Invalid operation")

def perform_teacher_operation(admin):
    
    pass

def perform_principal_operation(admin):

    pass

def main():
    db = Database()
    option = select_option()
    perform_operation(option)

if __name__ == "_main_":
    main()
