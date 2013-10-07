asterisk-originate-2
====================

This is an Enhanced version of app originate for Asterisk 11.5+ which replaces the stock Asterisk Originate dial plan application.  This enhanced version has been extended to support passing Caller Line ID name and number as well as any channel variables.  The goal is to make the Originate dial plan application provide all of the functionality currently found in the Asterisk Manager Interface Originate command.

To use the new function, you must pass the following variables:

	•	tech_data - Channel technology and data for creating the outbound channel. For example, SIP/1234.
	•	type - This should be 'app' or 'exten', depending on whether the outbound channel should be connected to an application or extension.
	•	arg1 - If the type is 'app', then this is the application name. If the type is 'exten', then this is the context that the channel will be sent to.
	•	arg2 - If the type is 'app', then this is the data passed as arguments to the application. If the type is 'exten', then this is the extension that the channel will be sent to.
	•	arg3 - If the type is 'exten', then this is the priority that the channel is sent to. If the type is 'app', then this parameter is ignored.
	•	timeout - Timeout in seconds. Default is 30 seconds.
	•	cid_num - This is the CallerID Number to use for the call
	•	cid_name - This is the CallerID Name to use for the call
	•	vars - If you need to pass any variables, this is the place to do it.

For example, to originate a call to 4165551212 using the CLID Name of "Test" and CLID Number of "4165551313" you would call the following from the dial plan:

exten => _X.,n,Originate(SIP/${NUM_TO_DIAL}@TARGET,exten,context,extension,1,30,"Test", "4165551313")

If you need to pass additional variables they can be added as the last variable, for example:

exten => _X.,n,Originate(SIP/${NUM_TO_DIAL}@TARGET,exten,context,extension,1,30,"Test", "4165551313","MY_VAR=${MY_VAR})

  
