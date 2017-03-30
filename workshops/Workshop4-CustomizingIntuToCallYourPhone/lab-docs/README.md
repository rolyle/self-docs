# Workshop 4: Customizing Intu to call your phone

In this workshop, you will configure Intu's telephony plan to have Intu call your phone by using the Nexmo Cloud Communications API. 

A plan is a set of preconditions, a set of actions, and a set of postconditions to address a given goal. You'll learn more about the importance of plans and how they work later in this workshop.

**Before you begin:** You must have a Mac or Windows laptop, and you must have completed Workshop 1: Say Hello!. You will notice that Intu and Self are used interchangeably. Self is the technical name for Intu.

Complete the following tasks:

1. [Signing up for a Nexmo account](#signing-up-for-a-nexmo-account)
2. [Getting your Nexmo credentials](#getting-your-nexmo-credentials)
3. [Adding the telephony service to Intu](#adding-the-telephony-service-to-Intu)
4. [Understanding plans](#understanding-plans)
5. [Modifying plans to have the telephony service call your phone number](#modifying-plans-to-have-the-telephony-service-call-your-phone-number)

## 1. <a name="signing-up-for-a-nexmo-account">Signing up for a Nexmo account</a>

1. [Sign up for a Nexmo account](https://dashboard.nexmo.com/sign-up)
  
## 2. <a name="getting-your-nexmo-credentials">Getting your Nexmo credentials</a>

1. On the [Nexmo dashboard](https://dashboard.nexmo.com/), click the top right drop down menu (the one with your name next to it) to expand the account menu.

2. Click **Settings**.

3. Copy the values of the **API key** and **API Secret** parameters, and paste them into a new text file using your favourite text editor.

4. You will need to pay for minutes on the Nexmo service. This will allow your account to allow to make calls using the API key/secret you copied above.

## 3. <a name="adding-the-telephony-service-to-Intu">Adding the telephony service to Intu</a>

1. [Log in to the Intu Gateway](https://rg-gateway.mybluemix.net/).

2. Click **MANAGE** on the left side of the page, and click **Services**.
3. In the **Filter By** fields, select your Organization and Group.
4. Click **Add Service**.
5. Specify your Nexmo credentials.
  1. In the **Service Name** field, specify **TelephonyV1**.
  2. In the **User ID** field, specify the **API key** value from your text file.
  3. In the **Password** field, specify the **API Secret** value from your text file.
  4. In the **Service Endpoint** field, specify: **ws://nexmo-watson.mybluemix.net/ws-embodiment**
6. Click the blue **Add** box.
7. If you currently have Intu already running, stop it to enable the Telephony service to automatically provision a US phone number for your device.

## 4. <a name="understanding-plans">Understanding plans</a>

Plans are the primary driving factor in how Intu can accomplish goals. For example, you can preconfigure a plan that tells Intu how to act in a certain situation without any code changes.

Plans contain two major components:

  * **Preconditions**: A set of conditions that must be met for a particular plan to begin execution.
  
  * **Actions**: After all preconditions are met, a series of actions are taken to to complete a plan. Intu supports two types of actions: CreateAction, which creates a blackboard object and places it on the blackboard, and UseSkillAction, which tells Intu to execute a specified skill.

All plans are loaded when Intu starts. When a goal object is placed on the blackboard, the GoalAgent finds the best possible plan, executes the plan, and establishes whether that goal was completed successfully (i.e., the plan finished with no action failures) or failed (i.e., no plan was found to carry out execution).

## 5. <a name="modifying-plans-to-have-the-telephony-service-call-your-phone-number">Modifying plans to have the Telephony service call your phone number</a>

1. Locate the **plans** directory where you will be modifying your plan. If you used the Intu INSTALLER (from the Intu Gateway) to install Intu in Workshop 1, the path is:

	* **For Mac users:** /Applications/IBM/Self/latest/etc/shared/plans
	
	* **For Windows users:** C:\Users\username\AppData\LocalLow\IBM\Self\INTU_VERSION\etc\shared\plans
	
	*Note for Windows Users:* replace *INTU_VERSION* with the latest version of Intu you installed. You can look in the *Self* directory to see which one is the newest.

2.  Open the `default.json` file in the **plans** directory using your favorite text editor (if on Mac, refrain from using TextEdit as it will format text and cause the plan not to be found. On Windows, it is preferable to use Notepad/Wordpad and on Mac it is preferable to use Sublime or nano/vim).

3. Browse through the different plans and notice how plans can have different preconditions based on the data that is represented.
For example, look at the first plan called `"dialog_answer"`. It contains a set of preconditions (the key is `"m_PreConditions"`) that must be answered for that plan to execute. The first parameter, the array with the key `"m_Params"`, in that precondition states that the data being analyzed must have the format `"{"answer" : {"response" : ["some value"] }, }"`, where the array in response must not be equal to null, while the second precondition states the response array must not have a key of `"id"` in the response array.

4. Search for a plan called `"outgoing_call"`, and change the value of `"m_ToNumber"` in the second action to your phone number (Be sure to include the country code first, e.g. **15551231234**). Now, look at the actions for this plan. The first action will have Intu `"Dialing"`, while the second action will carry out the execution to call the number specified.

5. Run Intu. 

	1. If you have closed your **Intu Manager**, navigate to the directory where you installed it in Workshop 1, and open Intu Manager.
	2. Login with your Bluemix credentials. 
	3. Once logged in, select your Organization and Group.
	4. Verify that you can see the device on which you installed Intu. 
	5. Click on the on/off toggle to restart your device.
	6. The status icon should turn green and a new Terminal/command prompt window will open in the background as Intu starts running.

6. Ask Intu "Can you call me?". When your phone rings, answer it. Have a conversation with Intu. Say "Tell me a joke". You should hear a joke. You can continue to talk or hang up.

## Reminder: Update services within 30 days of registering on the Gateway

If you want to test Intu after the trial period ends, you must create your own instances of these services and configure Intu to use them.

### A. Creating instances of Watson services
To use Intu, you need operational instances of the following services in Bluemix: Conversation, Weather Company Data, Speech to Text, and Text to Speech.

**Pro tip:** As you complete this task, you'll receive credentials for each service instance, and you'll need these credentials later. Open a new file in your favorite text editor and create a section for each service so that you can temporarily store its credentials.

1. On the Bluemix dashboard, click **Catalog** in the top right navigation bar.

2. In the All Categories menu on the left, under Services, click on **Watson**.
3. Create an instance of the Conversation service.
  1. Click the **Conversation** tile.
  2. Keep all the default values, and click **Create**.
  3. Click the **Service Credentials** tab.
  4. Click **View Credentials** for the new Conversation service instance.
  5. Copy the values for your password and username and paste them into a new text file in your favourite text editor.
  6. Click the **<--Watson** breadcrumb near the top left (directly above your Conversation service name). The list of your service instances is displayed.
  7. Add the next service instance by clicking the **Create Watson** **+** button. The Watson service catalog is displayed.
4. Create instances of the Weather Company Data, Speech to Text, and Text to Speech services by repeating the same substeps 1 - 7 that you completed to create the Conversation service instance.

### B. Configuring Intu to use your service instances

To configure Intu to use your instances of these Watson services, log in to to the [Intu Gateway](https://rg-gateway.mybluemix.net/) and complete the following steps:

1. Click on **MANAGE** on the left hand side navigation bar, and select **Services**. 

2. Select your Organization and Group in the top Filter by menu, if not already selected.
3. For your instances of the Conversation, Weather Company Data, Speech to Text, and Text to Speech services, click **Edit**, and specify the user ID and password (saved in your text file in the previous section **Creating instances of Watson services**), and click **Save**.
4. To configure your instance of **Conversation**, navigate to **DOWNLOADS** on the left of your Intu Gateway browser page, download the **Intu Starter Kit**, and follow the instructions in the `readme.txt` file. Alternatively, go to the instructions for **Workshop 2**, and follow the steps in: **1. Setting up the Conversation service**.

**Important:** Do not change the service endpoint unless you are an enterprise user.
