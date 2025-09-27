### Hosting a Static Website on an Amazon S3 Bucket

Hosting a static website on Amazon S3 is a cost-effective and scalable way to make your site available to the public. Here's a step-by-step guide based on the provided screenshots.

---

### Step 1: Create an S3 Bucket

First, you need to create a new S3 bucket to store your website files.

1.  Navigate to the S3 service in your AWS Management Console.
2.  Click **Create bucket**.
3.  Give your bucket a unique name. In the screenshot, the bucket is named **`mywebbucket-21`**. Make sure the name is globally unique.
4.  Choose the **AWS Region** where you want your bucket to be located. The screenshot shows **Asia Pacific (Mumbai) `ap-south-1`**. This is where your website's files will be physically stored.
5.  Keep all other settings at their defaults and click **Create bucket**.
![Step 1 - Create Bucket](/images/Create%20Bucket.png)

---

### Step 2: Upload Your Website Files

After creating the bucket, you need to upload your static website files into it.

1.  Open the newly created bucket.
2.  Click the **Upload** button.
3.  Add your website files, including your main HTML file (e.g., **`index.html`**) and any associated CSS, JavaScript, and image files.
4.  The screenshot shows **`index.html`** and two image files, **`candy.webp`** and **`candy.webp`**, have been uploaded.
 ![Step 1 - Create Bucket](/images/Add%20files.png)
---

### Step 3: Configure Public Access

By default, S3 buckets are private. To make your website accessible to the public, you need to unblock public access and configure a bucket policy.

1.  **Disable "Block public access"**:
    * Go to the **Permissions** tab of your S3 bucket.
    * Under **Block public access (bucket settings)**, click **Edit**.
    * Uncheck the box that says **Block all public access**.
    * Save the changes. This allows you to grant public access later.
![Step 1 - Create Bucket](/images/edit%20block%20public%20access.png)

2.  **Add a bucket policy**:
    * In the same **Permissions** tab, scroll down to **Bucket policy**.
    * You need to create a JSON policy that allows public read access to the objects in your bucket. The policy generator can help with this. The screenshot provides a sample policy.
    * The key parts of the policy are:
        * `"Effect": "Allow"`: Grants permission.
        * `"Principal": "*"`: Applies to everyone (public access).
        * `"Action": "s3:GetObject"`: Allows users to retrieve objects (files).
        * `"Resource": "arn:aws:s3:::mywebbucket-21/*"`: Specifies that this policy applies to all objects (`/*`) within your bucket.
    * Copy and paste the generated policy into the policy editor and click **Save changes**.
![Step 1 - Create Bucket](/images/add%20policy.png)
![Step 1 - Create Bucket](/images/create%20policy.png)

---

### Step 4: Enable Static Website Hosting

Finally, you need to enable the static website hosting feature for your bucket and specify your index document.

1.  Go to the **Properties** tab of your S3 bucket.
2.  Scroll down to the **Static website hosting** section and click **Edit**.
3.  Choose **Enable** and set the **Index document** to your main HTML file, typically **`index.html`**. You can also specify an **Error document** if you have one.
4.  Save the changes.

AWS will now provide you with a **Bucket website endpoint** URL. This is the public URL for your static website.

---

### Step 5: Access Your Website

You can now access your website using the **Bucket website endpoint** provided in the previous step.

1.  Open a new browser tab.
2.  Paste the endpoint URL and press Enter.
3.  You should see your static website loaded. The screenshot shows the "NEW ICE-CREAM BRAND - V2" website successfully hosted.

![Step 1 - Create Bucket](/images/host%20website.png)

---

### Step 6: Enable Versioning

Enabling versioning on your S3 bucket allows you to keep multiple versions of your files. This is very useful if you need to revert to an older version of your website.

1.  Go to the Properties tab of your S3 bucket.
2.  Scroll down to Bucket Versioning and click Edit.
3.  Select Enable.
![Step 1 - Create Bucket](/images/Enable%20versioning.png)
4.  Click Save changes.
![Step 1 - Create Bucket](/images/show%20versioning.png)

Now, whenever you upload a file with the same name as an existing file, S3 will keep the previous version. You can restore older versions if needed.