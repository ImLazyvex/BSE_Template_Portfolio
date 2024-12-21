# Voice Assistant with AI
This project uses Rasberry Pi and ChatGPT to create a voice assistant. This voice assistant listens to voice commands and has an interaction with the user, also responding with a voice.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Rushil S. | Monta Vista High School | Computer Science | Incoming Sophomore |

<!--
**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**
-->

<img src="Rushil.jpg" width="300" height="400" />

# Final Milestone

<iframe width="935" height="526" src="https://www.youtube.com/embed/yWZoRjWE-IM" title="Rushil S. Third Milestone" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<h3>Summary</h3>

I created all the code using libraries like SpeechRecognition, openai, lgpio, and pyttsx3. SpeechRecognition was used to capture user speech from the USB microphone and then turn it to text. After this multiple if and elif statements check for certain keywords and phrases that may be in the user's inputted speech. If "turn on/off the light" comes from the input, then a light on a breadboard is controlled using the lgpio module to turn on and off. If the name "Tom" is said, a conversation is started and a method called get_response() is called. This method makes openai use the text from the user's input to generate a text response through the ChatCompletion.create() method. Finally, pyttsx3 is used to turn that text into outputted speech that is heard from the USB speaker. 

One special feature is that if the user has already started a conversation earlier in the program (by saying "Tom"), then the user doesn't need to continue saying "Tom" to keep generating responses from the voice assistant. To end a discussion, the user just has to say "end discussion/stop discussion" and the AI will stop responding until the user says "Tom" again.

<h3>Challenges and What I Learned</h3>

My main struggle in BSE was the hardware as I had never dealt with circuitry before and barely used any tools before while doing robotics since I always coded. I eventually learned it with the help of the instructors and became comfortable with making circuitry for my project, using items like the relay module, and using tools like the solder. Another challenge I had was getting the Raspberry Pi interface to be stable, as it was continously freezing which caused annoying interruptions during my code tests, dependency installations, etc. I figured out that I had to use a hotspot during my 3rd milestone, which luckily was the only time I was really coding. 

My biggest triumphs overall from BSE were learning how to deal with circuits, learning how to use a Raspberry Pi, and creating a good, working project at BSE. Some key topics I learned at BSE were learning how to use speech to text and text to speech modules and most importantly AI modules. 

<h3>What's Next</h3>

I would like to expand on my project by allowing the user to continue previous conversations and allow the AI to use context from previous conversations. This would be so that the user doesn't have to restate everything from a previous conversation again. This would also make the AI more familiar with the user, what they talk about, and their preferences.

# Second Milestone

<iframe width="935" height="526" src="https://www.youtube.com/embed/CYtspTGLkoA" title="Rushil S.  Second Milestone" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<h3>Summary</h3>

During my second milestone, I added the entire circuitry. This includes a relay module connected to the Raspberry Pi which recieves the high/low signals from the Raspberry Pi. The relay module controls electricity flow from the battery pack back to the LED circuit on the breadboard. Essentially if it's high, then electricity is flowed back into the LED circuit from the battery pack, but if it's low, then the LED circuit doesn't get and power back from the battery pack. The LED is connected to resistors to prevent it from taking too much voltage in, as the battery pack provides 6V of power. I also installed all the dependencies onto my Raspberry Pi so I can use certain libraries when I code during my next milestone.

The simplicity at the core of the project constrasted to the complex errors that are outputted really suprise me. This is because you can find an error that doesn't seem to relate to anything on your project yet something totally random causes it. For example, I had a wire plugged into the wrong pin but an error related to my USB mic was being outputted. And this is all while you have only a few parts connected.

<h3>Challenges</h3>

One challenge I faced while building the circuitry was the LED frying continuously despite it being connected to a resistor that should've reduced the voltage coming towards the LED. What I didn't realize was that it was such a weak resistor that almost no power was being taken away from the circuit.
Another problem I had was understanding the relay module as I had never seen one before and online tutorials/descriptions provided very little to no explanation as to how to use one. 

<h3>What's Next</h3>

Next I am going to be making the code for my project to allow it to use the AI to generate responses based on the text it hears. I also want to make it commit actions based on certain keywords and phrases it hears such as "turn on the light" to turn on an LED on a breadboard.

# First Milestone

<iframe width="935" height="526" src="https://www.youtube.com/embed/qS4kptm6oVI" title="Rushil S. First Milestone" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<h3>Summary</h3>

In my project, I use a USB microphone and a USB speaker. I also have a Raspberry Pi (4) and an HDMI Video Capture device. I use a PiSwitch to control the on and off of the Raspberry Pi as it can go between the power supply and the Raspberry Pi itself. The USB microphone and speaker both connect to the Raspberry Pi and in the future will be used to capture user audio and provide a response. The HDMI Video Capture device is connected to both the Raspberry Pi and the computer. This is so that the Raspberry Pi's interface can be displayed on OBS, which allows for coding the Raspberry Pi, installing dependencies on it, etc. So far I have generated an OpenAI API key for future use when I create the code for the Voice Assistant. I have also installed the OS onto the microSD card for the Raspberry Pi. 

<h3>Challenges</h3>

A big challenge I faced while setting up the Raspberry Pi was the OS on the mircoSD card corrupting. I closed OBS at a point without shutting down my Raspberry Pi and somehow the OS corrupted so I had to restart and reinstall the Raspberry Pi OS onto the microSD card. Another problem I had was the PiSwitch not working, but eventually the PiSwitch fixed itself. My last challenge, which wasn't too big, was related to using OBS as the Raspberry Pi's interface sometimes got stuck on booting, but after the reinstallations of the OS due to the other OBS prblem, the booting problem also was fixed.

<h3>What's Next</h3>

In the future I will install the dependencies onto the Raspberry Pi and build the circuit for the voice assistant which will include an LED to turn on and off using the voice assistant. I will also create the code much later on using the speech recognition libraries and other Raspberry Pi related libraries.

# Schematics
<img src="voiceassistantschematic.png" width="600" height="400" />

# Code

```python
import lgpio
import speech_recognition as sr
import pyttsx3
import openai

# Initializing pyttsx3
listening = True
engine = pyttsx3.init()

# Set your openai api key and customize the chatgpt role
openai.api_key = "ABC"
messages = [{"role": "system", "content": "Your name is Tom and give answers in 2 lines"}]

# Customizing the output voice
voices = engine.getProperty('voices')
rate = engine.getProperty('rate')
volume = engine.getProperty('volume')

# Define the GPIO pin number for the relay
RELAY_GPIO_PIN = 18

# Initialize the GPIO
h = lgpio.gpiochip_open(4)

# Set up GPIO pin as output for the relay
lgpio.gpio_claim_output(h, RELAY_GPIO_PIN)

def get_response(user_input):
    messages.append({"role": "user", "content": user_input})
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=messages
    )
    ChatGPT_reply = response["choices"][0]["message"]["content"]
    messages.append({"role": "assistant", "content": ChatGPT_reply})
    return ChatGPT_reply

def turn_on_light():
    lgpio.gpio_write(h, RELAY_GPIO_PIN, 1)
    print("Light turned ON")

def turn_off_light():
    lgpio.gpio_write(h, RELAY_GPIO_PIN, 0)
    print("Light turned OFF")

while listening:
    with sr.Microphone() as source:
        recognizer = sr.Recognizer()
        recognizer.adjust_for_ambient_noise(source)
        recognizer.dynamic_energy_threshold = 3000

        try:
            print("Listening...")
            audio = recognizer.listen(source, timeout=5.0)
            response = recognizer.recognize_google(audio)
            print(response)

            if "tom" in response.lower():
           
                response_from_openai = get_response(response)
                engine.setProperty('rate', 120)
                engine.setProperty('volume', volume)
                engine.setProperty('voice', 'greek')
                engine.say(response_from_openai)
                engine.runAndWait()
            
            elif "turn on the light" in response.lower():
                turn_on_light()

            elif "turn off the light" in response.lower():
                turn_off_light()
                
            else:
                print("Didn't recognize 'turn on the light' or 'turn off the light'.")

        except sr.UnknownValueError:
            print("Didn't recognize anything.")

# Clean up GPIO on exit
lgpio.gpiochip_close(h)
print("GPIO cleanup completed")
```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| CanaKit Raspberry Pi 4 4GB Starter PRO Kit - 4 GB RAM | This is used to setup the Raspberry Pi (power supply, OS, cooling systems, etc). | $119.99 | <a href="https://www.amazon.com/CanaKit-Raspberry-4GB-Starter-Kit/dp/B07V5JTMV9/ref=sr_1_3?crid=3I3XY2ESCUCT9&dib=eyJ2IjoiMSJ9.rWngnqnkl0ze0Tu3Q89m-YyU-TuUu5H4EMJPDIgXQWCwbXT8lsJ8fb2-wg7gIbBJ8WM4PJbB1M3gRUYqjucM4RLndoVWVnz1DPY7kEp-sdrcjct9cl9cHpMy4d4CkWd3NQCEZYEA1BfUEJ9shmgH8GrvVNP6xx_vyfJFr-6t7JUC__VJ31efjqF0QijDPe1q_FoMVwdnQPxWnyEBmnnMduXCdDvDfe4RWoyXPgtMazFFI08-sM8kqzOL0v0Xz4Kt_lKxTMvz9h2eiFSLk27fE19Ox_DmrlnK7A6aIPg7UD0.e7PYmGO8gXf6rqj6ZP-MNcl8u78WcJz-fjfFvesuiVw&dib_tag=se&keywords=cana%2Bkit%2Braspberry%2Bpi%2B4&qid=1719254845&s=electronics&sprefix=canakit%2Braspberry%2Bpi%2B4%2Celectronics%2C120&sr=1-3&th=1"> Link </a> |
| AXHDCAP 4K HDMI Video Capture Card, Cam Link Card Game Audio Capture Adapter HDMI to USB 2.0 Record Capture Device for Streaming, Live Broadcasting, Video Conference, Teaching, Gaming | The HDMI Capture Card is used to connect the Raspberry Pi to the computer and displays the Pi's interface on the computer through OBS, a display software. | $9.98 | <a href="https://www.amazon.com/Audio-Express-AXHDCAP-Broadcasting-Conference/dp/B0C2MDTY8P/ref=sr_1_3?crid=3CYMQPJXZRG8C&dib=eyJ2IjoiMSJ9.m1E68xLLqhA5tsiHj04YRMJb8qOQG0I9OIpslSLmshw3-fn3xScLIzDEqGlqaXSGxtAQAPa-AOpmBLNL66x1bKwc7JRj5VG3K5KdIgodTnLWYtH_YL-Erp_-J95CCnBd4FvfMl8J43ZIR1c0l4DVqPKDRjmOKmUSCPiBrVgl_xpCuzT5vQNfpbp9PMT3iHnqcy3gw8r3QSnb6jxE0LerJzDC7nGw71z3-MLAtCMa0wh3Y2JPGQTEGoNKP5c1q6KNaVIVkq3g28A7yIQCXTdzUnRciCgg01U8Vz-K5XLBEUQ.jcZvqXwyFOd_ecf2tS-oanK5CPwNooPeurTQLRoY814&dib_tag=se&keywords=hdmi+capture+card&qid=1719254880&s=electronics&sprefix=hdmi+capture+car%2Celectronics%2C136&sr=1-3"> Link </a> |
| Youmi Mini USB 2.0 Microphone Mic for Laptop/Desktop PCS - Skype/Voice Recognition Software Driver-Free Audio Receiver Adapter for MSN PC Notebook | This mini USB mic is used to take in user speech as an input directly into the Raspberry Pi. | $7.96 | <a href="https://www.amazon.com/Newest-YOUMI-Microphone-Laptop-desktop/dp/B01MQ2AA0X/ref=sr_1_4?crid=1BQLNHUY2LHCU&dib=eyJ2IjoiMSJ9.cXsUHDop17wBDFrYbVzRrHrOY7kUIPMiN1S0YCF5404Wgb0QjQT1wceu3Q8jkkRHLxgAk26JOwDWRuAiCko8EaN7zvVFG_q40WHskbnh_lh1ygpmk7WO1bli8rKX0dIXgq9ZmuUo-f8scAzuiixKYHUqT9d8Er8MADzLu9G5l2h5lV5bg0iFkLRZY0Ogp3jYJKazsimT2Z4_wRT_2ZsmlqDKlT5chu3rOhCPbD-B1GLYGwTOWArf0vYo675I5ZSV0T-1tTis95pypu4Pw4RCA6v2awtZBAJJQGh9bT6SrdY.gD6a-wpksQfcfHIGeBmxmVOxPB2wPCIqCP4wgSe1Fac&dib_tag=se&keywords=mini+usb+microphone&qid=1719254942&s=electronics&sprefix=mini+microphone%2Celectronics%2C157&sr=1-4"> Link </a> |
| USB Mini Speaker Computer Speaker Powered Stereo Multimedia Speaker for Notebook Laptop PC(Black) | This USB speaker is plugged into the Raspberry Pi and outputs the response generated by the OpenAI API using text to speech. | $12.99 | <a href="https://www.amazon.com/HONKYOB-Speaker-Computer-Multimedia-Notebook/dp/B075M7FHM1/ref=sr_1_3?crid=2SDLTTDK66DTZ&dib=eyJ2IjoiMSJ9.0-6fNa1XyAe92bnEjoLadYyiU339uTafOqA19X5YlwQ9i4XcyPCYTNNbH2vS6gRPaNs7mxlOunD1MtzGaLjQSzDKRx8ezG2TepjVNPgZEMcVr9vaBVIZCQFwfXUzTIZ28D4Aby6KRCZjXSM6eu0mhw.ZM5vShmdj24UC2kX0Zh06-sgaqYvyJaNgyslXVHUwwk&dib_tag=se&keywords=adafruit%2Busb%2Bspeaker&qid=1719254984&s=electronics&sprefix=adafruit%2Busb%2Bs%2Celectronics%2C112&sr=1-3&th=1"> Link </a> |
| HiLetgo 2pcs 5V One Channel Relay Module Relay Switch with OPTO Isolation High Low Level Trigger | This relay module is connected by wires to the Raspberry Pi to be sent a high and low signal to control electricity flow to whatever it is connected to (i.e an LED), controlling on and off. | $7.39 | <a href="https://www.amazon.com/HiLetgo-Channel-optocoupler-Support-Trigger/dp/B00LW15A4W/ref=sr_1_2_sspa?crid=2SLR7UAFCVOIE&dib=eyJ2IjoiMSJ9._DYrg2VaJ__x0WDwc6kzeKzUZ-I4cG_HuKZguKLJ6x2wU1JWRAwS7DXLXaPIqbDC75yrqeufpq5UIjGYHhyPUxsyI1oDFu_xzRGc6JKWduau0Cj_6h0WhCwygPCtvA4_CgYTlryCan8bYBTf8OuDtGnTHNTNy8HIE5u3vAD2ZvF2iqD9pHIOJo9CTFOLb1co4zIsEVCo2ff6SQZqB8Ydi-9P0zeNgCAj4aBscyz5IYf1-8t5ilh3uW4sioFKwkUiRVyO-VPdg6PyLJ-9ZzOA1VTnVwBr0zxKjkxOA1sXyzE.Y9tJENLjhR535KMgmf2mT8tunOt8rUZxFo0aKOdIi3A&dib_tag=se&keywords=single+relay+module&qid=1720195075&s=electronics&sprefix=songle+relay+modul%2Celectronics%2C145&sr=1-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |

<!--
# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
-->

# Starter Project

<iframe width="935" height="526" src="https://www.youtube.com/embed/4CdzAQ-fwT0" title="Rushil S.  Starter Project" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<h3>Summary</h3>

This project uses a pushbutton to toggle between two LED lights. The pushbutton is connected to a 5V pin, a ground through a resistor, and a digital pin. The digital pin allows for the pushbutton to be used as an input mechanism, as connecting the pushbutton to the digital pin allows for the pushbutton's state (pushed or not) to be continuously read. There are 2 LEDs which both have the same setup in terms of connection to the Arduino board. Each LED has a direct connection to a ground, and then through a resistor, connects to a digital pin. These digital pins allow the LED's state (on or off) to be controlled by the code. All of the cables, resistors, LEDs, and pushbuttons have been soldered into the protoshield. For items that aren't connected in the protoshield (which has specific rows and columns that are automatically connected due to metal lining), solder is used to form those connections between the items. There are pins soldered into the protoshield that extend all analog, digital, etc pins from the Arduino board. 

The code uses setup() to initialize the 2 LEDs as outputs and the pushbutton as an input. This is all done using their ports so the computer understands where the LEDs and pushbutton are. In loop(), the button's current state (pressed or not) is read. Then an if statement checks if the button is being pressed and if this is the first time in the current button press that this if statement is being ran. Then the toggled is swapped (i.e. true -> false) so that based on the toggle, the right LED will be turned on and the right LED will be turned off. This creates a toggling motion for each button press. Finally, the boolean controlling whether the if-statement has already been ran in the button press is set to true, which stops the LEDs from infinitely toggling. Once the button is released (not being pressed), then the boolean controlling whether the if-statement has been ran is set to false so the next time the button is pressed, the LEDs can be toggled. 

<h3>Challenges</h3>

While soldering, a bit of the solder itself spilled onto the middle columns. This caused the entire circuit to short as the 5V and Ground sides were interacting with each other. Another challenge was getting the polarity of the LED correct. At the start, I put the LED the wrong way, not realizing this can cause it to not function. I had to desolder the LED and put it in a new spot, making sure it was placed the right way. An interesting problem I encountered near the end was using pin 13. Pin 13 controls the Arduino Board's LED no matter what, so when I used pin 13 for one of the LEDs, it was not being turned on, instead the board's LED was turning on. 

<h3>What's Next</h3>

In my main project, I will learn how to use and work with Raspberry Pi, and I will learn how to use the OpenAI API. I will figure out how to setup a Raspberry Pi and how to create circuits and code circuits for it.

<h3>Code</h3>

```c++
// constants because they are pin numbers
const int BUTTON_PIN = 7;  // the number of the pushbutton pin
const int LED_PIN =  9;   // the number of the LED pin
const int LED_PIN2 = 13; // number of LED pin # 2
bool isToggled = false; // checks which LED should be turned on (False -> LED 1, True -> LED 2)
bool alreadyRan = false; // checks if loop is running multiple times on one button press so lights don't continuously switch

// buttonstate changes
int buttonState = 0;   // variable for reading the pushbutton status

void setup() {
  // initialize the LED pins as outputs:
  pinMode(LED_PIN, OUTPUT);
  pinMode(LED_PIN2, OUTPUT);
  // initializing the pushbutton as an input device
  // the pull-up input pin will be HIGH when the button is pressed and LOW when the button is not pressed.
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {
  // reads the state of button (pushed/not pushed) --> HIGH/LOW
  buttonState = digitalRead(BUTTON_PIN);
  
  // control LED according to the state of button
  if(buttonState == HIGH && !alreadyRan)         // If button is not pressed
  {
    isToggled = !isToggled; // swaps toggle to other side
    if (isToggled)
    {
      digitalWrite(LED_PIN2, HIGH); // turn on LED # 2
      digitalWrite(LED_PIN, LOW); // turn off LED # 1
    }
    else
    {
      digitalWrite(LED_PIN, HIGH); // turn on LED # 1
      digitalWrite(LED_PIN2, LOW); // turn off LED # 2
    }
    alreadyRan = true; // This will make it so if statement isn't entered multiple times in one button press
  }
  else if (buttonState == LOW)
  {
    alreadyRan = false; // Allows if to be entered again since button has been released now
  }
}
```
