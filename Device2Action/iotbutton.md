# IoT Button

In this tutorial, we will try to connect ReButton with Azure IoT Central and integrate with Power Automate to provide different IoT solutions.

# About ReButton
Build IoT solutions with IoT Button!

Seeed [ReButton](https://seeedjp.github.io/ReButton/) is a developer device for simple trigger actions, supporting multiple clicks and long press.
In addition, you can connect Seeed Grove sensors to add more data points.

1. When you push ReButton, it will power up and connect to Internet via pre-configured Wi-Fi.
2. ReButton will receive Device Twin changes from pre-configured Azure IoT Central or Azure IoT Hub.
3. ReButton will send Device to Cloud Message to pre-configured Azure IoT Central or Azure IoT Hub.
4. After D2C message is sent, ReButton will shutdown.

![](images/1.png)

Note: Part of tutorial based on [Docs for ReButton](https://seeedjp.github.io/ReButton/) and [IoT Central Documentation](https://docs.microsoft.com/en-us/azure/iot-central/) with the update of Azure IoT Central V3.

# Prerequisites
## Join the Microsoft 365 Developer Program
1. Goto [Microsoft 365 Dev Center](https://developer.microsoft.com/en-us/microsoft-365/dev-program) and click ```Join Now```

<img src="images/p-1.png" alt="Join Microsoft 365 Dev Program" width="500"/>

2. Login with your personal Microsoft account, you could create one if you do not have Microsoft account.

<img src="images/p-2.png" alt="Join Microsoft 365 Dev Program" width="300"/>

2.1 If you see this message, your account may missing some information, mostly will be the full name of the account.

<img src="images/p-3.png" alt="Join Microsoft 365 Dev Program" width="300"/>

2.2 Click the top-right corner to view your account information and click ```Add your name```.

<img src="images/p-4.png" alt="Join Microsoft 365 Dev Program" width="300"/>

2.3 Fill in your first name and last name, then click ```Save```, sign out and login agin at [Microsoft 365 Dev Center](https://developer.microsoft.com/en-us/microsoft-365/dev-program) to continue.

<img src="images/p-5.png" alt="Join Microsoft 365 Dev Program" width="500"/>

3. Follow the instructions and complete all the fields needed.

<img src="images/p-6.png" alt="Join Microsoft 365 Dev Program" height="250"/> <img src="images/p-7.png" alt="Join Microsoft 365 Dev Program" height="250"/>

4. Click ```SET UP E5 SUBSCRIPTION```

<img src="images/p-8.png" alt="Join Microsoft 365 Dev Program" width="500"/>

5. Fill in the information, for username will suggest "admin", for domain please choose a domain name which is not yet be chosen by anyone. You will create an account ```admin@yourdomain.onmicrosoft.com```, we will use this account for following labs and tutorials, so keep your password and account in safe. Click ```Continue``` and add your phone number for verification.

<img src="images/p-9.png" alt="Join Microsoft 365 Dev Program" width="250"/>

6. You have successfully created your Microsoft 365 developer account with E5 subscription, to know more about E5 subscription please visit [this link](https://www.microsoft.com/en-us/microsoft-365/enterprise/e5).

<img src="images/p-10.png" alt="Join Microsoft 365 Dev Program" width="250"/>

### Reference
- [Welcome to the Microsoft 365 Developer Program](https://docs.microsoft.com/en-us/office/developer-program/microsoft-365-developer-program)

- [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/en-us/office/developer-program/microsoft-365-developer-program-get-started)

---

## Redeem the Azure Pass
After created the ```onmicrosoft.com``` account, we need an active subscription for creating the IoT Central in Azure.

1. Visit [Azure Pass](https://www.microsoftazurepass.com/) website, click ```Start``` and login with your ```onmicrosoft.com``` account.

2. Confirm your email address is correct, then click ```Confirm``` and enter your Azure Pass promotion code, click ```Claim Promo Code```.

<img src="images/r-1.png" alt="IoT Button Tutorial" width="500"/>

3. Follow the instruction and fill in the information, you will be redirected to the [Azure Portal](https://portal.azure.com/).

# Getting Started
## Step 1 - Create IoT Central

1. Sign in [Azure Portal](https://portal.azure.com/)
2. Click ```Create a resource``` and search ```IoT Central Application```

<img src="images/13.PNG" alt="IoT Button Tutorial" width="500"/>

3. Create ```IoT Central Application```

<img src="images/14.PNG" alt="IoT Button Tutorial" width="500"/>

4. Fill in ```resource name```, ```Application URL```, and set template as ```Custom Application```. Pricing plan can choose either ```Standard 1``` or ```Standard 2```. Then click ```create```.

<img src="images/15.PNG" alt="IoT Button Tutorial" width="400"/>

## Step 2 - Create ReButton Template

1. Access ```IoT Application URL``` and login with your Microsoft Account.
2. Navigate to the Device Templates page.
3. Create the ReButton device temmplate by clicking the ```+ New``` button.
4. Scroll down and find "ReButton", select it and click ```Next: Review```.
5. Confirm the information and click ```Create```.

<img src="images/i-01.png" alt="IoT Button Tutorial" width="700"/>

## Step 3 - Create Device Template View

1. In "ReButton" template, click "Overview" under "Views".
2. In "Edit view", you can delete the previous blocks on left hand side.

<img src="images/i-02.png" alt="IoT Button Tutorial" width="700"/>

3. In "Telemetry", select "Action number", then click ```Add tile```. Repeat the step and select "Battery voltage", "Message" respectively. 

<img src="images/i-03.png" alt="IoT Button Tutorial" width="200"/>

4. After editing, click ```Save``` and ```Publish```, confirm the publish information and click ```Publish``` again.

<img src="images/i-04.png" alt="IoT Button Tutorial" width="500"/>

## Step 4 - Create Device

1. Create a device in your ReButton template, in "Devices" select the "ReButton" template and click ```+ New```. Then confirm the information and click ```Create```.

<img src="images/i-05.png" alt="IoT Button Tutorial" width="500"/>

2. Click ```Connect``` on Top Right corner of Azure IoT Central page.

<img src="images/i-06.png" alt="IoT Button Tutorial" width="600"/>

3. Copy 3 values.
```Scope ID```
```Device ID```
```Primary Key```

<img src="images/9.png" alt="IoT Button Tutorial" width="400"/>

## Step 5 - Getting access to IoT button

Use AP Mode (Access Point Mode) to configure IoT button. **To avoid battery drain, IoT button will automatically shutdown in 10 minutes, at AP mode.** So that we recommend you to setup IoT Hub or IoT Central, first.

1. **Hold button until RGB LED turns into White.**
RGB LED will start with Blue, Yellow, Cyan, then White. This will take about 10 seconds.

2. **Release button and confirm IoT button is in AP mode.**
When IoT button successfully boots into AP Mode, RGB LED will blink in White.

3. **Connect to AP.**
Look for Wi-Fi Access Point ```AZB-xxxxxxxxxxxx``` and connect to it from your PC.
(```xxxxxxxxxxxx``` is MAC address of your IoT button Wi-Fi.)

<img src="images/2.png" alt="IoT Button Tutorial" width="300"/>

Use a Web Browser to access IoT button - Home at ```http://192.168.0.1.```

<img src="images/3.png" alt="IoT Button Tutorial" width="400"/>

## Step 6 - Wi-Fi Configuration

Configure Wi-Fi settings to connect to Internet.

1. Click ```Wi-Fi``` at IoT button - Home.

<img src="images/4.png" alt="IoT Button Tutorial" width="400"/>

2. Select your Wi-Fi Access Point from ```Wi-Fi SSID``` list.
If you do not see your Access Point, refresh browser.
3. Enter ```Wi-Fi Passphrase``` for your Wi-Fi AP.
4. (Optional) In case you would like to use specific Internet ```Time Server```, enter FQDN to Time Server.
Default Internet Time Server is pool.ntp.org -> cn.pool.ntp.org -> europe.pool.ntp.org -> asia.pool.ntp.org -> oceania.pool.ntp.org .

5. Click ```Save```.

## Step 7 - Azure IoT Central Configuration

1. Browse to IoT button - Home page then click ```Azure IoT Central```.
2. Enter ```Scope ID```, ```Device ID```, ```SAS Key``` from Azure IoT Central.
3. Click ```Save```.

<img src="images/10.png" alt="IoT Button Tutorial" width="400"/>

## Step 8 - Power Off

Exit AP Mode and power off IoT button.

Click ```Shutdown``` button.

## Step 9 - Create Excel table

1. Go to [OneDrive](https://onedrive.live.com/) and create Excel workbook

<img src="images/11.PNG" alt="IoT Button Tutorial" width="400"/>

2. Follow the column name below

|Device|Action|Time|
|-|-| -|

3. Click ```Format as Table```

<img src="images/12.PNG" alt="IoT Button Tutorial" width="600"/>


## Step 10 - Create event-based rule

1. Go back to ```IoT Application URL```.

2. To add a new event-based rule to your application, in the left navigation menu, select "Rules" and click ```+New```.

<img src="images/i-07.png" alt="IoT Button Tutorial" width="250"/>

3. Give a name to this rule, "Device template" select ```ReButton```. In "Conditions", "Telemetry" select ```Message```, "Operator" choose ```Contains``` and "Value" select ```Any```. When every message appears will be triggering this rule to run.

4. Confirm the information and click ```Save```.

<img src="images/i-08.png" alt="IoT Button Tutorial" width="700"/>

## Step 11 - Add Microsoft Power Automate as Action

1. To create flow, in [Power Automate](https://asia.flow.microsoft.com/en-us/), goto "Create" and click ```Instant flow```.

<img src="images/create.png" alt="Create flow" width="500"/>

2. A "Build an instant flow" box will show, click ```skip```.

<img src="images/create2.png" alt="skip flow" width="500"/>

3. Choose, the trigger, in search bar, type ```flow```, select the trigger ```Manually trigger a flow```.

4. Search ```IoT Central``` and click ```When a rule is fired```. (Note: Choose "Azure IoT Central V3")

<img src="images/i-09.png" alt="IoT Button tutorial" width="500"/>

5. You may require to start the free trial, click ```Start trial``` and login with your ```onmicrosoft.com``` account.

<img src="images/i-10.png" alt="IoT Button tutorial" width="400"/>

6. Click the dropdown and select the ```Application``` and ```Rule```

<img src="images/i-11.png" alt="IoT Button tutorial" width="500"/>

7. Click ```+ New step``` and search ```Excel```. Select ```Excel Online (Business)```, add an action ```Add a row in a table```.

<img src="images/i-12.png" alt="IoT Button tutorial" width="500"/>

6. Fill in the information below:
- Device: Device Name
- Action: PushButton Message
- Time: Webhook Timespamp 

You may find the information in "Dynamic content", the field under "When a rule is fired".

<img src="images/i-13.png" alt="IoT Button tutorial" width="500"/>

7. Click ```Save``` on the top right corner and test your flow by pressing the ReButton.

<img src="images/i-14.png" alt="IoT Button tutorial" width="700"/>