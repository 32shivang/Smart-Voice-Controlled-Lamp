# Smart-Voice-Controlled-Lamp

Developed an automated voice-controlled Lamp. Used Adafruit io cloud service and IFTTT API.

Materials:

The only physical materials required are:

- An ESP8266 breakout board (I used the ESP-12E from Acrobotics)
- A Google Assistant enabled device (Apps available for Android and iPhone, or Google Home)
- A computer with access to the Internet

While these are the only physical materials required, this tutorial also requires that you set up accounts on various websites, and install the Arduino IDE.

- Adafruit IO - Create a free account.
- IFTTT - Create a free ("Maker") account.
- Google - The same account you're using the Google Assistant for.

## Steps to automate your home:

### Step 1: Setting Up Adafruit IO

Adafruit IO is an IOT platform built around the Message Queue Telemetry Transport (MQTT) Protocol. MQTT is a lightweight protocol that allows multiple devices to connect to a shared server, called the MQTT Broker, and subscribe or write to user defined topics. When a device is subscribed to a topic, the broker will send it a notification whenever that topic changes. MQTT is best suited for applications with low data rates, strict power constraints, or slow Internet connections.

In addition to providing the MQTT Broker service, Adafruit IO also allows you to set up dashboards that let you directly manipulate or view the current value of each topic. Since it can be accessed from a web browser, it makes it the ideal hub for monitoring and controlling all of your various IOT projects.

After creating your Adafruit IO account, you should be taken to the homescreen. Select "Feeds" from the left-hand menu. Click the Actions drop-down menu, and create a new feed. I called mine "onoff".

Next, go to Dashboards in the left-hand menu. Click the Actions drop-down menu, and create a new dashboard. I called mine "LightSwitch". Open the new dashboard, and you should be taken to a mostly blank page. Pressing the blue + button will let you add new UI components to the dashboard. For now, all we'll need is a toggle button, which should the first option. When prompted to choose a feed, select the one you just made, and keep the defaults for the rest of the settings.

That's all for now on the Adafruit IO end of things. Next step is connecting your ESP8266 to the MQTT Broker.

### Step 2: Connecting the NodeMcu

Connecting NodeMcu to the Adafruit IO system is relatively straightforward. Before you get started with the code, you'll need to install the Adafruit MQTT Client library, which can be found under the Arduino Library Manager (Sketch > Include Library > Library Manager...). Even though this library is produced and maintained by Adafruit, it can be used to connect to any MQTT server.

Please see the code from Lamp_Automation.ino file

### Step 3: Connecting to Google Assistant Through IFTTT

In this last step, we'll connect our Google Assistant to the Adafruit IO MQTT Broker to allow us to control the lights with voice commands. To do this, we'll use the IFTTT (If This Then That) platform, which allows hundreds of different services to trigger actions in a variety of other services.

After you've set up your account and taken a look around, you'll need to go to the Maker's Platform to start making your own applets. Select "Private" from the left hand menu, then click the blue "New Applet" button. This will take you to the applet editor, where you choose triggers ("If This") and the subsequent actions ("Then That").

For your trigger, choose "Google Assistant" as the service, then select "Say a simple phrase" from the drop down menu of specific triggers. This will bring up a new list of fields to fill in, including variations of the activation phrase, the Google Assistant's response, and the language. For my activation phrases, I chose "Turn the light on," "Turn on the light," and "Switch the light on".

The next section is the filter, which allows your applet to do different things based on either global variables, like time of day, or manipulate user input with a simple Javascript-like language. This is a more advanced feature that I may come back to in a later tutorial, but for now you don't need to worry about it.

The final part of your applet is the Action, what your applet does in response to the Trigger. For the service, choose "Adafruit", and for the specific Action, choose "Send data to Adafruit IO". This will bring up two fields that you need to fill in. The first should be replaced with the name of the Adafruit IO feed you want to send data to, in this case "onoff". The second field is the data to send. For this applet, we'll send "ON", which is the string our ESP8266 is waiting for.

Now all that's left is to add the title and description. Since this is a private applet, they don't really matter that much, but the IOFTTT standard is to have the title be a brief description of what the applet does while the description is a more in depth look at how the applet works.

Once you have that applet finished, create a second one for turning the lights "OFF". You should now see two applets on your IFTTT Platform page. To activate them, go to the My Applets page on the main IFTTT site, click on the applet card, and click set the on-off toggle switch to "On". If you haven't already, IFTTT will ask to connect to your Adafruit IO and Google Assistant accounts. Allow the accounts to be linked, then turn on the second applet as well.

Once both applets are turned on, the setup should be complete!

### Step 4: Testing and Troubleshooting

Now all that's left is to test the system. To do this, you'll need a device with the Google Assistant enabled. This is built into the latest versions of the Android operating system, as well as the Google Home series of devices. If you don't have either of these, the Google Allo messaging app, available for Android and iOS, also includes the Google Assistant. Start up the assistant, make sure it's logged into the proper account, and say the activation phrase you used in the previous step. After a 2-5 second delay, the light on your ESP8266 board should switch on or off. Try the other phrase, and make sure it works too.

Congratulations! You've just made a internet-connected, voice controlled light! Hopefully this tutorial has provided enough of a foundation that you can start making your own variety of voice-controlled IOT projects. Have fun!

## Troubleshooting

There are a number of places that the connection between your voice and the light can break down. If the light isn't changing when your speak, there are a few things you should check.

- Does the light change when you toggle the switch on the Adafruit IO dashboard? If not, your ESP8266 is either not connecting to the server, not subscribing to the feed, or not checking for the correct string values. Check the Serial Monitor output of your ESP8266 device to find out which.
- Is the Google Assistant hearing you properly? If you use the Google Allo app, you can see what the Assistant heard, or you can directly type the phrase you want it to interpret.
- Is the Google Assistant responding with the correct phrase? If not, then your Google account and your IFTTT account aren't connected. Make sure you're using the same Google accounts for the assistant and IFTTT.
- Is the Adafruit IO dashboard not updating when the IFTTT applet triggers? If not, then your Adafruit IO account and your IFTTT account aren't connected. Double check on IFTTT to make sure that your accounts have been linked.

# DEMO: https://bit.ly/3itm8Qd

### Thank You
