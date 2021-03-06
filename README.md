Nfc Creator
==============
The Java ME-based NFC Creator can write many different NFC Forum NDEF message formats to all supported tag formats, delete the existing message from a tag (by overwriting it with an empty message), read the contents of an NDEF-formatted tag and clone the message to other tags. The application checks the device for NFC availability.

The following message types are currently supported for writing:
- Smart Poster with URI, title*, action* and image* (* optional)
- URI record, automatically encoded with all defined URI abbreviations.
- Text record; the default English language / UTF-8 encoding can be adapted in the source code.
- SMS: stored as a URI record if it contains a number and body text, or as a Smart Poster if the optional title and action are selected as well.
- Annotated URL: NDEF message containing an URL and a text record. Similar to the Smart poster, but without the meta-record to save a few bytes.
- MIME record for PNG and GIF images; the image can be selected from provided samples.
- Geo record: URL record containing a link to coordinates specified by longitude and latitude. Can be written in the "geo:" URI scheme ( http://geouri.org/), as a link to Ovi Maps (starts the Nokia Maps client on Symbian) or with the NfcInteractor.com generic maps service that works on Symbian and MeeGo Harmattan. 
- Custom record: user-definable record type and payload.
- Combination tag format: creates a message consisting of two records:
  1. Custom record (for handling with a custom content handler plug-in) & 
  2. URL (e.g., a link to the Nokia Store to download the app including the content-handler plug-in).
- vCalendar record: event in iCalendar format (uses the text/x-vCalendar MIME type), supporting summary (= subject), starting and ending date/time.

A simple reading functionality shows basic information about the tag but doesn't parse the record's contents. For Smart Poster, URI and Text records, the type and its payload are shown on the screen. For all other message types, the format and name are shown.

Deleting a tag (over)writes the tag contents with an empty record. Cloning a tag first reads the NDEF message from a tag, and then writes the cached message to any number of additional tags. Note that cloning just copies the NDEF message, it does not alter the ID of the tags.

When selecting the "Read Raw Mifare" mode, the app reads the complete contents of a Mifare tag to a log file (default: E:\nfc\). It uses the default key according to the Mifare specs. The "Write Raw Mifare" mode stores the newest log file to another Mifare tag.

The app is made in a way so that it is ideal for quickly writing various messages to tags, or as a starting point for own development tests and NFC experiments.

Therefore, the structure of the application has to be modified to be suitable for a rich tag reader / writer app - e.g., the individual record handling should be externalized into separate classes, and the UI should be modularized for the different writing modes.

Note: This project was previously called Nfc Interactor. The new and more powerful version of the Nfc Interactor is now based on Qt; this project is however still useful as a Java ME tag reading and writing example, and has therefore been renamed to Nfc Creator to reflect its focus on writing tags, whereas the new Qt-based Nfc Interactor can also analyze tags. 

More information:
http://www.nfcinteractor.com/apps/nfccreator/


PREREQUISITES
-------------------------------------------------------------------------------

- Java ME basics.


IMPORTANT FILES/CLASSES
-------------------------------------------------------------------------------

- NfcMenuForm.java : handles the user interaction and controls the Nfc Manager.
- NfcManager.java : encapsulates the NFC interaction.


KNOWN ISSUES & LIMITATIONS
-------------------------------------------------------------------------------

- The app is a flexible starting point for NDEF message experiments. For other usecases, you should extend the app to separate the NFC interaction and the various NDEF message types into extra classes.


BUILD & INSTALLATION INSTRUCTIONS
-------------------------------------------------------------------------------

Preparations
~~~~~~~~~~~~
The download includes a NetBeans 7 project, but you can also import the app with Eclipse Pulsar. If you choose NetBeans, make sure you download the full installation package. At install-time, select at least the Java ME target (including its required dependencies on standard Java SE development).

For compiling and testing, get the Symbian Belle SDK:
http://www.developer.nokia.com/info/sw.nokia.com/id/ec866fab-4b76-49f6-b5a5-af0631419e9c/S60_All_in_One_SDKs.html

Alternatively, you can use the Series 40 Nokia 6212 NFC SDK from:
http://www.forum.nokia.com/Library/Tools_and_downloads/Archive.xhtml 

Make sure you have a Symbian phone with NFC support (C7-00: Symbian Anna firmware or newer) or one of the previous NFC capable Nokia Series 40 devices to test.

Build & installation instructions using NetBeans
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open the Nfc Creator project
   File > Open Project, select the project directory.

2. Make sure you select the Symbian Belle / Series 40 Nokia 6212 NFC SDK as the target,
   especially in case NetBeans reports missing references.

3. Press the Build button to build the project and create the 
   NfcCreator.jar / .jad installation files. 
   Install the application to the device using the Nokia Ovi Suite 
   or by using NetBean's built-in deployment functionalities.


COMPATIBILITY
-------------------------------------------------------------------------------

- NetBeans 7.x or Eclipse Pulsar
- Symbian Belle SDK
  or Series 40 Nokia 6212 NFC SDK

Tested on: 
- Nokia C7-00 with Symbian Anna and Belle
- Nokia 701 with Symbian Belle


CHANGE HISTORY
--------------------------------------------------------------------------------

8.0 Raw Mifare reading and logging to file.
    Raw Mifare writing based on newest saved file.
	Created interface class for logging and user feedback.
	Separated Form implementation from MIDlet code.
	UI operating mode selector now always in popup mode.
	Additionally logs tag information in a text field on the screen.
	Removed ".php" file extension from geo tags link on nfcinteractor.com.
	Improved code comments.
7.0 Renamed to Nfc Creator (new version of Nfc Interactor is based on Qt).
    Option to write tags with NfcInteractor.com maps redirection link.
6.2 Added support for writing vCalendar tags
6.1 Added feature to clone tags
6.0 Improved UI with instructions and slim popup-style operation mode list when in a write operation mode.
    Additional input field to specify text tag language from the UI.
5.3 Support for GEO URL records
    Support for Annotated URL messages
5.2 Selection of image to write, additional small GIF sample image.
5.1 New feature to write a combination tag type (custom record + URI record)
5.0 Refactoring to move NFC functionality into separate NfcManager class.
    Checks for NFC support at application startup. If the Nokia C7 without NFC is detected, a firmware update is recommended.
4.0 Added support for sms records and custom records. Code improvements.
1.0 First version


RELATED DOCUMENTATION
-------------------------------------------------------------------------------

Project page
http://www.nfcinteractor.com/apps/nfccreator/

NFC 
http://www.developer.nokia.com/Develop/NFC/

Java ME Development
http://www.developer.nokia.com/Develop/Java/

