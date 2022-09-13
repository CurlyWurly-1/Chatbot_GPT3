# Chatbot
Speech recognition feeding GPT-3, with the response being spoken back.


GENERAL INFO - How to install on your laptop/desktop

 - You need to have Python3 installed (e.g. 3.10) , a useful IDE (e.g. VsCode) and some basic programming knowledge
 - There are 2 main python programs:
   - The "WIN10" version called "WIN10_chatbot.py" is self contained i.e. it doesn't call "speak.py".
   - The "Jetson Nano" version called "jetson_nano_chatbot.py" uses a separate program called "speak.py" for speech output
 - To use theses programs, you will have to install the following modules (works on python3.10). In WIN10, execute the following in an elevated  "CMD Prompt" window (Run as Administrator). If executing in Jetson Nano, add SUDO before the commands 
   - pip3 install pyttsx3
   - pip3 install openai
   - pip3 install speechRecognition
   - pip3 install PyAudio
 - Be aware that the speech recognition part runs in your desktop/laptop, so the speed of speech recognition relies on how fast the CPU is. 

GPT3 INFO - How to get an API key

To get this working with GPT-3, you will need to modify the code to enter your GPT-3 API Key (In the WIN10 Python program, look at about line 30). You can get an API key as follows:
 - In a browser go to https://openai.com/api/ and create your own account
 - When you are logged in, click top right on the "Personal" icon and select "View API keys". In the next screen, press "Create new secret key" and copy the key that gets created. The format of the key will be something like "zz-xxxxxxxxxxyyyyyyyyyyzzzzzzzzzzaaaaaaaaaabbbbbbbb" 
 - Copy this key into the python program (about line 30) so that it looks something like this. N.B. This mocked up value will not work - you must create your own! 
   - openai.api_key = "zz-xxxxxxxxxxyyyyyyyyyyzzzzzzzzzzaaaaaaaaaabbbbbbbb"


USAGE - Brief info on how it works
 - The concept is this 
   - After the python program has initialised, The program pauses at the "listening" prompt. The program is now waiting for sounds to exceed a set background noise level. 
   - When someone speaks, the sound level will exceed the background noise level and so this triggers the python program to record the audio from now on until a period of silence has been exceeded. The period of silence indicates that speaking has finished and so this then kicks off the next process, where the python program now tries to translate the words it has just heard into text form, which is stored in a text variable. 
   - The python program now passes the text sentence (the contents of the text variable) into the GPT-3 cloud system via the GPT-3 API.
   - The GPT-3 cloud system processes the input text sentence using its own AI processes, and tries to construct a semantically relevant text sentence as a response.
   - The GPT-3 cloud system now passes this response text sentence back to the python program via the GPT-3 API. 
   - In the python program, This response text sentence is now passed to the speech part of the program so that it can be spoken back to you. After the spoken part has finished, the python program then returns back to the start i.e. the "listening" prompt will be re-displayed, so you can say something else.
 - To get this working, try executing it first with a headset. If the headset is working OK, then the program should automatically pick up which device to use (Nano can be tricky here).
 - Only speak after you see "listening". The program automatically detects when you have finished speaking and if all OK, you should then see "processing". The spoken output will then be issued and after it has finished, you will see "listening" again
 - Try asking "Who are you". The reply should say "Buddy" but be aware that if your device performance is poor, you may have to wait quite a few seconds for the speech recognition part to complete. If you don't get anything spoken back after 20 seconds, something is wrong - Check the device connections 
 - Try saying the following and hear what you get back - Check the python code to see how these responses were programmed 
   - What is your name?
   - What is my name? 
   - How old am I?
   - When is my birthday?  
 - If you extended the "prompt" info to include where you live now, you could ask what are the best restaurents near where I live 

