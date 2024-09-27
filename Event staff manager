#SOURCE CODE:-

#PYTHON-MYSQL CONNECTIVITY PROJECT WORK
#IMPORTING MODULES:-
import mysql.connector
import datetime
from tabulate import tabulate

#INPUTING DETAILS OF DB FROM USER AND ESTABLISHING MYSQL CONNECTION
db=input("ENTER NAME OF DATABASE:")

mydb=mysql.connector.connect(host='localhost',user='root',passwd='rage')

mycursor = mydb.cursor()

sql="CREATE DATABASE if not exists %s" %(db,)
mycursor.execute(sql)

print("DATABASE CREATED SUCCESSFULLY..")

mycursor=mydb.cursor()

mycursor.execute("Use "+db)
TableName=input("Name of Table to be created:")

query="Create table if not exists " +TableName+" \
(EMPNO int primary key,\
NAME varchar(15) not null,\
JOB varchar(15),\
BASICSALARY int,\
HRA float,\
GROSSSALARY float,\
TAX float ,\
NETSALARY float );"

mycursor.execute(query)

print("Table"+TableName+" CREATED SUCCESSFULLY...")

#DISPLAYING MENU TO USER FOR PERFORMING VARIOUS FUNCTIONS

while True:
    print('\n')
    print("*"*120)
    print('\n')
    print("\t\t\t\tRAGE EVENT MANAGEMENTS\n")
    print("*"*120)
    print('\t\t\t\t\tMAIM MENU')
    print("*"*120)
    print('\t\t\t\t1. ADDING EMPLOYEE RECORDS')
    print('\t\t\t\t2. FOR DISPLAYING RECORD OF ALL THE EMPLOYEES')
    print('\t\t\t\t3. FOR DISPLAYING RECORD OF A PARTICULAR EMPLOYEE')
    print('\t\t\t\t4. FOR DELETING RECORDS OF ALL THE EMPLOYEES')
    print('\t\t\t\t5. FOR DELETING A RECORD OF A PARTICULAR EMPLOYEE')
    print('\t\t\t\t6. FOR MODIFICATION IN A RECORD')
    print('\t\t\t\t7. FOR DISPLAYING PAYROLL')
    print('\t\t\t\t8. FOR DISPLAYING SALARY SLIP OF ALL THE EMPLOYEES')
    print('\t\t\t\t9. FOR DISPLAYING SALARY SLIP OF A PARTICULAR EMPLOYEE')
    print('\t\t\t\t10.FOR EXIT')
    print('ENTER CHOICE...',end='')

#INPUTING CHOICE FROM USER
    
    choice=int(input())

#1.FOR ADDING EMPLOYEE RECORDS:
    
    if choice==1:
        try:
            print('ENTER EMPLOYEE INFORMATION')
            mempno=int(input('ENTER EMPLOYEE NO:'))
            mname=input('ENTER EMPLOYEE NAME :')
            mjob=input('ENTER EMPLOYEE JOB(POSITION),IN CAPITALS:')
            mbasic=int(input('ENTER BASIC SALARY:'))
            if mjob.upper()=='HOD':
                mhra=mbasic*0.30
                mtax=mbasic*0.2
            elif mjob.upper()=='MANAGER':
                mhra=mbasic*0.25
                mtax=mbasic*0.15
            else:
                mhra=mbasic*0.15
                mtax=mbasic*0.10
            mgross=mbasic+mhra
            mnet=mgross-mtax
            rec =(mempno,mname,mjob,mbasic,mhra,mgross,mtax,mnet)
            query = "insert into " + TableName + "(EMPNO,NAME,JOB,BASICSALARY,HRA,GROSSSALARY,TAX,NETSALARY) values (%s,%s,%s,%s,%s,%s,%s,%s)"
            mycursor.execute(query,rec)

            mydb.commit()
            print('RECORD ADDED SUCCESFULLY ')
        except Exception as e :
            print('SOMETHING WENT WRONG ',e)

#2.FOR DISPLAYING RECORD OF ALL EMPLOYEES:
            
    elif choice==2:
        try:
            query ='select * from ' +TableName
            mycursor.execute(query)
            #print(query)
            print(tabulate(mycursor, headers=['EMPNO','NAME','JOB','BASIC SALARY','HRA','GROSS SALARY','TAX','NETSALARY'],tablefmt='fancy_grid'))
            '''myrecords=mycursor.fetchall()
            for rec in myrecords:
                print(rec)'''

        except:
            print('SOMETHING WENT WRONG')

#3.FOR DISPLAYING RECORD OF A PARTICULAR EMPLOYEE:
    elif choice==3:
        try:
            en=input('Enter employee no. of the record to be displayed...')
            query="select * from " +TableName+" where empno="+en
            mycursor.execute(query)
            myrecord=mycursor.fetchone()
            print("\n\nRecord of Employee No.:"+en)
            print(myrecord)
            c=mycursor.rowcount
            if c==-1:
                print("Nothing to display")

        except:
            print('something went wrong')

#4.FOR DELETING RECORDS OF ALL EMPLOYEES:

    elif choice==4:
        try:
            ch=input('do you want to delete all the records (y/n)')
            if ch.upper()=='Y':
                mycursor.execute('delete from '+TableName)
                mydb.commit()
                print('ALL THE RECORDS ARE DELETED')
        except:
            print('SOMETHING WENT WRONG')


#5.FOR DELETING RECORD OF A PARTICULAR EMPLOYEE:     

    elif choice==5:
        try:
            en=input('Enter employee no. of the record to be deleted...')
            query='delete from '+TableName+' where empno='+en
            mycursor.execute(query)
            mydb.commit()
            c-mycursor.rowcount
            if c>0:
                print('Deletion done')
            else:
                print ('Employee no ',en,'not found')
        except:
            print('SOMETHING WENT WRONG')

#6.FOR MODIFICATION IN RECORD OF AN EMPLOYEE:
            
    elif choice==6:
        try:
            en=input('Enter employee no. of the record to be modified...')
            query='select * from '+TableName+' where empno=' +en
            mycursor.execute(query)
            myrecord=mycursor.fetchone()
            c=mycursor.rowcount
            if c==-1:
                print('Empno '+en+' does not exist')
            else:
                mname=myrecord[1]
                mjob=myrecord[2]
                mbasic=myrecord[3]
                print('empno :',myrecord[0])
                print('name:',myrecord[1])
                print('job :',myrecord[2])
                print('basic :',myrecord[3])
                print('hra :',myrecord[4])
                print('gross :',myrecord[5])
                print('tax :',myrecord[6])
                print('net :',myrecord[7])
                print('--------------------')
                print('type value to modify below or just press ENTER for no change')
                x=input('enter name')
                if len(x)>0:
                    mname=x
                x=input('enter job')
                if len(x)>0:
                    mjob=x
                x=input('enter basic salary')
                if len(x)>0:
                    mbasic=float(x)
                query='update '+TableName+' set name='+"'"+mname+"'"+','+'job='+"'"+mjob+"'"+','+'basicsalary='\
                       +str(mbasic)+' where empno='+en
                mycursor.execute(query)
                mydb.commit()
                print('RECORD MODIFIED')
        except:
            print('SOMETHING WENT WRONG')

#7.FOR DISPLAYING PAYROLL:               
                
    elif choice==7:
           try:
               query='select * from '+TableName
               mycursor.execute(query)
               myrecords=mycursor.fetchall()
               print("\n\n\n")
               print('*'*100)
               print('Employee Payroll'.center(95))
               print('*'*100)
               now =datetime.datetime.now()
               print("Current Date and Time:", end='')
               print(now.strftime("%Y-%m-%d %H:%M:%S"))
               print()
               print('*'*100)
               print('%-5s %-15s %-10s %-8s %-8s %-9s %-8s %-9s' %
                     ('Empno','Name','Job','Basic','Hra','Gross','Tax','Net'))
               print('*'*100)
               for rec in myrecords:
                   print('%-5d %-15s %-10s %-8.2f %-8.2f %-9.2f %-8.2f %-9.2f ' % rec)
               print('*'*100)
           except Exception as e:
                ('SOMETHING WENT WRONG',e)

#8.FOR DISPLAYING SALARY SLIP OF ALL EMPLOYEES:                
                  
    elif choice==8:
        try:
            query= 'select * from '+TableName
            mycursor.execute(query)
            now = datetime.datetime.now()
            print("\n\n\n")
            print("-"*100)
            print("SALARY SLIP".center(96))
            print("-"*100)
            print('THUGLIFE COORP'.center(95))
            print('-'*100)
            print("Current Date and Time:", end='')
            print(now.strftime("%Y-%m-%d %H:%M:%S"))
            print('-'*100)
            myrecords=mycursor.fetchall()
            for rec in myrecords:
                print('%-5s %-15s %-10s %-8.2f %-8.2f %-9.2f %-8.2f %-9.2f '%rec)
            print('-'*100)    
        except Exception as e:
            print('SOMETHING WENT WRONG',e)

#9.FOR DISPLAYING SALARY SLIP OF A PARTICULAR EMPLOYEE:

    elif choice==9:
        try:
            en=input("Enter employee number whose pay slip you want to retreive:")
            query='select * from '+TableName+' where empno='+en
            mycursor.execute(query)
            now = datetime.datetime.now()
            print("-"*100)
            print("THUGLIFE CO-ORP.".center(95))
            print("-"*100)
            print('SALARY SLIP'.center(97))
            print('-'*100)
            print("Current Date and Time:", end=' ')
            print(now.strftime("%Y-%m-%d %H:%M:%S"))
            print('-'*100)
            #print(query)
            print(tabulate(mycursor, headers=['EMPNO','NAME','JOB','BASIC SALARY','HRA','GROSS SALARY','TAX','NETSALARY'],tablefmt='fancy_grid'))

        except Exception as e:
            print('SOMETHING WENT WRONG',e)

#INPUTING IF USER WANT TO EXIT:
            
    elif choice==10:

        break
    else:
        print('WRONG CHOICE...')