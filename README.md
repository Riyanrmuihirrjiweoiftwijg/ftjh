#importing mysql connector
import mysql.connector
mydb=mysql.connector.connect(host='localhost', user='root', passwd='1234')

#checking if the connection is present
if mydb.is_connected():
    print("---Connection is Established---")
else:
    print("---Connection was not Established---")


#cursor object
cur=mydb.cursor()

#creating the database
cur.execute("create database Stock")

#using the database            
cur.execute("use Stock")

#creating the food table
cur.execute("create table food(FSLNo int primary key, Product_name varchar(20), Manufacturer varchar(20), Unit_price int)")

#creating the stationery table
cur.execute("create table stationery(SSLNo int primary key, Product_name varchar(20), Manufacturer varchar(20), Unit_price int)")

#creating the grocery table
cur.execute("create table grocery(GSLNo int primary key, Product_name varchar(20), Region varchar(20), Unit_price int)")


#Loop Variables
yn="Y"
role="MANAGER"


while yn=="Y":
        print("-"*10,"YOU ARE PLAYING AS A MANAGER","-"*10)
        print('''You can
1. ADD an item to a table
2. REMOVE an item from a table
3. EDIT an item from a table
4. SEE the stock''')
        ch=int(input("What Would You Like To Do?: "))
        if ch>4:
            print("#"*50)
            print("#"*20,"WRONG INPUT! TRY AGAIN","#"*20)
            print("#"*50)
            continue

        
#ADD ITEM
        if ch==1:
            print("-"*50)
            print('''Which Table would you like to the add the item to?
1. Food Table
2. Stationery Table
3. Grocery Table''')
            tabselect=int(input("Select from 1/2/3:"))
            print("-"*50)
            

#Adding item to 1st table
            if tabselect==1:
                print("-"*7,"YOU ARE NOW EDITING THE FOOD TABLE","-"*7)
                print("-"*50)
                entries=int(input("How many items would you like to add?: "))
                i=0
                while i<entries:
                    slno=int(input("Enter the S.L. Number of the product: "))
                    name=input("Enter the name of the product you would like to add: ")
                    man=input("Enter the Manufacturer of the product: ")
                    price=int(input("Enter the Unit price of the product: "))
                    incom=("insert into food(fslno,product_name,manufacturer,unit_price)values(%s,%s,%s,%s)")
                    insert=(slno,name,man,price)
                    cur.execute(incom,insert)
                    mydb.commit()
                    print("-"*10,"ITEM HAS BEEN ADDED!","-"*10)
                    entries=entries-1
                print("-"*50)    
                print("-"*9,"ALL THE ITEMS HAVE BEEN ADDED!","-"*9)
                print("-"*50)

                
#Adding item to 2nd table
            if tabselect==2:
                print("-"*7,"YOU ARE NOW EDITING THE STATIONERY TABLE","-"*7)
                print("-"*50)
                entries=int(input("How many items would you like to add?: "))
                i=0
                while i<entries:
                    slno=int(input("Enter the S.L. Number of the product: "))
                    name=input("Enter the name of the product you would like to add: ")
                    man=input("Enter the Manufacturer of the product: ")
                    price=int(input("Enter the Unit price of the product: "))
                    incom=("insert into stationery(sslno,product_name,manufacturer,unit_price)values(%s,%s,%s,%s)")  
                    insert=(slno,name,man,price)
                    cur.execute(incom,insert)
                    mydb.commit()
                    print("-"*10,"ITEM HAS BEEN ADDED!","-"*10)
                    entries=entries-1
                print("-"*50)
                print("-"*9,"ALL THE ITEMS HAVE BEEN ADDED!","-"*9)
                print("-"*50)

    
#Adding item to 3rd table
            if tabselect==3:
                print("-"*7,"YOU ARE NOW EDITING THE GROCERY TABLE","-"*7)
                print("-"*50)
                entries=int(input("How many items would you like to add?: "))
                i=0
                while i<entries:
                    slno=int(input("Enter the S.L. Number of the product: "))
                    name=input("Enter the name of the product you would like to add: ")
                    region=input("Enter the place from where it has ben imported from: ")
                    price=int(input("Enter the Unit price of the product: "))
                    incom=("insert into grocery(gslno,product_name,region,unit_price)values(%s,%s,%s,%s)") 
                    insert=(slno,name,region,price)
                    cur.execute(incom,insert)
                    mydb.commit()
                    print("-"*10,"ITEM HAS BEEN ADDED!","-"*10)
                    entries=entries-1
                print("-"*50)
                print("-"*9,"ALL THE ITEMS HAVE BEEN ADDED!","-"*9)
                print("-"*50)

            yn=input("Would you like to continue? Y/N: ")
            if yn=="N":
                print("-"*10,"#"*10,"*"*10,"THANK YOU SO MUCH FOR TESTING THIS SERVICE!","*"*10,"#"*10,"-"*10)
            else:
                continue


#REMOVE ITEM            
        if ch==2:
            print("-"*50)
            print('''Which Table would you like to remove the item from?
1. Food Table
2. Stationery Table
3. Grocery Table''')
            tabselect=int(input("Select from 1/2/3:"))
            print("-"*50)


#Remove item from 1st table
            if tabselect==1:
                print("-"*7,"YOU ARE NOW EDITING THE FOOD TABLE","-"*7)
                print("-"*50)
                print('''On the basis of what would you like to remove an item by
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                bitem=int(input("Enter your choice from 1/2/3/4: "))
                if bitem==1:
                    no=input("Enter the SLNo. you'd like to delete: ")
                    rem="delete from food where FSLNo=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==2:
                    no=input("Enter the Product_name of the product you'd like to delete: ")
                    rem="delete from food where product_name=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==3:
                    no=input("Enter the Manufacturer of the product you'd like to delete: ")
                    rem="delete from food where manufacturer=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==4:
                    no=input("Enter the Unit_Price of the product you'd like to delete: ")
                    rem="delete from food where unit_price=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)


#Remove item from 2nd table
            if tabselect==2:
                print("-"*7,"YOU ARE NOW EDITING THE STATIONERY TABLE","-"*7)
                print("-"*50)
                print('''On the basis of what would you like to remove an item by
1. SSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                bitem=int(input("Enter your choice from 1/2/3/4: "))
                if bitem==1:
                    no=input("Enter the SLNo. you'd like to delete: ")
                    rem="delete from stationery where SSLNo=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==2:
                    no=input("Enter the Product_name of the product you'd like to delete: ")
                    rem="delete from stationery where product_name=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==3:
                    no=input("Enter the Manufacturer of the product you'd like to delete: ")
                    rem="delete from stationery where manufacturer=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==4:
                    no=input("Enter the Unit_Price of the product you'd like to delete: ")
                    rem="delete from stationery where unit_price=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)


#Remove item from 3rd table                    
            if tabselect==3:
                print("-"*7,"YOU ARE NOW EDITING THE GROCERY TABLE","-"*7)
                print("-"*50)
                print('''On the basis of what would you like to remove an item by
1. GSLNo
2. Product_name
3. Region
4. Unit_price''')
                bitem=int(input("Enter your choice from 1/2/3/4: "))
                if bitem==1:
                    no=input("Enter the SLNo. you'd like to delete: ")
                    rem="delete from grocery where GSLNo=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==2:
                    no=input("Enter the Product_name of the product you'd like to delete: ")
                    rem="delete from grocery where product_name=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==3:
                    no=input("Enter the Region of the product you'd like to delete: ")
                    rem="delete from grocery where Region=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
                if bitem==4:
                    no=input("Enter the Unit_Price of the product you'd like to delete: ")
                    rem="delete from grocery where unit_price=%s"
                    dele=(no,)
                    cur.execute(rem,dele)
                    mydb.commit()
                    print("-"*50)
                    print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN DELETED!","-"*10)
                    print("-"*50)
                    
            yn=input("Would you like to continue? Y/N: ")     
            if yn=="N":
                print("-"*10,"#"*10,"*"*10,"THANK YOU SO MUCH FOR TESTING THIS SERVICE!","*"*10,"#"*10,"-"*10)
            else:
                continue


#EDIT ITEM
        if ch==3:
            print("-"*50)
            print('''Which Table would you like to Edit?
1. Food Table
2. Stationery Table
3. Grocery Table''')
            tabselect=int(input("Select from 1/2/3:"))
            print("-"*50)


#Edit for 1st table
            if tabselect==1:
                print("-"*7,"YOU ARE NOW EDITING THE FOOD TABLE","-"*7)
                print("-"*50)
                print('''Which column would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                eitem=int(input("Enter your choice from 1/2/3/4: "))
                editedv=input("Enter the edited value: ")

                if eitem==1:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update food set FSLNo=%s where FSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update food set FSLNo=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update food set FSLNo=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update food set FSLNo=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==2:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update food set Product_name=%s where FSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update food set Product_name=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update food set Product_name=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update food set Product_name=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==3:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update food set Manufacturer=%s where FSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update food set Manufacturer=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update food set Manufacturer=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update food set Manufacturer=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==4:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update food set Unit_price=%s where FSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update food set Unit_price=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update food set Unit_price=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update food set Unit_price=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)


#Edit for 2nd Table
            if tabselect==2:
                print("-"*7,"YOU ARE NOW EDITING THE STATIONERY TABLE","-"*7)
                print("-"*50)
                print('''Which column would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                eitem=int(input("Enter your choice from 1/2/3/4: "))
                editedv=input("Enter the edited value: ")

                if eitem==1:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update stationery set SSLNo=%s where SSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update stationery set SSLNo=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update stationery set SSLNo=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update stationery set SSLNo=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==2:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update stationery set Product_name=%s where SSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update stationery set Product_name=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update stationery set Product_name=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update stationery set Product_name=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==3:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update stationery set Manufacturer=%s where SSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update stationery set Manufacturer=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update stationery set Manufacturer=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update stationery set Manufacturer=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==4:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update stationery set Unit_price=%s where SSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update stationery set Unit_price=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update stationery set Unit_price=%s where Manufacturer=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update stationery set Unit_price=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)


#Edit for 3rd table
            if tabselect==3:
                print("-"*7,"YOU ARE NOW EDITING THE STATIONERY TABLE","-"*7)
                print("-"*50)
                print('''Which column would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                eitem=int(input("Enter your choice from 1/2/3/4: "))
                editedv=input("Enter the edited value: ")

                if eitem==1:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update grocery set GSLNo=%s where GSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update grocery set SSLNo=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update grocery set SSLNo=%s where Region=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update grocery set SSLNo=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==2:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update grocery set Product_name=%s where GSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update grocery set Product_name=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update grocery set Product_name=%s where Region=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update grocery set Product_name=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==3:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update grocery set Region=%s where GSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update grocery set Region=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update grocery set Region=%s where Region=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update grocery set Region=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                if eitem==4:
                    print("-"*50)
                    print('''On the basis of which condition would you like to edit
1. FSLNo
2. Product_name
3. Manufacturer
4. Unit_price''')
                    ebitem=int(input("Enter your selection from 1/2/3/4: "))
                    value=input("Enter the corresponding value of the condition: ")

                    if ebitem==1:
                        edit="update grocery set Unit_price=%s where GSLNo=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==2:
                        edit="update grocery set Unit_price=%s where product_name=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==3:
                        edit="update grocery set Unit_price=%s where Region=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)

                    if ebitem==4:
                        edit="update grocery set Unit_price=%s where Unit_price=%s"
                        editv=(editedv, value)
                        cur.execute(edit,editv)
                        mydb.commit()
                        print("-"*50)
                        print("-"*10,cur.rowcount, "ITEM(S) HAS BEEN EDITED!","-"*10)
                        print("-"*50)
                        
            yn=input("Would you like to continue? Y/N: ")
            if yn=="N":
                print("-"*10,"#"*10,"*"*10,"THANK YOU SO MUCH FOR TESTING THIS SERVICE!","*"*10,"#"*10,"-"*10)
            else:
                continue


#SEE THE STOCK
        if ch==4:
            print("-"*50)
            print('''Which Table would you like to See?
1. Food Table
2. Stationery Table
3. Grocery Table''')
            tabselect=int(input("Select from 1/2/3:"))
            print("-"*50)


#Seeing the stock of FOOD 
            if tabselect==1:
                cur.execute("select * from food")
                food=cur.fetchall()
                print("#"*10,"-"*10,"THE FOOD STOCK TABLE","-"*10,"#"*10)
                print("FSLNo, Product_name, Manufacturer, Unit_Price")
                for i in food:
                    print(i)
                print()


#Seeing the stock of STATIONERY 
            if tabselect==2:
                cur.execute("select * from stationery")
                stationery=cur.fetchall()
                print("#"*10,"-"*10,"THE STATIONERY STOCK TABLE","-"*10,"#"*10)
                print("SSLNo, Product_name, Manufacturer, Unit_Price")
                for i in stationery:
                    print(i)
                print()


#Seeing the stock of Grocery
            if tabselect==3:
                cur.execute("select * from grocery")
                grocery=cur.fetchall()            
                print("#"*10,"-"*10,"THE GROCERY STOCK TABLE","-"*10,"#"*10)
                print("GSLNo, Product_name, Region, Unit_Price")
                for i in grocery:
                    print(i)
                print()

        yn=input("Would you like to continue? Y/N: ")
        if yn=="N":
            print("-"*10,"#"*10,"*"*10,"THANK YOU SO MUCH FOR TESTING THIS SERVICE!","*"*10,"#"*10,"-"*10)
        else:
            continue
# ftjh
