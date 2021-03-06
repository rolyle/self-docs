#Frequently Asked Questions: Miscellaneous

###Here is a collection of some random FAQs

* Troubleshooting flow in general.
   1. Is robot turned on? Is it connected to a power supply?
   2. Does the robot have wifi connection?
   3. Is Conversation Service on gateway setup properly?
      self_dialog : It should be the workspace id for Intu dialog
      self_domain : It should be the workspace id for customized user conversation. If there is no custom workspace, DELETE it!
   4. Install Intu on local machine and test. Get the logs from the following location:
      Mac: ~/Library/Application Support/IBM/Intu Manager/Intu Manager.log
      Windows: C:\Users\{username}\AppData\LocalLow\IBM\Intu Manager\Intu Manager.log

      If there is no parent connection -> Create a new organization and re-try
      If there are 404 or 401 errors in logs for services you believe you have configured -> Check if the services configured on the gateway have correct username/ password as Bluemix
   5. After local machine installation is done, check if the topics are registered: 127.0.0.1:9443/info
   6. Check parent url to see the machine. Find the parent URL and org ID from Intu Manager.log. The url will look like `ws://xxxx`. The `ws://` would need to be replaced with `http://` while checking on browser. So the final url would be: `{URL}/info?orgid={ORG_ID}`
   7. Login to Intu Manager => select your org / group and this will populate all devices under that org / group. First device on the list will be the parent. It should turn green when it is connected. If no parent connection occurs, check the Intu Manager log. 
   8. Install Intu on Robot / RaspberryPI. If robot is not shown in Intu Manager, kill Intu instance on Robot and restart it with "-c 0 -f 0" parameters to see debug logs to check the issue.
   
* Does a normal end user need to download Intu manager + whatever the unity front end is to run? E.g: Intu manager+Watson avatar, or is it ONLY the sys admin that needs Intu manager locally?
  * Anyone can download the Intu Manager.  If you would like to install Intu onto a device, such as a robot or your own local machine, you will need to download the Intu Manager. Additionally you should download the Intu Manager if you would like to monitor devices in your organizations.

* In the config.json file, why do we need to have the services endpoints (e.g:conversation) and their credentials locally? Does the avatar not talk to the Intu manager with the Intu manager handling the services there? Also, if we change the values (endpoints/credentials) locally, does that get updated in the Intu gateway (synced)?
  * In the config.json, you only need to add your organization and group ids and bearer tokens.  Please see Workshop 7 for more details on how to run the Intu Avatar.

* When you create an organization in the gateway, are you creating a parent? Is each device registered under the same organisation a child to that parent/organization?
  * When you create an organization, a parent will be created automatically.  Each device registered to the organization is a child of the parent.

* What are different groups in the gateway? How are these used? (Are these "children"?)
  * An organization should have multiple groups if you want each device in the different groups to use different service credentials, perhaps they will use a different Conversation Workspace.  An example might be a Hotel Organization and each group has a different function within the hotel, perhaps one group is for the Front Lobby Concierge and another group is for In-Room queries.

* Is it possible to chain agents together?
  * Agents communicate through the blackboard only by design. All objects on the blackboard are derived from the IThing class.

* How do you setup Intu to have multiple users?
  * Once you create an organization, you can invite other users to join the group.  In the Gateway, navigate to the Manage -> Groups tab and you can add a user from there.

* Do you need one version of Intu on your machine for one instance of the avatar?
  * The Avatar doesn't need the Intu instance to run on the local machine. It connects using a web socket.

* Can we change the installation path?
  * Not currently.

* Does Intu install any extra files that do not reside in the installation location?
  * On windows we install everything into the **C:/Users/<user name>/AppData/LocalLow/IBM/**

* What does GetStaticRTTI() return? Do we have some API docs?
  * We implemented our own RTTI (Run time type information) rather than using the more expensive compiler based option. The GetStatisRTTI() function is invoked by a virtual function called GetRTTI() found in each class. This returns the RTTI object that defines the type, including the name of the class and it's base type. 

[Back to the index](../../README.md)
