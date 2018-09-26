# Lab 2 - Intro to S3

**Purpose:** Setup a simple "hello world" website on S3.

## 1 - Connect to AWS S3 Console

Using the account you created in lab 1, log back into the AWS console.  

The sign-in page is available at:

https://console.aws.amazon.com

Once logged in, you should select S3 from the list of available services.  All the rest of this lab will be done in the S3 app.

## 2 - Create a New Bucket

All data in S3 is stored in a construct called a *bucket*.  An S3 bucket is a collection of key/value blobs that share a common region and configuration.

The best practice for S3 bucket creation is to seperate buckets based upon region and purpose.  For our lab, we will be creating a bucket in your default region to serve as the host for a website.

Click the `Create Bucket` button to get started with your S3 bucket.  This will bring up a dialog that requires you to specify some settings on the bucket.

First, and most imnportantly, you must select a region and name for a bucket.  Note that S3 bucket names are globally unique.  So, your name cannot be in use in any other account.  Next, you must pick the region to create the bucket in.  Think carefully when creating buckets because neither the name nor the region can be changed after creation.

After supplying the name and region, we will click `Next` to proceed through the dialogs.  The values under `Configure Options` and `Set Permissions` can be changed after creating the bucket.  For now, we will leave all of these as their default values.

Once you get to `Review`, take a last look at your name and region and make sure they are correct.  Once confirmed, you can click `Create Bucket` to continue,

## 3 - Upload Your First File

From the GUI, click on the name of the bucket.  This will bring you to the bucket overview page.  Since your bucket is currently empty, one of the first things you will need to do is create some content to load into it. 

In your text editor of choice, create a file called `index.html`.  The contents of this file should be an HTML page.  If you want a quick copy/paste version, you can use the following:

```html
<html>

  <body>
    <h1>Hello from AWS</h1>
  </body>

</html>
```

Once you create this file, click on the `Upload` button on the S3 console.  This gives you a dialog where you can click `Add files` and browse to the file you just created.

After adding the file, click `Next` to procees through the dialogs.  We don't need to change any properties on this file.  Then, on the last dialig, click `Upload`.

You should now see a file called `index.html` in your bucket.  Click on this file.  It will show you several pieces of information about the file.  One interesting piece of information is the URL link to the file.  

Feel free to click this link if you want.  When you do, you will see and Access Denied page.  This is because AWS IAM is restricting access to the file.  Shortly, we will resolve this issue.

## 4 - Setup Web Hosting

On the bread crum trail (or by using the back button), navigate to the bucket overview page.  We are going to set up the bucket to host a static website.

Click on the `Properties` tab.  From here, you will see several settings you can turn on for a bucket.  The one we care about is `Static website hosting`.  Click it.

From this dialog, select `Use this bucket to host a website`.  Once selecting this, type `index.html` for the index document.  (As a note for people familiar with IIS, S3 websites are case-sensitive.  There is a difference between `index.html` and `Index.html`.)

Make note of the endpoint listed.  It is in the form of:

http://{bucketname}.s3-website-{region}.amazonaws.com

We will use this URL to test our site next.

Click `Save`.  You should set that the `Bucket hosting` setting is now checked.  To confirm hosting is working, open the URL endpoint.

You should see an error page for a 403.  (If you get a 404, you have need to confirm the URL from step 4).

## 5 - Applying IAM Policy

There are a couple of ways to make a bucket public.  The method we are going to use is by creating an IAM policy,

Click the `Permissions` tab on your console for the S3 bucket overview.  From here, click `Bucket Policy`.  

An IAM policy is a JSON document that describes permissions allowed or denied to a particular resource.  For this policy, copy the following document into the policy editor.  You will need to change the name of the bucket from `mycooldemos3bucket` to whatever your bucket name is.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::mycooldemos3bucket/*"
        }
    ]
}
```

After clicking `Save`, you will get a warning the this bucket has public access.  Since this is intended to be a public website, we can ignore this warning.  (But remember, NEVER put secret information of ANY KIND in a public S3 bucket).

Try refreshing your web link from before.  You should now see "Hello from AWS" displayed on the page.

## Conclusion

At the conclusion of this lab, you should have learned how to do the following things:

* Use the S3 console
* Create an S3 bucket
* Upload a file to S3
* Set up a bucket to be a static website host
* Apply a simple IAM bucket policy

