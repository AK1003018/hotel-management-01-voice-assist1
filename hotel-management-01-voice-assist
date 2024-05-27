import sqlite3
import datetime
import random
import pyttsx3

# (SQLite connection)
conn = sqlite3.connect('hotel.db')
cursor = conn.cursor()

# (Create tables if they don't exist)
cursor.execute('''
    CREATE TABLE IF NOT EXISTS bookings (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT,
        phone TEXT,
        address TEXT,
        checkin TEXT,
        checkout TEXT,
        room_type TEXT,
        price_per_day INTEGER,
        restaurant_charges INTEGER,
        payment_status INTEGER
    )
''')

conn.commit()

# (pyttsx3)
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if 0 <= hour < 12:
        speak("Good Morning!")
    elif 12 <= hour < 18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")

    print("\t\t\t\t\t\t ** WELCOME TO HOTEL CASANOVA **\n")
    speak("Welcome to Hotel Casanova!")

    speak("You can book your room by following the below procedure..")


# (Global Variable Declaration)
i = 0


# (Home)
def Home():
    print("\t\t\t >> Main Menu <<\n")
    print("\t\t\t 1 Booking\n")
    print("\t\t\t 2 Rooms Info\n")
    print("\t\t\t 3 Room Service(Menu Card)\n")
    print("\t\t\t 4 Payment\n")
    print("\t\t\t 5 Record\n")
    print("\t\t\t 0 Exit\n")

    ch = int(input("-> "))

    if ch == 1:
        print(" ")
        Booking()

    elif ch == 2:
        print(" ")
        Rooms_Info()

    elif ch == 3:
        print(" ")
        restaurant()

    elif ch == 4:
        print(" ")
        Payment()

    elif ch == 5:
        print(" ")
        Record()

    else:
        speak("Session ended successfully!")
        exit()


# (Booking)
def Booking():
    global i
    print(" BOOKING ROOMS")
    print(" ")

    while True:
        name = input("Name: ")
        phone = input("Phone No.: ")
        address = input("Address: ")

        checkin = input("Check-In (YYYY-MM-DD): ")
        checkout = input("Check-Out (YYYY-MM-DD): ")

        room_type = input("Room Type: ")

        price_per_day = 0  # Initialize price_per_day variable

        # (Assign price_per_day based on room_type)
        if room_type == 'Standard Non-AC':
            price_per_day = 3500
        elif room_type == 'Standard AC':
            price_per_day = 4000
        elif room_type == '3-Bed Non-AC':
            price_per_day = 4500
        elif room_type == '3-Bed AC':
            price_per_day = 5000

        # (Insert booking details into the database)
        cursor.execute('''
            INSERT INTO bookings (name, phone, address, checkin, checkout, room_type, price_per_day, restaurant_charges, payment_status)
            VALUES (?, ?, ?, ?, ?, ?, ?, 0, 0)
        ''', (name, phone, address, checkin, checkout, room_type, price_per_day))
        conn.commit()

        print("\t\t\t*** ROOM BOOKED SUCCESSFULLY ***\n")
        speak("\t\t\t*** ROOM BOOKED SUCCESSFULLY ***\n")
        speak("Please complete further requirements")

        i += 1

        choice = input("Do you want to make another booking? (yes/no): ")
        if choice.lower() != 'yes':
            break

    Home()


# (ROOMS INFO)
def Rooms_Info():
    print("		 ------ HOTEL ROOMS INFO ------")
    print("")
    print("STANDARD NON-AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed, Television, Telephone,")
    print("Double-Door Cupboard, 1 Coffee table with 2 sofa, Balcony and")
    print("an attached washroom with hot/cold water.\n")
    print("STANDARD NON-AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed, Television, Telephone,")
    print("Double-Door Cupboard, 1 Coffee table with 2 sofa, Balcony and")
    print("an attached washroom with hot/cold water + Window/Split AC.\n")
    print("3-Bed NON-AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed + 1 Single Bed, Television,")
    print("Telephone, a Triple-Door Cupboard, 1 Coffee table with 2 sofa, 1")
    print("Side table, Balcony with an Accent table with 2 Chair and an")
    print("attached washroom with hot/cold water.\n")
    print("3-Bed AC")
    print("---------------------------------------------------------------")
    print("Room amenities include: 1 Double Bed + 1 Single Bed, Television,")
    print("Telephone, a Triple-Door Cupboard, 1 Coffee table with 2 sofa, ")
    print("1 Side table, Balcony with an Accent table with 2 Chair and an")
    print("attached washroom with hot/cold water + Window/Split AC.\n\n")

    input("Press Enter to go back to the Main Menu")
    Home()


# (RESTAURANT FUNCTION)
def restaurant():
    print(" Restaurant functionality is not implemented yet.")

    input("Press Enter to go back to the Main Menu")
    Home()


# (PAYMENT)
def Payment():
    print(" Payment functionality is not implemented yet.")

    input("Press Enter to go back to the Main Menu")
    Home()


# (RECORD)
def Record():
    cursor.execute('SELECT * FROM bookings')
    bookings = cursor.fetchall()

    print("	 *** HOTEL RECORD ***\n")
    print("| Name	 | Phone No. | Address	 | Check-In | Check-Out	 | Room Type	 | Price/day	 |")
    print(
        "----------------------------------------------------------------------------------------------------------------------")

    for booking in bookings:
        print("|", booking[1], "\t |", booking[2], "\t|", booking[3], "\t|", booking[4], "\t|", booking[5], "\t|",
              booking[6], "\t|", booking[7])

    print(
        "----------------------------------------------------------------------------------------------------------------------")

    input("Press Enter to go back to the Main Menu")
    Home()


# (Driver Code)
wishMe()
Home()

