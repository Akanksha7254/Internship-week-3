# Internship-week-3
# Creating a Weather Web Application
 📌 In this project, I developed a Weather App in Python that can fetch real-time weather data based on user input, such as a city name.
 
  🧐 Here's a quick breakdown of the code:
- Use a weather API (e.g., OpenWeatherMap, Weatherstack) to fetch real-time weather data.
- Display relevant weather information, including temperature, humidity, weather conditions, and more.
- Implement graceful error handling for scenarios like incorrect location input or network issues.
- Ensure that the user interface is user-friendly and provides clear instructions for a pleasant user experience.


In this project, we will be building a weather application. This application will show the temperature of a location. To fetch weather information we will need an API. An API(Application Programming Interface) is a function that allows applications to interact and share data using various components and microservices. For this project, we will be using Open weather API  for fetching weather data


#  Modules Required.

   pip install geopy :  
      geopy is a Python client for several popular geocoding web services.geopy makes it easy for Python developers to locate the coordinates of addresses, cities, countries, and landmarks across the globe using third-party geocoders and other data sources.

      
   pip install timezonefinder:
     This is a python package for looking up the corresponding timezone for given coordinates on earth entirely offline

     
   pip install pytz:
    pytz brings the Olson tz database into Python. This library allows accurate and cross platform timezone calculations using Python 2.4 or higher. It also solves the issue of ambiguous times at the end of daylight saving time, which you can read more about in the Python Library Reference (datetime.tzinfo). Almost all of the Olson timezones are supported.

# Importing required modules

    from tkinter import *
    import tkinter as tk
    from  geopy.geocoders import Nominatim
    from tkinter import ttk,messagebox
    from timezonefinder import TimezoneFinder
    from datetime import datetime
    import requests
    import pytz
# staring of main window.
    root=Tk()
    root.title("Weather App")
    root.geometry("900x500+300+200")
    root.resizable(False,False)

# creating function .

    def getWeather():
        try:
             city=textfield.get()               # textfield to enter the name of the city for which current weather is calculated

             geolocator=Nominatim(user_agent="geoapiExcercises")           # to mark the lattitude and longitude of a laocation
             location= geolocator. geocode(city)
             obj = TimezoneFinder()                                         # Time zone finder
             result = obj. timezone_at(lng=location.longitude,lat=location.latitude)

             home=pytz.timezone(result)                       # accessing local date and time
             local_time=datetime.now(home)
             current_time=local_time.strftime("%I : %M %p")
             clock.config(text=current_time)
             name.config(text="CURRENT WEATHER")


#Using Weather API.

             api="https://api.openweathermap.org/data/2.5/weather?q=" + city + "&appid=2297b0c4773a552e284c4ed946e2116d"
             json_data = requests.get(api).json()
             condition = json_data["weather"][0]['main']   # accessing the required weather parameters to be displayed.
             description = json_data['weather'][0]['description']
             temp = int(json_data['main']['temp']-273.15)
             pressure = json_data['main']['pressure']
             humidity = json_data['main']['humidity']
             wind = json_data['wind']['speed']

             t.config(text=(temp,"°"))
             c.config(text=(condition,"|","FEELS","LIKE",temp,"°"))

             w.config(text=wind)
             h.config(text=humidity)
             d.config(text=description)
             p.config(text=pressure)             
        except Exception as  e:             #Exception raised
             messagebox.showerror("Weather App","Invalid Entry !!!!")


#Adding Widgets to the Web Application

    Search_image=PhotoImage(file="Copy of search.png")    #adding search image
    myimage=Label(image=Search_image)
    myimage.place(x=20,y=20)

    textfield=tk.Entry(root,justify="center",width=17,font=("poppins ",25,"bold"),bg="#404040", border=0 ,fg="white") # adding text field to enter name of the location
    textfield.place(x=50,y=40)
    textfield.focus()

    Search_icon=PhotoImage(file="Copy of search_icon.png")        # adding search icon
    myimage_icon=  Button(image=Search_icon,borderwidth=0,cursor="hand2",bg="#404040",command=getWeather)
    myimage_icon.place(x=400,y=34)

    Logo_image=PhotoImage(file="Copy of logo.png")  # adding logo
    logo=Label(image=Logo_image)
    logo.place(x=150,y=100)

    Frame_image=PhotoImage(file="Copy of Copy of box.png")
    frame_myimage=Label(image=Frame_image)
    frame_myimage.pack(padx=5,pady=5,side=BOTTOM)

    name=Label(root,font=("arial",15,"bold"))    # to display location name and time
    name.place(x=30,y=100)
    clock=Label(root,font=("Helvetica",20))
    clock.place(x=30,y=130)

    label1=Label(root,text="WIND",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef") #displaying required parameters
    label1.place(x=120,y=400)

    label2=Label(root,text="HUMIDITY",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label2.place(x=225,y=400)

    label3=Label(root,text="DESCRIPTION",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label3.place(x=430,y=400)

    label4=Label(root,text="PRESSURE",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label4.place(x=650,y=400)

    t=Label(font=("arial",70,"bold"),fg="#ee666d")
    t.place(x=400,y=150)
    c=Label(font=("arial",15,"bold"))
    c.place(x=400,y=250)

    w=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")    #Placing the Widgets in the application
    w.place(x=120,y=430) 
    h=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    h.place(x=240,y=430)
    d=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    d.place(x=450,y=430)
    p=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    p.place(x=670,y=430)

# ending the mainloop

    root.mainloop()


# CODE
    from tkinter import *
    import tkinter as tk
    from  geopy.geocoders import Nominatim
    from tkinter import ttk,messagebox
    from timezonefinder import TimezoneFinder
    from datetime import datetime
    import requests
    import pytz

    root=Tk()
    root.title("Weather App")
    root.geometry("900x500+300+200")
    root.resizable(False,False)


    def getWeather():
        try:
             city=textfield.get()

             geolocator=Nominatim(user_agent="geoapiExcercises")
             location= geolocator. geocode(city)
             obj = TimezoneFinder()
             result = obj. timezone_at(lng=location.longitude,lat=location.latitude)

             home=pytz.timezone(result)
             local_time=datetime.now(home)
             current_time=local_time.strftime("%I : %M %p")
             clock.config(text=current_time)
             name.config(text="CURRENT WEATHER")

  
             api="https://api.openweathermap.org/data/2.5/weather?q=" + city + "&appid=2297b0c4773a552e284c4ed946e2116d"
             json_data = requests.get(api).json()
             condition = json_data["weather"][0]['main']
             description = json_data['weather'][0]['description']
             temp = int(json_data['main']['temp']-273.15)
             pressure = json_data['main']['pressure']
             humidity = json_data['main']['humidity']
             wind = json_data['wind']['speed']

             t.config(text=(temp,"°"))
             c.config(text=(condition,"|","FEELS","LIKE",temp,"°"))

             w.config(text=wind)
             h.config(text=humidity)
             d.config(text=description)
             p.config(text=pressure)
        except Exception as  e:
             messagebox.showerror("Weather App","Invalid Entry !!!!")



    Search_image=PhotoImage(file="Copy of search.png")
    myimage=Label(image=Search_image)
    myimage.place(x=20,y=20)

    textfield=tk.Entry(root,justify="center",width=17,font=("poppins ",25,"bold"),bg="#404040", border=0 ,fg="white")
    textfield.place(x=50,y=40)
    textfield.focus()

    Search_icon=PhotoImage(file="Copy of search_icon.png")
    myimage_icon=  Button(image=Search_icon,borderwidth=0,cursor="hand2",bg="#404040",command=getWeather)
    myimage_icon.place(x=400,y=34)

    Logo_image=PhotoImage(file="Copy of logo.png")
    logo=Label(image=Logo_image)
    logo.place(x=150,y=100)

    Frame_image=PhotoImage(file="Copy of Copy of box.png")
    frame_myimage=Label(image=Frame_image)
    frame_myimage.pack(padx=5,pady=5,side=BOTTOM)

    name=Label(root,font=("arial",15,"bold"))
    name.place(x=30,y=100)
    clock=Label(root,font=("Helvetica",20))
    clock.place(x=30,y=130)

    label1=Label(root,text="WIND",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label1.place(x=120,y=400)

    label2=Label(root,text="HUMIDITY",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label2.place(x=225,y=400)

    label3=Label(root,text="DESCRIPTION",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label3.place(x=430,y=400)

    label4=Label(root,text="PRESSURE",font=("Helvetica",15,"bold"),fg="White",bg="#1ab5ef")
    label4.place(x=650,y=400)

    t=Label(font=("arial",70,"bold"),fg="#ee666d")
    t.place(x=400,y=150)
    c=Label(font=("arial",15,"bold"))
    c.place(x=400,y=250)

    w=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    w.place(x=120,y=430)
    h=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    h.place(x=240,y=430)
    d=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    d.place(x=450,y=430)
    p=Label(text="....",font=("arial",20,"bold"),bg="#1ab5ef")
    p.place(x=670,y=430)
  
root.mainloop()

# Output.
![image](https://github.com/Akanksha7254/Internship-week-3/assets/146561059/711cbb31-434a-4bb2-b609-7606398a0e87)

![image](https://github.com/Akanksha7254/Internship-week-3/assets/146561059/8f0b314c-6c67-4493-b1c0-8d9e5cb9b8ff)
![image](https://github.com/Akanksha7254/Internship-week-3/assets/146561059/50ca1f74-fd40-4b03-8c37-6ec44dc892f5)
![image](https://github.com/Akanksha7254/Internship-week-3/assets/146561059/1ca52c44-8feb-4828-afa4-d79f749b6eb5)
![image](https://github.com/Akanksha7254/Internship-week-3/assets/146561059/6b0f298b-5b58-4553-b2de-13da9eef549b)





