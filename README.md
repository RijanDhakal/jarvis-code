import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import wikipedia

# setting male voice [0] / for female [1]
engine = pyttsx3.init('sapi5')
voices = engine.getProperty("voices")
engine.setProperty('voice' , voices[0].id)

# creating a speak fun
def speak(text):
    """
    this function will convert text to speech
    argument : text
    returns : voice
    """
    engine.say(text)
    engine.runAndWait()

# taking comman
def takeCommand():
    """
    this functions takes commands i.e 
    inputs the speech of user
    """
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening .........")
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognizing...")
        query = r.recognize_google(audio)
        print(f"Command : {query}\n")
    except Exception as e:
        print("Could not request results from Google Speech Recognition service" , e )
        print("say that again please !!!")
    return query

# Greeting function
def wish_me():
    hour = (datetime.datetime.now().hour)
    if hour >= 0 and hour <= 12 :
        speak("Good Morning sir , How are you doing ?")
    elif hour > 12 and hour <= 18:
        speak("Good afternoon sir , How are you doing ?")
    else:
        speak("good evening sir , how are you doing ?")
    speak("How can i help you ?")

wish_me()
while True:
    text = takeCommand().lower()
    # speak(text)

    if text is None:
        continue

    if "your" in text and "name" in text:
        speak("My name is Jarvis and i am developed by Sir Rijan Dhakal . How can i assist you today ?")

    if "doing" in text and "well" in text:
        speak("Marvelous , How can i assist you today ?")
    
    if "doing" in text and "bad" or "not good" in text:
        speak("No problem sir , never stop grinding . How can i assist you today ?")
    
    if "time" in text:
        st = datetime.datetime.now().strftime("%H:%M:%S")
        speak(f"the time is {st} ")

    elif "how are you" in text:
        speak("I'm very nice boss ! How can I assist you today?")
        
    elif "who" in text and "you" in text :
        speak("I am Jarvis, your personal assistant. How can I help you?")

    elif "thank" in text:
        speak("You are welcome boss")
    
    elif "exit" in text:
        speak("Good bye boss , have a wonderful time.")
        exit()
    
    elif "google" in text :
        speak("ok boss . Opening google...")
        webbrowser.open("https://www.google.com/")
    
    elif "facebook" in text:
        speak("ok boss . opening facebook")
        webbrowser.open("https://www.facebook.com/")
    
    elif "instagram" in text:
        speak("ok boss . opening instagram")
        webbrowser.open("https://www.instagram.com/")

    elif "youtube" in text:
        speak("ok boss . opening youtube")
        webbrowser.open("https://www.youtube.com/")
    
    elif "wikipedia" in text:
        speak("Searching wikipedia...")
        text = text.replace("wikipedia" , "")
        result = wikipedia.summary(text , sentences = 2)
        print(result)
        speak(f"according to wikipedia {result}")
    
    elif "play" in text or "music" in text:
        speak("which song you want to listen boss")
        song = takeCommand().lower()
        speak(f"playing {song}")
        webbrowser.open(f"https://www.youtube.com/results?search_query={song.replace(' ', '+')}")


    else:
        continue
