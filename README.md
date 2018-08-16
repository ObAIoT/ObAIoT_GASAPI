# ObAIoT_GASAPI
A collection of useful Google Apps Script API and web services
First of all, a Gmail verifier is present for validating if a email address is a valid Gmail.

# Setup
This library is already published as an Apps Script, making it easy to include in your project. To add it to your script, do the following in the Apps Script editor:
1. Click on the menu item "Resources > Libraries..."
In the "Add a Library" text box, enter the project key ```MSNSZfBH_WHXkkG_V3T5W5eFrpvyrbQzU``` and click the "Add" button.
Choose a version in the dropdown box (to pick the latest version).
Click the "Save" button.

# Getting Started
* Google Apps Script API
```javascript
var gmailVerifierApi = new ObAIoTGASAPI.cGmailVerifier();
var response = gmailVerifierApi.validate(gmail);
```
response is a JSON object: <br/> {"success":true,"gmail":"contact@obaiot.com","isValidGmail":true} <br/>
success: true for API call success or false for failure,  <br/>
gmail: the gmail to validate,  <br/>
isValidGmail: indicates if a valid Gmail address  <br/>

* Web Service: 
Example is in javascript, the API endpoint: <br/> 
https://script.google.com/macros/s/AKfycbxswDaJlXbeV9dzcm8dTHLqGunlBeSOoiKtgD5rGQoRpwItAa9w/exec
```javascript
 try {
    var webHookUrl = 'https://script.google.com/macros/s/AKfycbxswDaJlXbeV9dzcm8dTHLqGunlBeSOoiKtgD5rGQoRpwItAa9w/exec';
    var payload = {
      "gmail" : gmail,  
    }
    
    var options =  {
      "method" : "post",
      "contentType" : "application/json",
      "payload" : JSON.stringify(payload)
    };
    
    var response = UrlFetchApp.fetch(webHookUrl, options); 
    var responseCode = response.getResponseCode();
    if (responseCode == 200) {
      return response;
    }
    else {
      Logger.log('validateEmail, post to Gmail Verifier web service failed, error code = ' + responseCode);
      return response;
    }
  }
   catch (ex) {
    Logger.log('validateEmail, post to Gmail Verifier web service failed, ex = ' + ex);
  }
```
