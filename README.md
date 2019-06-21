# PyHSS

Python Home Subscriber Server implementing basic Diameter / 3GPP S6a Interfaces.


## Introduction
PyHSS is a simple Home Subscriber Server (HSS) implementation written in Python.
HSS communication is via the [DIAMETER](https://tools.ietf.org/html/rfc6733) protocol, with some extensions defined by 3GPP.


## Implemented Responses 
 * Capabilities Exchange Answer (CEA)
 * Device Watchdog Answer (DWA)
 * Disconnect Peer Answer (DPA)

 
## Structure
The file *hss.py* runs a simple Sockets based listener to field Diameter requests.
It relies on the *diameter.py* file to:
 * Decode incoming packets (Requests)(Returns AVPs as an array, called *avp*, and a Dict containing the packet variables (called *packet_vars*)
 * Generates responses (Answer messages) to Requests (when provided with the AVP and packet_vars of the original Request)
 * Generates Requests to send to other peers

 
## Extending
To implement a new response is simply a matter of adding the *packet_vars['command_code']* and *packet_vars['ApplicationId']* to the if/elif loop in *hss.py*.
You can then access each of it's AVPs from the *avp* array, and the packet variables from the dictionary called *packet_vars*.
To add a new response you'd edit *diameter.py* and add a new function called Answer_YOURCOMMANDCODE, and build the AVPs and packet variables as required.


## Contact
Any contributions welcome, this was written to fix a problem (VoLTE implementation on an EPC with a HSS that couldn't be easily customized), but will hopefully be of some use to the community.

You can contact me at nick (at) nickvsnetworking.com or via my blog at [nickvsnetworking.com](https://nickvsnetworking.com)