## Standalone Emergency Alerting CAP Player

OBPlayer can be set up as a standalone CAP alert broadcaster. Install OBPlayer in-line with your broadcast audio\video chain and it will automatically interrupt the regular broadcast when it receives a valid CAP-CP formated alert. Use the DIY RS232 GPIO to trigger relays to cut into scheduled programming.

Start OBPlayer and login to Dashboard

__Sync/Media Tab__

Uncheck 'Enable Scheduler', and 'Enable Fallback Media Player'. This disables all other media settings.

__Audio/Visualizations Tab__

Audio Output "Auto Detect" Defaults to Pulse audio

Audio Input "Auto Detect" Defaults to Pulse audio

Only change these audio settings if you know what you are doing.

__Video/Image Tab__

Leave this unchecked when using in a radio\audio application

__Emergency Alerts Tab__

Enable Emergency Alerts

__Voices__

Select Primary and Secondary languages in order preference with accompanying language voice. Use a voice starting with 'mb-' if mbrola voices are installed.

__SGC Code__ 

Enter SGC code for your region availble from [Statistic Canada](https://www.statcan.gc.ca/en/subjects/standard/sgc/2011/index) or [Standard_Geographical_Classification_code](http://en.wikipedia.org/wiki/Standard_Geographical_Classification_code_%28Canada%29). More than one SGC can be entered, separated by commas.

* Alert Repeat Duration = Default 30 minutes.

* NAAD Streams. Enter in 2 of your Countries NAAD Streams and Archive URL

* Truncate long messages. Default = No Emergency messages should be issued by Pelmorex with all the concise info contained in first line. Selecting this, could mean reading out the entire message with unrecognizable TTS translations of websites and URLs. The long message might go on several minutes.

* Play Moderate and Advisory Alerts. Check if you want these to play. Default = No

* Play Test Alerts. Enable this for playing test alerts. Default = No Normally the play test messages option is for playing messages marked as Test, which normally shouldn't be played to the public. The test messages for public distribution do not have the status value "Test". They are like normal alerts

__On board CAP Alert Testing__

1. Simple Test. Generates an internal CAP-CP formated message and plays using TTS

2. Embedded Audio Test. Generates an internal CAP-CP message and plays a supplied MP3 file instead of TTS.

3. External Audio Test. Generates an internal CAP-CP alert message, fetches and plays a test MP3 file from Pelmorex.

4. Embedded Audio and Image Test. Generates an internal CAP-CP test the displays a JPG image and plays audio recording.

__NOTE__ _English and French are presently the only supported language for on board testing with Audio and Visual alerting_

__Configuring Audio Line In__

Status Tab VU Meter shows levels of line in source signal

When using USB/XLR adapter, disable on board audio from BIOS. Go to Pulse Audio Settings>Configuration On board audio = "Off"

__Monitoring Dual NAAD Feeds with Duplicates__

Monitoring two NAAD streams and the same alert comes in on both streams. If by chance a CAP alert came in on different feeds, the alert would be treated as one alert. The player is smart enough to detect and not play duplicates.

__GPIO Trigger with RS-232 DTR on CAP-CP Alerts__

When enabled and a matching CAP-CP message is broadcast, an alert cycle starts, the serial port will be opened and the DTR line will be set. After the alert cycle has completed, the DTR line will be cleared and a relay will be closed.

Install this package in order to use the RS-232 feature.

~~~~
python-serial
~~~~

__Lead-In Delay (in seconds)__"

This is the number of seconds of silence that will be inserted at the beginning of each alert cycle before the first alert starts playing, but after the DTR/icecast stream notifies that an alert cycle has started. The default is 1 second. Always leave it at 1 or greater. Setting this to 5 or so seconds will give time for buffering to occur.

__Trigger RS-232 DTR on Alerts__

When checked, will show the "RS-232 Device Filename" option. The device filename should be something like /dev/ttyS0, or /dev/ttyUSB0 if using a USB-to-Serial adapter. For initial setup, disable all RS-232 ports so there is only one available.

__Trigger Icecast Stream on Alerts__

Will start and stop the icecast streamer module (in the streaming tab) the same as the serial port. In addition to this setting, you must also uncheck the "Play Stream on Startup" option on the streaming tab, or else the streamer will start playing when obplayer starts.

__Add Dialout Group__

~~~~
whoami output will be your username
~~~~

__Serial ports on Linux__

User account needs to have access to the serial port and be a member of the dialout group.

~~~~
sudo usermod -a -G dialout <username>
~~~~

Log out / log back in (or reboot). User now has access to the serial port and all its control lines.

__Check group membership__

~~~~
groups <username> 
~~~~

If 'dialout' appears in the output you are in the dialout group. 
