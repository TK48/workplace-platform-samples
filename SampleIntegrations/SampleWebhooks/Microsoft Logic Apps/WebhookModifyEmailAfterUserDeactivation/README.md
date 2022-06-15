# This code is now deprecated since Ms Logic Apps is not part of the thid-app directory of Workplace
--
# Webhook that modifies the user email address following their deactivation on Workplace

**Language:** JSON

## DESCRIPTION
This usecase example shows how to receive a webhook request when a [user](https://developers.facebook.com/docs/workplace/reference/graph-api/member) is deactivated on Workplace (manually or automatically) and how to modify the user email address afterwards appending a date to it. Example:

1. User A, whose email address is `userA@mydomain.com`, is deactivated on Workplace (manually or automatically).
2. Workplace notifies your webhook that User A has been deactivated.
3. The webhook code changes the email address of User A from `userA@mydomain.com` to `userA_20210601@mydomain.com`. Note that `20210601` would be the date of today.

It could solve for situations of email collision where new users inherit email addresses from old users.

## SETUP
* Create a custom integration in the section of Integrations from the Workplace admin panel.
* Generate an access token, and copy both the app secret and the access token, that will be needed to replace in the code.
* Create a Logic App on Azure.
* Go to the Logic App code view, and copy paste the JSON code in this repository with the access_token replaced.
* Configure the [WP webhook](https://developers.facebook.com/docs/workplace/reference/webhooks/) within the custom integration.

### PARAMETERS
Here are the details of the script parameters to be replaced:

   | Parameter         | Description                                                |  Type           |  Required    |
   |:-----------------:|:----------------------------------------------------------:|:---------------:|:------------:|
   | ACCESS_TOKEN      |  The access token of the Workplace integration             | _String_ | Yes |

### CREATE/CONFIGURE WEBHOOK ON WORKPLACE
More information on how to create an integration with the webhook functionality can be found in [this link](https://developers.facebook.com/docs/workplace/reference/webhooks/). You will need to create the integration and then register a webhook that can at least receive the events from "admin_activity", under the category of "Security".
To do so, you will need to add the callback url of your server, and an arbitrary verify token that needs to be the same on Workplace and in the webhook script.

### GENERATE ACCESS TOKEN
More information on how to generate an access token on Workplace can be found in [this link](https://developers.facebook.com/docs/workplace/custom-integrations-new/). The integration that you just created for the webhook should at least have the following permissions: "Read user email addresses", "Read security logs", "Read work profile" and "Manage work profiles".

## RUN
Once the webhook is configured in MS Azure Logic Apps and registered on Workplace, its code will run every time a user is deactivated on Workplace. It will trigger the change of email address for that user.
