Django-mailchimp-subscribe
==========================

This is an instruction on how to add a "subscribe to mailchimp" on your Django website.

Because most sites regularly use external connections nowadays, you don't want to have a high number of packages if it can be avoided.  Django-requests makes swift work handling CURL and WGET calls in a better manner.

This repo describes how to use Django-requests to make a CURL call to add a person to a mailchimp list.

Dependency:
Django-requests

NOTE: located in the views.py function, these two lines do the heavy lifting.  
```python
 data = '{ "apikey": "' + apikey + '", "id": "' + listid + '", "email": { "email": "' + email + '" }, "merge_vars": {}, "email_type": "html", "double_optin": true, "update_existing": true, "replace_interests": true, "send_welcome": true }'

response = post('https://###.api.mailchimp.com/2.0/lists/Subscribe.json', data=data, headers={'Content-type': 'application/json', 'Accept': 'text/plain'}).text
```
Here's how they work:
starting backwards with the response line, the 2.0 api configuration uses URL Slugs instead of GET variables.  The lists/Subscribe slug is the operator to add a person to a mailchimp subscription.  The .json ending indicates the method that the payloads are to be handled, both in and out.  

The data variable is the json input (hence why this example uses .json).  It follows the standard for the operator designed.  IN this case it's lists/subscribe.  Use the example here to add and remove parts as desired:  https://apidocs.mailchimp.com/api/2.0/lists/subscribe.php

you should see this in return:
```json
    {
        "email": "example email",
        "euid": "example euid",
        "leid": "example leid"
    }
 ```
Anything else is a problem.

Using the 2.0 standard, all you have to do if you want to perform other operations is to change the slug, and the data string.  It should work.

Good luck.

