# Lab 4 - Intro to API Gateway

**Purpose:** Setup an API Gateway endpoint for your hello world function.

**Pre-requiste:** You must have completed Lab 3 prior to running this lab.

## 1 - Connect to AWS API Gateway Console

Using the account you created in lab 1, log back into the AWS console.  

The sign-in page is available at:

https://console.aws.amazon.com

Once logged in, you should select API Gateway from the list of available services.  Open the API Gateway page to continue this lab.

## 2 - Create a New API

This next step is going to be different depending upon whether or not an API Gateway enpoint already exists in your account.  Assuming one does not, you will be presented with a page that gives you an overview of API Gateway.  From this page, you can click the '`Get Starterd`' link.

You are now given a choice of three different ways to create a new API.  The default will be to create an example API.  However, we want to create a '`New API`'.  Select that radio button.

For the details of the API, give it the name '`hello-world-api`' and leave all other options the same.  Click `'Create API`' to continue.

If you aleady have an API in your account, the main page for API Gateway will give you a button to `'Create API`'.  Click that, and follow the instructions above.  

## 3 - Create a Simple Action

From the page for the API, you should see an `Action` dropdown.  Click it, and select '`Create Method`'.  This is going to allow you to specify a REST HTTP action for the `/` resource.  Select '`Get`' from the dropdown and click the checkbox.

## 4 - Specify Integration

You should now see a page where you can select the integration type for your API gateway endpoint.  Choose '`Lambda Function`'.  Next, in the '`Lambda Function`' text box, type '`hello-world-lambda`' to tie this API method to your existing function.  Leave all other options the default and click `Save`.

You will get a dialog confirming you want to grant API Gateway permissions in IAM to call your function.  To proceed, click `OK`.

## 5 - Testing Integration

Now that you have an integration set up, it is time to test it.  The screen currently showing should be the integration details for your GET method.  (If it isn't you can select GET from the method under your `/` resource).

The should be a `'TEST`' link on this page.  Click it to open the test page.

The resulting test page doesn't give you any options (since you didn't declare any parameters for the GET).  Click the '`Test`' button, and look at the results.

You should see something that looks like this...

```
Request: /
Status: 200
Latency: 214 ms

Response Body
{
  "message": "hello world"
}

Response Headers
{"X-Amzn-Trace-Id":"Root=1-5bbb5a6c-1ecb91f25c64e48f371ace99;Sampled=0","Content-Type":"application/json"}
```

Your API Gateways test has successfully interacted with your Lambda function.

## 6 - Deploy your API

Now that we have successfully tested the API, it is time to deploy it.  From the '`Action`' dropdown, select `'Deploy API`'.

This will bring up a dialog where you need to specify which stage to deploy you API to.  A stage allows you to have potentially multiple versions of an API - each having a potentially different schema or integration.

We are going to select '`[New Stage]`' from the dropdown.  Next, specify '`api`' for the stage name and click '`Deploy`'.  

## 7 - Invoke your API

From the next page, you should get a link that has the invoke URL for you API.  Either in a browser or Postman, you can execute this link.  You should receive the following result document back:

```json
{"message": "hello world"}
```

## 8 - Look at changes to your Lambda function

You can leave API Gateway now.  We should open up Lamba again from the AWS service list.

You should see `hello-world-lambda` in the list of available functions.  Click on it.

In the resulting page, you can see that the configuration of your function has change.  You should see that API Gateway has been added as an event trigger for the function.

## Conclusion

At the conclusion of this lab, you should have learned how to do the following things:

* Create an API Gateway API
* Create an HTTP method on an API Gateway
* Associate an API Gateway method with a Lambda function
* Test an API Gateway integration
* Deploy an API Gateway integration

