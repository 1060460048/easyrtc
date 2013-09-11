EasyRTC: Change Log
===================


v0.9.0a (note, alpha means alpha... please let us know of issues.)
-------
New Features:
 * Server/API - Rooms. An EasyRTC application can have multiple rooms. A user can be in one or more rooms at the same time. Users can only see other users in the same room. If no room is provided, connections will be entered into a room named `default`.
 * Server/API - Custom authentication method. Username / Credential can be provided. Username is broadcast to other authenticated users, so it may be used by apps.  
 * Server/API - Groups. A user can be in one or more groups. This is intended to be set via the authtication method.   
 * Server - Reworked to be node.js module. (BIGGEST NEW FEATURE)
 * Server - Many new server events. Ths is intended to be the new way for developers in interect with EasyRTC server.
 * Documentation - New documentation for internal EasyRTC command messages which highlight how the API and server communicate to each other.
Changes:
 * Server/API - Delta lists. When the online list is changed, only the changed connections are broadcast. This should reduce bandwidth and improve scalability.
 * Server - No longer includes modules for express, socket.io. These must now be included in your server app. (See our server examples)
 * Server - No longer uses the winston module for logging. The default listener logs to the console. This can be easily overruled by setting your own `log` listener.   
Fixes:
Upgrade Note:
 * This is a major release which will require existing installations to carefully upgrade.

v0.8.1b
-------
New Features:
Changes:
 * Server - Moved API files to the /api/ folder thus cleaning up the /static/. API files are publicly linked using /easyrtc/easyrtc.js and /easyrtc/easyrtc.css. For transitional purposes, the old public file locations are still accessible.
 * Server/Api - Renamed easyRTCcmd socket message type to easyrtcCmd. Should have no outside effect. 

Fixes:
 * API - Firefox - Strips TURN servers from ICE config if they are present. Firefox doesn't currently handle TURN servers well.
 * API - Added one second delay to getUserMedia call to try and correct some page loading problems.

v0.8.0
------

New Features:

 * API - Added support for grabbing the screen as the local media source. Currently this only works in Canary, and causes the browser to crash if you try to use it in a peer connection. 
 * API - Added support for grabbing video at high-definition instead of the default standard definition. Warning: the browser may cheat and give you a lower resolution than you asked for that has the desired aspect ratio.
 * API - Added a number of callbacks to the initManaged method to support richer interactions with the client.
 * API - Added a cleaner error reporting mechanism. The code now calls showError(errCode, errText) to report an error. showError will in turn call onError (which you can still override).
 * API - Added support for calls that get cancelled (by the initiator) before they are accepted or rejected.
 * API - Added a method to query the status of a peer to peer call.
 * API - Added the dontAddCloseButtons method.
 * API - When initMediaSource is called, the API creates a temporary video object to determine the pixel dimensions of the local camera. Until this version, that video object wasn't being explicitly destroyed, which resulted in a feedback shriek in Firefox and the most recent versions of Chrome. The temporary video object is now being destroyed.
 * Server - Added socket.io options to config.js. Note that socketIoClientGzipEnabled is now false by default as gzip causes issues on some servers (often Windows).
 * Demos - Added a screen sending and screen receiving demo. These tend to crash the browser at this point. Hopefully Google will get that feature working properly again.
 * Demos - Added a multiperson tablet-oriented chat demo that runs very nicely on your Android devices.
 * Documentation - Moved the client API documentation from mark-down format to jsDoc and added inline examples. Check out the easyRTC.html file in the docs directory. The easyrtcjs.html file is a helper file that shouldn't be looked at directly.

Changes:
 * Demos - In demos which show the local media stream as both audio and video (as a mirror), the video object with the local media stream is muted and given a volume of 0.
 * Demos - Removed references to Firefox requiring flags
 * Server - Version bumps for node modules express (3.2.x) and winston (0.7.x).
 * Server - Added additional public stun servers
 
Fixes:
 * API - The mozRTCSessionDescription object didn't used to work properly in Firefox. Now it appears to be required.
 * API - When initMediaSource is called, the API creates a temporary video object to determine the pixel dimensions of the local camera. Until this version, that video object wasn't being explicitly destroyed, which resulted in a feedback shriek in Firefox and the most recent versions of Chrome. The temporary video object is now being destroyed.   


v0.7.0
------

New Features:

 * API - Added initial support for Data Channels.
 * API - Added more debugging output and provided a means to control it through the easyRTC.debugPrinter variable and easyRTC.enableDebug function.
 * API - Added code to log application state (WRT webrtc) to the server.
 * API - New function setSocketUrl() to point to web socket server. Allows website to be hosted using a seperate server (suchs as Apache). The default remains for the easyRTC server to function as both the web and socket server.
 * API - Support for hanging up on calls still being set up - on the initiating side by extending the easyRTC.hangup function, and on the receiving side by adding the easyRTC.setCallCancelled callback setter.
 * API - Added easyrtc.getConnectStatus function to get the state of a connection to a peer.
 * Server - SSL support for web and socket server including non-ssl forwarding.
 * Server - Logging features. Both console and file based logging with fine-grained configuration.
 * Server - Checks if required modules are installed at start.
 * Demos - Added demos for data channel messaging and data channel file sharing.
 * Documentation - Server configuration.
 * Documentation - This changelog :)

Changes:

 * API - The callSuccessCB argument to easyRTC.call now has a second argument, which can be either 'audiovideo' or 'datachannel'. The callSuccessCB function may be get called twice if the peer connection is using data channels as well as audio or video.
 * API - Fixed easyRTC.connect so that you can reconnect after calling disconnect.
 * Server - Websocket 'onMessage' section moved to external function for easier editing.
 * Server - Much of the general server code moved to external functions.
 * Demos - Various visual html fixes and changes.
 * Demos - Removed unneeded CSS for selfVideo tag from demo_audio_only.html, changed callerVideo id to callerAudio id, removed selfVideo tag and javascript which referenced it, changed a variable name from 'video' to 'audio'.

Fixes:

 * Server - Bad link to a stun server.


v0.6.0
------

New Features:

 * Demo landing page which includes links and compatibility chart.
 * Option to disable demos in config.js.
 * powered_by_easyrtc.png image. Please use it to promote the project.

Changes:

 * change Split live demos to their own folder.
 * change Major graphical upgrade for demos and landing page.

v0.5.0
------
 * Initial release.