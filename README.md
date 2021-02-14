# Virtual-Alexa-Lidya-on-Python
This is my personal virtual AI called Lidya. 


import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes




listener = sr.recognize()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voices',voices[1].id)

def talk(text):

    engine.say(text)
    engine.runAndWait()

def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()

        if 'lidya' in command:

            print(command)

    except:

          pass

    return command


def run_lidya():

    command = take_command()

    if 'play' in command:
        song= command.replace('play', '')
        talk('playing' + song)
        pywhatkit.playonyt(song)


    elif 'time' in command:

        time= datetime.datetime.now().strftime('%H:%M')
        print(time)
        talk('Current time is' + time)

    elif 'who is ' in command:

       person = command.replace('who is', '')
       info = wikipedia.summary(person, 1)
       print(info)
       talk(info)

    elif 'date' in command:

        talk('sorry, i am busy')

    elif 'are you single' in command:

        talk('I am in relationship with wifi')

    elif 'jokes' in command:

        talk(pyjokes.get_joke())

    else:

        talk('please say it again')

while True:
    run_lidya()








