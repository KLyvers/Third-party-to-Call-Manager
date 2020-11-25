# Axis A8105-E door station with video

Verified working with CUCM 12.5 with video calling to Jabber 12.9 and 9971 series endpoints

The biggest issue was that the device did not assume to send the call to the registrar server. The `To SIP address:` needed to include the CUCM server DNS/IP. **Shoutout to Axis support for the three hour call to help figure this out.**

## CUCM configuration

Build a Phone security profile to allow for digest authentication.

1. Navigate to:  
**System -> Security -> Phone Security Profile**

2. Add New, pick `Third-party SIP Device (Advanced)`

3. Add a useful name for the `Name*` field  
example: *Axis SIP Device Security Profile*

![Profile Settings snip](/images/CUCM-SecProfile-Axis-DigestAuth.jpg)

4. Click `Save` to create the profile.


Create a local user account the device will authenticate with.

1. Navigate to:  
**User Management -> End user**

2. Add New and populate required fields. The `Last name*` does not effect configuration but shows up in reports/exports so make it useful.

`User ID*` enter *a8004*

`Digest Credentials` will be what the device uses to authenticate to CUCM. My setup is Alphanumeric with no capital letters.

`Confirm Digest Credentials` re-enter above

3. Click `Save` to create the End user

Create the device

1. Navigate to:  
**Device -> Phone**

2. Click _Add New_ then pick `Third-party SIP Device (Advanced)` then click _Next_

3. In the Device Information box configure the device based on your use case/system setup.  
 `MAC Address*` this should be the actual MAC address of your device. Do not add _SEP_ or other common prefixes here.  
 `Phone Button Template` pick _Third-party SIP Device (Advanced)   
![Device Information snip](/images/CUCM-DeviceInfo-Axis.jpg)

4. In the Protocol Specific Information box  
 `Device Security Profile*` set to the security profile made earlier. Example: *Axis SIP Device Security Profile* from dropdown  
 `SIP Profile*` select *Standard SIP Profile* from dropdown  
 `Digest User` select the End User created earlier from the dropdown. Example: *a8004*  
![Protocol Specific snip](/images/CUCM-ProtocolInfo-Axis.jpg)


5. Click `Save` then `Apply Configuration` the Apply Configuration popup will note that this will drop calls in progress.

Configure line/Directory Number on the device

1. Click on `Line [1] - Add a new DN  
In our example we will configure with extension 568, however your number plan may be different.
