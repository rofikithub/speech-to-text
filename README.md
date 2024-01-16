# Speech To Text

A few lines of code written in python using libraries (SpeechRecognition, PyAudio) that convert speech to text. 

## Prerequisites

In order to run the python script, your system must have the following programs/packages installed.
* Python 3.6.7
* SpeechRecognition 3.8.1 (Internet required to convert speech to text while execution)
* PyAudio

## Approach
* script.py execute in terminal.
* After a printed start in the terminal, you begin to speak in English and end once your sentence is completed. 
* It will take a few minutes to convert speech to text and print on your terminal.
  
## Install Packages
* pip install SpeechRecognition 
* pip install PyAudio 
* pip install sounddevice 

## Code
```
# Program to convert speech to text
# Author @rofikithub

import speech_recognition as sr

recognizer = sr.Recognizer()


def capture_voice_input():
    with sr.Microphone() as source:
        recognizer.adjust_for_ambient_noise(source=source)
        print("Listening...")
        audio = recognizer.listen(source)
    return audio


def convert_voice_to_text(audio):
    try:
        text = recognizer.recognize_google(audio)
        print("You said: " + text)
    except sr.UnknownValueError:
        text = ""
        print("Sorry, I didn't understand that.")
    except sr.RequestError as e:
        text = ""
        print("Error; {0}".format(e))
    return text


def process_voice_command(text):
    if "hello" in text.lower():
        print("Hello! How can I help you?")
    elif "goodbye" in text.lower():
        print("Goodbye! Have a great day!")
        return True
    else:
        print("I didn't understand that command. Please try again.")
    return False


def main():
    end_program = False
    while not end_program:
        audio = capture_voice_input()
        text = convert_voice_to_text(audio)
        end_program = process_voice_command(text)


if __name__ == "__main__":
    main()
```
