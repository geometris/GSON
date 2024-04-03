# GSON Toolbox
## A Visual Studio Code Extension for GSON scripting and Debugging
* Easily extend existing Geometris device functionality to integrate with peripherals  and systems.
* Over the air device script debugging with breakpoints, watches, and stepping through the source code.
* For qualified opportunities, Geometris will make scripts for your systems and peripherals for free.

![GSON editing](https://skyonics.blob.core.windows.net/gsonreadme/gsoneditimg.png)

## Requirements

* The GSON Toolbox requires .NET 8. You can download and install .NET 8 [here](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
* To use GSON scripting, you'll need a Geometris Whereqube device with firmware installed that supports GSON scripting. Contact [support](mailto:support@geometris.com)
* To use serial port attached scripting and debugging, you'll need to have a serial port harness, power supply, and the appropriate drivers installed. Contact [support](mailto:support@geometris.com)
* To use live debugging and the CAST configuration management portal integration, you'll need an API key supplied by Geometris. Contact [support](mailto:support@geometris.com)
* If you want to use live debugging on devices that user your own sim, you'll need to use either the [Twilio API](https://www.twilio.com/en-us) to contact the device via sms, or use integration with your carrier API. Contact [support](mailto:support@geometris.com)




## Getting Started
<p>Begin creation of a gson script by creating a jsonc file (json with comments).
You can use File->New File and type your filename with a jsonc extension: for example, myscript.jsonc.</p>
<p>A gson script is a json file, supporting C style comments such as // and /*  */. To begin, simply create a json object, then we'll add the gson script json schema that defines everything a gson script can do.</p>
<code>
{
	"$schema":""
}
</code>
<p>A new menu will appear when you save the jsonc file on the upper right hand corner of Visual Studio Code.</p>

![GSON toolbox menu](https://skyonics.blob.core.windows.net/gsonreadme/gsontoolboxmenu.png) 

<p>You can use this to automatically place the gson script schema into your project by clicking "Get Schema" on the menu. This will place the file 'gsonscriptschema.json' under a subfolder named 'schema'. You may now reference this file in your document:</p>
<code>
{
	"$schema":"./schema/gsonscriptschema.json"
}
</code>
<p>Doing this enables the json schema for the Visual Studio Code editor, which will provide autocompletion to make creation of a script easier.</p>

## Learning Resources
<p>To see what is possible and learn to use the gson schema, we recommend using the GSON learning resources:</p>

* [Quick Start Guide PDF (to view directly in VSC, consider using a PDF viewer extension)](https://skyonics.blob.core.windows.net/gsonreadme/Geometris%20GSON%20Programming%20Quick%20Start%20Guide.pdf)
* The Geometris Youtube channel for tutorial videos.

<p></p>

## Using the GSON Toolbox

<p>The extension offers these functions on the drop down menu:</p>

* Get Schema
* Assemble File
* Log File Debugging
* Serial Port Debugging
* Download to Device
* Over the Air Debugging
* Save to CAST
* Update to CAST

### Get Schema

<p>Using this command, as shown before, will copy the file /schema/gsonscriptschema.json into your working folder. This makes it accessible as a json schema for your script files. Reference it through the property:</p> <code>"$schema":"/schema/gsonscriptschema.json"</code>
<p>Save the json with this property, and Visual Studio Code will provide autocomplete for your script statements written in json.</p>

### Assemble File

<p>This command converts your open jsonc file into a gson file. The gson file contains the interpreter instructions to run on your device.</p> 
<p>If your script contains any errors, the assembler will report the problems to you for correction.</p>
<p>The gson file will be written to a subfolder in your project named "out". From there, you may distribute the script to your devices through:</p>

* Manually in the CAST configuration management portal: [CAST](https://www.skyonics.net)
* Download to a device connected on your workstation's serial port (see Download to Device, below)
* Upload the script to CAST from the extension (see Save to CAST and Update to CAST below). 



### Download to Device

<p>If you have your device connected to your PC via serial port, the GSON Toolbox can directly place your assembled script onto the device using this command. It will upload the opened script, then reset the device to cause it to load the new script file.</p>
<p>This only works if you have a connected device. After the device resets, you may use the serial port debugging to initiate interactive script debugging in Visual Studio Code.</p>


### Interactive Script Debugging

<p>The GSON Toolbox provides interactive debugging capability, so that you can debug scripts running on a device directly from visual studio code.</p>

* Debug a script on a device, either attached via serial port or anywhere installed in the field.
* Set breakpoints in the script and stop execution to observe script behavior.
* Step through script commands and watch its operations on the device.
* Watch your variables and see their values in Visual Studio Code.

[Click to See Demonstration](https://skyonics.blob.core.windows.net/gsonreadme/gsondebug.mp4)

* You'll need to initiate debugging from the script file containing your "main" function.
* Set a break point simply by clicking left of your script line numbers.
* You can run the script to run until the next breakpoint is found.
* You can step into a command to debug evaluation of conditions and actions inside the command.
* You can step over a command to get to the next one. 
* You can stop or restart script debugging; this does not actually stop or restart the script on the device.
* You can create watches for your variables in the *WATCH* area of Visual Studio Code. You can't change the values manually, but you can watch as the script updates the values during execution, whenever you stop at a breakpoint or step through the code.

#### Serial Port Debugging

<p>If you have your device connected to your PC via serial port, the GSON Toolbox can debug script execution on the attached device. Make certain to assemble the script first, and use the Download to Device command to put the script onto the device.</p>
<p>Initiating the command "Serial Port Debugging" will start interactive debugging with the connected device.</p>

#### Over the Air Debugging

<p>Over the Air Debugging allows you to do interactive debugging of a script running on any device.</p>

* You'll need to have a device that is online, running script-enabled firmware, and using a script you have the source jsonc file for.
* See "Configuration of the GSON Toolbox" below.

<p>
After setting up, you can initiate the command "Over the Air Debugging". 
</p>

* The GSON Toolbox will ask you for the serial number of the device you want to connect into the debug session.
* If you are using your own sims, the GSON Toolbox will also ask for the phone number to send the SMS commands to in order to initiate the session.
* A few moments will pass while the GSON Toolbox connects the device into the session.
* The debugging toolbar will appear at the top of the workspace, and now debugging operations are possible.


### Configuration of the GSON Toolbox

<p>In order to integrate with CAST, or to initiate over the air debugging to a device with a Geometris SIM, you'll require an API Key from Geometris.Contact [support](mailto:support@geometris.com)</p> 
<p>To configure the API key, 

1. Click the extensions button on your Visual Studio Code navigation bar.
2. Find the GSON Toolbox in you list of installed extensions.
3. Click on the gear to open the configuration menu, then click "Extensions Settings"
4. Visual Studio Code will display the extensions setting page.
![Settings](https://skyonics.blob.core.windows.net/gsonreadme/gsontoolboxsettings.png)
5. Enter your API Key in Gson: Skyonics API Key
</p>
<p>
If your devices use Geometris SIMs, Click: Gson: Is Native to indicate you use Geometris sims.
</p>
<p> 
If your devices do not use Geometris SIMs, you'll need to integrate via the Twilio API.

* Click off the Checkmark: Gson: Is Native to indicate you use your own sims.
* Enter your Twilio integration details ino the fields named "Twilio API Key", "Twilio From", and "Twilio SID".
* You can click on the files icon to return to your project.
</p>

) 

<p>You can use this to automatically place the gson script schema into your project by clicking "Get Schema" on the menu. This will place the file 'gsonscriptschema.json' under a subfolder named 'schema'. You may now reference this file in your document:</p>
<code>
{
	"$schema":"./schema/gsonscriptschema.json"
}
</code>
<p>Doing this enables the json schema for the Visual Studio Code editor, which will provide autocompletion to make creation of a script easier.</p>
