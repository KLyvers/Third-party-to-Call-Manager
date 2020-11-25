# Axis A8105-E door station with video

Verified working with CUCM 12.5 with video calling to Jabber 12.9 and 9971 series endpoints

The biggest issue was that the device did not assume to send the call to the registrar server. The `To SIP address:` needed to include the CUCM server DNS/IP. Shoutout to Axis support for the three hour call to help figure this out.

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

Click `Save` to create the End user
