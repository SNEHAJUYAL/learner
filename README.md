# learner
import mysql.connector

mydb=mysql.connector.connect(host="localhost",user="root",password = "HELLO6456")
mycursor=mydb.cursor()
mycursor.execute("create database if not exists library")
mycursor.execute("use library")

#CREATING REQUIRED TABLES

mycursor.execute("create table if not exists lib_member( Serial_No mediumint auto_increment primary key ,cardno varchar(50) , name_of_person varchar(30), phone_no varchar(20), address varchar(60), dob date)")

mycursor.execute("create table if not exists books( Serial_No mediumint auto_increment primary key, book_name varchar(30), book_no int, genre varchar(10), authors_name varchar(25), language varchar(15))")

mycursor.execute("create table if not exists lib_transaction( Serial_No mediumint auto_increment primary key , cardno varchar(50) references lib_member(cardno), book_name varchar(20), date_of_lend date, date_of_return date)")

mycursor.execute("create table if not exists buy_new_books( Serial_No mediumint auto_increment primary key , orderno varchar(6) ,name_of_book varchar(20),del_date date,price char(4))")
mydb.commit()



def clear():
    for i in range(1):
        print()

#1. TO CREATE A LIBRARY ACCOUNT
        
def add_new_account():
    print("FILL ALL PERSONAL DETAILS OF ACCOUNT HOLDER\n\n")
    cardno = input('Enter your card no : ')
    name_of_person = input("Enter your name :  ")
    phone_no = input("Enter your phone no :  ")
    address = input("Enter your address :  ")
    dob = input("Enter your date of birth(yyyy-mm-dd) :  ")
    mycursor.execute("insert into lib_member(cardno,name_of_person,phone_no,address,dob) values('"+cardno+"','"+name_of_person+"','"+phone_no+"','"+address+"','"+dob+"')")
    mydb.commit()
    print("\n\nACCOUNT IS SUCCESSFULLY CREATED!!!\n\n")
    input("\n\n\n Press any enter to continue....\n")

    
#2. TO SEE DETAILS OF CARD HOLDER
            
def display_account_info():
    cardno = input("Enter card no :  ")
    mycursor.execute("select  *  from lib_member where cardno="+cardno+"")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
        
            
#3. TO UPDATE CARD HOLDER INFORMATION
                   
#To update name
        
def update_name():
    print("List of Members")
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    cardno =input("Enter card no.  :  ")
    name_of_person = input("Enter new name  :  ")
    mycursor.execute("update lib_member set name_of_person = '"+name_of_person+"' where cardno = "+cardno+"")
    mydb.commit()
    print("\n\nName has been updated\n\n")
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
            
#TO UPDATE PHONE NUMBER

def update_phone_number():
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    cardno = input("Enter card no :  ")
    phone_no = input("Enter new phone no :  ")
    mycursor.execute("update lib_member set phone_no = '"+phone_no+"' where cardno = "+cardno+"")
    mydb.commit()
    print("\n\nNumber has been updated\n\n")
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
                
#TO UPDATE ADDRESS

def update_address():
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    cardno = input("Enter card no :  ")
    address = input("Enter new address :  ")
    mycursor.execute("update lib_member set address = '"+address+"' where cardno = "+cardno+"")
    mydb.commit()
    print("\n\nAddress has been updated\n\n")
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")

#TO UPDATE DATE OF BIRTH
                
def update_dob():
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    cardno = input("Enter card no :  ")
    dob = input("Enter new date of birth(yyyy-mm-dd) :  ")
    mycursor.execute("update lib_member set dob = '"+dob+"' where cardno = "+cardno+"")
    mydb.commit()
    print("\n\nDate of birth has been updated\n\n")
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")


def update_card_holder_info():
    while True:
        clear()
        print("1.  Update Name")
        print(" ")
        print("2.  Update Phone no")
        print(" ")
        print("3.  Update Address")
        print(" ")
        print("4.  Update Date of Birth")
        print(" ")
        print("5.  Exit to Main Menu")
        print("\n\n")
        choice = int(input("Enter your choice.....:  "))

        if choice == 1:
            update_name()
        if choice == 2:
            update_phone_number()
        if choice == 3:
            update_address()
        if choice == 4:
            update_dob()
        if choice == 5:
            break
    input("\n\n\n Press any enter to continue....\n")



#4. TO DELETE AN ACCOUNT
                
def delete_account():
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    cardno= input("Enter card no:")
    mycursor.execute("delete from lib_member where cardno = "+cardno+"")
    mydb.commit()
    print("\n\nRemoved succesfully\n\n")
    mycursor.execute("select * from lib_member")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")


                
#5. TO ADD NEW BOOK
                
def add_book():
    print("FILL ALL BOOK DETAILS \n\n")
    book_name = input("Enter book  name :  ")
    book_no = input("Enter book number (limit 5 characters) :  ")
    genre = input("Enter genre :  ")
    authors_name = input("Enter the authors name :  ")
    language = input("Enter the language of book :  ")
    mycursor.execute("insert into books values('"+book_name+"','"+book_no+"','"+genre+"','"+authors_name+"','"+language+"')")
    mydb.commit()
    print("\n\nBook added  succesfully......\n\n")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")

        
#6. TO DISPLAY BOOK
        
def display_books():
    mycursor.execute("select *from books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")


            
#7. TO UPDATE BOOK DETAILS
            
#TO UPDATE BOOK NAME
        
def update_book_name():
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    book_no = input("Enter book no. :  ")
    book_name = input("Enter new name :  ")
    mycursor.execute("update books set book_name = '"+book_name+"' where book_no = '"+book_no+"'")
    mydb.commit()
    print("\n\nName has been updated\n\n")
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
                
#TO UPDATE GENRE
 
def update_genre():
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    book_no = input("Enter card no. :  ")
    genre = input("Enter new genre :  ")
    mycursor.execute("update books set genre = '"+genre+"' where book_no = '"+book_no+"'")
    mydb.commit()
    print("\n\nGenre has been updated\n\n")
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
                
#TO UPDATE AUTHOR NAME
                
def update_author_name():
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    book_no = input("Enter book no :  ")
    author = input("Enter new authors name :  ")
    mycursor.execute("update books set authors_name = '"+author+"' where book_no = '"+book_no+"'")
    mydb.commit()
    print("\n\nAuthors name has been updated\n\n")
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
                
#TO UPDATE LANGUAGE
                
def update_language():
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    book_no = input("Enter book no :  ")
    language = input("Enter new language :  ")
    mycursor.execute("update books set language = '"+language+"' where book_no = '"+book_no+"'")
    mydb.commit()
    print("\n\nLanguage has been updated\n\n")
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
        

def update_book_details():
    while True:
        clear()
        print("1.  Update Book Name")
        print("\n")
        print("2.  Update Genre")
        print("\n")
        print("3.  Update Author Name")
        print("\n")
        print("4.  Update Language")
        print("\n")
        print("5.  Exit to Main Menu")
        print("\n\n")
        
        choice = int(input("Enter your choice.....: "))

        if choice == 1:
            update_book_name()
        if choice == 2:
            update_genre()
        if choice == 3:
            update_author_name()
        if choice == 4:
            update_language()
        if choice == 5:
            break

            
                
#8. TO DELETE A BOOK
                
def delete_book():
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    book_no = input("Enter book no :  ")
    mycursor.execute("delete from books where book_no = '"+book_no+"'")
    mydb.commit()
    print("\n\nRemoved succesfully.....\n\n")
    mycursor.execute("select *from books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")


            
#9. TO ISSUE A BOOK
            
def issue_book():
    
    cardno = input("Enter your card no :  ")
    print("List of Books....")
    mycursor.execute("select * from books")
    for i in mycursor:
        print(i)
    print("\n")
    book_name = input("Enter the name of the book :  ")
    date_of_lend = input("Enter date of lending(yyyy-mm-dd) :  ")
    date_of_return = input("Enter date of return(yyyy-mm-dd) :  ")    
    mycursor.execute("insert into lib_transaction(cardno,book_name,date_of_lend,date_of_return) values('"+cardno+"','"+book_name+"','"+date_of_lend+"','"+date_of_return+"')")
    mydb.commit()
    print("\n\nBook Issued Successfully......\n\n")
    input("\n\n\n Press any enter to continue....\n")


            
#10. TO RETURN A BOOK
            
def return_book():
    cardno = input("Enter card no:")
    date_of_return = input("Enter date of returning(yyyy-mm-dd):")
    mycursor.execute("update lib_transaction set date_of_return='"+date_of_return+"' where cardno = "+cardno+"")
    mydb.commit()
    print("\n\nBook Returned Successfully......\n\n")
    input("\n\n\n Press any enter to continue....\n")

            
#11. TO SEE LENDING HISTORY
            
def lending_history():
    mycursor.execute("select  *  from lib_transaction")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")


            
#12. TO ORDER A NEW BOOK

def order_new_book():
    orderno = input("Enter the order no :  ")
    name_of_book = input("Enter the name of the book :  ")
    del_date = input("Enter the expected delivery date of books(yyyy-mm-dd) :  ")
    price = input("Enter the price of the book :  ")
    mycursor.execute("insert into buy_new_books(orderno,name_of_book,del_date,price) values('"+orderno+"','"+name_of_book+"','"+del_date+"','"+price+"')")
    mydb.commit()
    print("\n\nNew Book Ordered Successfully......\n\n")
    input("\n\n\n Press any enter to continue....\n")


        
#13. TO UPDATE ORDER DETAILS        
        
#TO UPDATE BOOK NAME        

def update_book2_name():
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    orderno = input("Enter order no:")
    name_of_book = input("Enter new name:")
    mycursor.execute("update buy_new_books set name_of_book = '"+name_of_book+"' where orderno = '"+orderno+"'")
    mydb.commit()
    print("\n\nName has been updated.....\n\n")
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
                
#TO UPDATE DELIVERY DATE
                
def update_delivery_date():
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    orderno=str(input("Enter card no:"))
    del_date=str(input("Enter new delivery date(yyyy-mm-dd):"))
    mycursor.execute("update buy_new_books set del_date = '"+del_date+"' where orderno = '"+orderno+"'")
    mydb.commit()
    print("\n\nDelivery date has been updated......\n\n")
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
                
#TO UPDATE PRICE
                
def update_price():
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    orderno = str(input("Enter card no :  "))
    price = str(input("Enter new price :  "))
    mycursor.execute("update buy_new_books set price = '"+price+"' where orderno = '"+orderno+"'")
    mydb.commit()
    print("\n\nPrice has been updated.......\n\n")
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")
              
def update_order_details():
    while True:
        clear()
        print("1.  Update name of book")
        print("\n") 
        print("2.  Update delivery date")
        print("\n")
        print("3.  Update price")
        print("\n")
        print("4.  Exit to Main Menu")
        print("\n\n")
        choice = int(input("Enter your choice:"))

        if choice == 1:
            update_book2_name()
        if choice == 2:
            update_delivery_date()
        if choice == 3:
            update_price()
        if choice == 4:
            break


        
#14. TO DISPLAY ORDERING HISTORY

def order_history():
    mycursor.execute("select * from buy_new_books")
    for i in mycursor:
        print(i)
    input("\n\n\n Press any enter to continue....\n")

            

def main_menu():
    while True:
      clear()
      print(' L I B R A R Y    M E N U')
      print('\n1 ------>  Create a New Account')
      print('\n2 ------>  See the account info')
      print('\n3 ------>  Update Card Holder info')
      print('\n4 ------>  Delete the Account')
      print('\n5 ------>  Add New Book')
      print('\n6 ------>  Display Books')
      print('\n7 ------>  Update Book Details')
      print('\n8 ------>  Delete Book')
      print('\n9 ------>  Issue Book')
      print('\n10 ------>  Return Book')
      print('\n11 ------>  Display Lending History')
      print('\n12 ------>  Order a New Book')
      print('\n13 ------>  Update Order Details')
      print('\n14 ------>  Display Ordering History')
      print('\n15 ------>  EXIT')
      print('\n\n')
      
      choice = int(input("Enter your choice ...:  "))
      print("\n\n")

      if choice == 1:
          add_new_account()
      if choice == 2:
          display_account_info()
      if choice == 3:
          update_card_holder_info()
      if choice == 4:
          delete_account()
      if choice == 5:
          add_book()
      if choice == 6:
          display_books()
      if choice == 7:
          update_book_details()
      if choice == 8:
          delete_book()
      if choice == 9:
          issue_book()
      if choice == 10:
          return_book()
      if choice == 11:
          lending_history()
      if choice == 12:
          order_new_book()
      if choice == 13:
          update_order_details()
      if choice == 14:
          order_history()
      if choice == 15:
          break
          

if __name__ == "__main__":
    main_menu()

