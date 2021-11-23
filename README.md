# mini-AI
# mini AI . it is perform some simple task .like as open google , open youtube and open instagram etc .
# .................................................start coding........................................
import speech_recognition as sr
import datetime
import wikipedia
import pyttsx3
import webbrowser
import random
import os  

#text to speech
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')


#print voices
engine.setProperty('voices',voices[0].id)
 
def speak(audio): 
    engine.say(audio)
    engine.runAndWait()

def wish():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour<12:
        speak("good morning sir ")
    elif hour>=12 and hour<18:
        speak("good afternoon sir ")
    else:
        speak("good night sir  ")
    speak("please tell me.  how can  help you")

def takecommand():
    ''' takecommand means aiis listen and then take  ans
    '''
    r = sr.Recognizer() 
    with sr.Microphone() as source:
        print("i am listning...")
        r.pause_threshold = 1
        r.energy_threshold = 500
        audio = r.listen(source)
    try:
        print("recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print("you:",query)  
         
    except Exception as e:
        #speak("errofr....")
        #print(e)
        print("say that again please......")
        return "none"
    return query

# for main function
if __name__ == "__main__":
    wish()
    takecommand()
    

    while True:
        query = takecommand().lower()
        
# wikipedia search
        

        if 'wikipedia' in query:
            speak('searching wikipedia sir....')
            query = query.replace("wikipedia","")
            results = wikipedia.summary(query, sentences=2) 
            speak(results)
            print(results)

            
        elif 'open youtube' in query or "open video online" in query:
            webbrowser.open("www.youtube.com")
            speak("opening youtube sir")

        elif 'open google' in query or "open chrome" in query:
            webbrowser.open("https://www.google.com")
            speak("opening google sir")

        elif 'open facebook' in query:
            webbrowser.open("https://www.facebook.com")
            speak("opening facebook sir")

        elif 'open instagram' in query:
            webbrowser.open("https://www.instagram.com")
            speak("opening instagram sir")

        elif 'open music' in query or 'play music' in query:
            music_dir =  'S:\\music\\songs'
            songs = os.listdir(music_dir)
            print("playing music sir")
            speak("playing music sir")
            os.startfile(os.path.join(music_dir, songs[0]))  


        elif 'exit' in query or 'stop' in query  or 'shutup' in query  or 'quit' in query  or 'bye' in query:
            ex_exit = 'ok. thank you sir'
            speak(ex_exit)
            exit()
            print(ex_exit)    

        elif "shutdown" in query:
            speak ("ok sir your system is shutdown ")
            os.system('shutdown -s')

        
