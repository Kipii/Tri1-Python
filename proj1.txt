import os
from datetime import datetime
import socket
import shutil
from netmiko import ConnectHandler
import requests

net_connect = ConnectHandler(
    device_type="linux",
    host="127.0.0.1",
    username="usr",
    password="pass",
)

def main():
    print("\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n Welcome to 2012957's Python Program")
    menu()


def menu():

    print("\n\nPlease make your choice!")
#options to choose from, for which we used an input function.
    choice = input("""
                      1: Show the local time and date
                      2: Show the local IP address
                      3: Show Remote home directory listing
                      4: Backup remote file
                      5: Save web page 
                      R: Restart
                      Q: Quit

                      \r\n Please enter your choice: """)

    if choice == "1":

        now = datetime.now() #uses the import datetime
        print("\n\n\n\n\n\nToday's date and time is : ", )
        dt_string = now.strftime("%d/%m/%Y %H:%M:%S") #date and time format
        print(dt_string)

        menu() #requests menu


    elif choice == "2":
        hostname = socket.gethostname()
        ipaddr = socket.gethostbyname(hostname)
        print("\n\n\n\n\n\nYour Computer IP Address is: " + ipaddr)
        menu()


    elif choice == "3":
        print("\n\n\n\n\n\nYour home directory is " +os.path.expanduser('~')+ " ,and it contains\n the following files:\n") #os.path.expanduser shows the main directory of the OS
        path = "C:/Users/Vpetr/"
        dirlist = os.listdir(path)
        print(dirlist)
        menu()

    elif choice == "4":
        print("\n\n\n\n\n\nYour backup file is now created! Check newcopy.bak :) ")
        shutil.copy(__file__, "newcopy.bak") #copies / # duplicates the file
        menu()

    elif choice == "5":
        print("\n\n\n\n\n\n\nYour html page is now downloaded! Please check softwaregatest.html This is a http website. ")

        url = 'http://www.softwareqatest.com/'
        r = requests.get(url, allow_redirects=True) #requests the url and rewrites it into a .html document
        open('softwaregatest.html', 'wb').write(r.content) 

        menu()

    elif choice == "r" or choice == "R": #requests the main() to restart the code entirely
        main()

    elif choice == "Q" or choice == "q": #quits the terminal
        exit()
    else:
        print("\n\n\n\n\n\nYou must only select from 1 to 5 or select Q to exit")
        print("\nPlease try again")
        menu()

main()
