APL Attachment Validation plugin is a FilterAPI plugin.  If properly installed and configured on your Remedy server, it provides
the ability to validate your attachment before it gets saved into a record.  Initially the only validation that is possible is virus scan.
The plugin provides 3 possible outputs.

1 - Success - The plugin runs into no errors or warnings, it returns nothing back, no message, or attachment
2 - Warning - The plugin detects configured warning configuration, it puts a Warning: message in the log, and grabs the attachment from the filesystem and re-attaches it to the record
3 - Error - The plugin is either unable to run the specified process, or it finds the error text specified, the plugin throws an error

To install the plugin and configure the server to utilize it, you'll need to perform the following steps

1: Modify the ar.cfg/ar.conf file and add the value from the template folder, 
   ensuring the server name/port are accurate for your environment
2: Modify the pluginsvr_config.xml in InstallDir\pluginsvr folder to include the 
   content in the template, ensuring that you don't add it inside another plugin-set
   Modify the 'userdefined' section as appropriate for your program/arguments/error/warning texts
3: Optionally import the Remedy Def file, this exists solely to ensure that the plugin is configured
   properly and accessible to the Remedy server
4: Go into the Server Information console, Attachment Security tab and put 'APL.ARF.ATTACHMENTVALIDATION' (without the ')
   in the Attachment Validation Plugin section
5: Copy APLAttachmentValidationPlugin.jar to the InstallDir\pluginsvr folder
6: Copy VirusScan.bat to the \temp folder (Or wherever you have configured the scanner to run) 
7: Restart your Remedy server

The test plugin form is there just to test that the plugin is available to the server...the use beyond that is limited, the true test is to
verify if in scenarios of an error occurring, that the AR Server doesn't attach the specified file.

The command that's executed should be configured to return only the text that you want the plugin to evaluate

It is not advisable to have the output directory be the same directory as your program is in, otherwise attachments being saved to the server
could potentially overwrite your files

For the virusParams configuration, if the value of $FILENAME$ appears in the param, that will automatically be replaced with the actual file name, any other value will be passed as defined