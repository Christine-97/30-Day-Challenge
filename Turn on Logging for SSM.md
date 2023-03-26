Turn on logging for the Session Manager plugin (Windows)
Locate the seelog.xml.template file for the plugin.

The default location is C:\Program Files\Amazon\SessionManagerPlugin\seelog.xml.template.

Change the name of the file to seelog.xml.

Open the file and change minlevel="off" to minlevel="info" or minlevel="debug".

Note
By default, log entries about opening a data channel and reconnecting sessions are recorded at the INFO level. Data flow (packets and acknowledgement) entries are recorded at the DEBUG level.

Change other configuration options you want to modify. Options you can change include:

Debug level: You can change the debug level from formatid="fmtinfo" to outputs formatid="fmtdebug".

Log file options: You can make changes to the log file options, including where the logs are stored, with the exception of the log file names.

Important
Don't change the file names or logging won't work correctly.

<rollingfile type="size" filename="C:\Program Files\Amazon\SessionManagerPlugin\Logs\session-manager-plugin.log" maxsize="30000000" maxrolls="5"/>
<filter levels="error,critical" formatid="fmterror">
<rollingfile type="size" filename="C:\Program Files\Amazon\SessionManagerPlugin\Logs\errors.log" maxsize="10000000" maxrolls="5"/>
Save the file.
