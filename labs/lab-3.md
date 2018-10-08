# Lab 3 - Intro to Lambda

**Purpose:** Setup a simple "hello world" Lambda function to be later called by API gateway.

## 1 - Connect to AWS Lambda Console

Using the account you created in lab 1, log back into the AWS console.  

The sign-in page is available at:

https://console.aws.amazon.com

Once logged in, you should select Lambda from the list of available services.  Open the Lambda page to continue this lab.

## 2 - Create a Function

We want to create a simple Lambda function that will return a Hello World JSON document.  To get started, click '`Create Function`' from the main page.

This gives you a few options - '`Author from scratch`', '`Blueprints`', and '`AWS Serverless Application Repository`'.  For this lab, we will be using the default options - '`Author from scratch`'.

Before we can create our function, we need to specific a few items.

First, we need a name.  Give our function the name '`hello-world-labmda`'.  

Next, we need to pick the runtime for our function.  Lambda supports a number of different runtimes, each with their own pros and cons.  For our labs, we will be using the '`Python 3.6`' runtime.

Finally, we need to specify the IAM role that our function will run under.  Since we have not yet created a service role, we can let the Lambda GUI create our role for us.  We will be using the basic template for our role.  Specify '`hello-world-lambda-role`' for the name of the role, and leave the policy template empty.

After specifying these values, click the '`Create Function`' button to create your new function.

## 3 - Edit the Function Code

From the next screen, you can see the basic implementation of your Lamba function.  You can see at the top of the page that there are no triggers set up for your function, and that it has access just to '`Amazon CloudWatch Logs`'.  

Scroll down on the page until you see the code for the function.  Replace the code with the following:

```Python
def lambda_handler(event, context):
    return { "message": "hello world" }
```

Once completing this edit, click `Save`.

## 4 - Test the Function

To test the function from the web console, we need to create a test event.  All Lambda calls are triggered in response to an event.  Thus, we need to set up a test event.

Click the '`Select a test event..`' dropdown from the top of the screen and click '`Configure test events`'.  The default event you get is from the '`Hello World`' template.  For different events, such as SQS or API Gateway, you would you a different event. 

Our simple function does not actually use the event we receive.  Thus, you can use the sample event as declared.  Give the test a name - '`helloworldevent`' - and Click '`Create`' to continue.

Now that you have '`helloworldevent`' selected from the test events, you can click '`Test`' to see the results of the function.

At the top of the page, there is a section that should - if everything went as expected - show "Execution result: succeeded".  

You can click the `details` expander to see the details of the function execution.

## 5 - Inspect Cloud Watch Logs

Now that you have executed a Lambda function, we can look at the logging for that function.  Select `CloudWatch` from the list of available AWS services.

Once in CloudWatch, you should select '`Logs`' from the menu on the left.  You should see a log group called '`/aws/lambda/hello-world-lambda`'.  Click on this log group link.

There will be at least one log stream in this group.  Click on the log stream.  From here, you should see the details that have been written to the log output from your test run.  All future calls to you Lambda function will be logged to a stream in this log group.

## 6 - Inspect IAM Role

Finally, we want to inspect the IAM role created for our function.  Select '`IAM`' from the list of available AWS services.

Once, in IAM, select `Roles` from the left menu.  You should see a role called '`hello-world-labda-role`' here.  Click on it.

Under the role, you should see one policy.  This policy was created by the Lambda console.  It will begin with '`AWSLambdaBasicExecutionRole-`'.  Expand the role and look at its policy summary.

You can see that your function has permissions into CloudWatch logs, but nothing else.  This permission is what allowed the function to write to the logs you just inspected.  If you wanted this function to interact with any other resource - such as S3 - you would need to attach a new policy.  (We will do this in a future lab)

## Conclusion

At the conclusion of this lab, you should have learned how to do the following things:

* Create a function from the Lambda console
* Specficy the type of IAM role to be created for a function
* Edit code in a Lambda function
* Test a Lambda function
* Inspect the logs of a function
* Inspect the IAM role created by Lambda

