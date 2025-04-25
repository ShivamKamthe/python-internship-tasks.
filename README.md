# python-internship-tasks.
# ✅ Task 1: Fibonacci Generator
A simple Python script to generate the Fibonacci series up to a specified number of terms.
def generate_fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        print(a, end=' ')
        a, b = b, a + b

if __name__ == "__main__":
    terms = int(input("Enter the number of terms: "))
    print("Fibonacci sequence:")
    generate_fibonacci(terms)

## ✅ Task 2: Voice Assistant
A basic custom voice assistant built using Python. It can respond to voice commands and perform automated tasks.
import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser

engine = pyttsx3.init()
recognizer = sr.Recognizer()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def greet():
    hour = datetime.datetime.now().hour
    if hour < 12:
        speak("Good Morning!")
    elif hour < 18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")
    speak("How can I assist you today?")

def listen():
    with sr.Microphone() as source:
        print("Listening...")
        audio = recognizer.listen(source)
    try:
        command = recognizer.recognize_google(audio)
        print(f"You said: {command}")
        return command.lower()
    except:
        speak("Sorry, I didn't catch that.")
        return ""

def run_assistant():
    greet()
    while True:
        command = listen()
        if 'time' in command:
            time = datetime.datetime.now().strftime('%I:%M %p')
            speak(f"The time is {time}")
        elif 'open youtube' in command:
            webbrowser.open("https://youtube.com")
        elif 'exit' in command:
            speak("Goodbye!")
            break

if __name__ == "__main__":
    run_assistant()
