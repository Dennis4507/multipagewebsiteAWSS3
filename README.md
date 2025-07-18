# multipagewebsiteAWSS3
Hosting a multi-page website on Amazon S3

Here is a detailed step-by-step guide on how i hosted my static Resume website on Amazon S3, also included are the  common issues i faced and how to resolved them:



I used VS code to deploy and edit my website. I build the  Website in HTML, CSS AND Javascript. 

I costomized an already made theme to my liking to get the mobile friendly responsiveness and also added the cascading project segment as well as the multipage aspect of the website. 

![alt text](<bilder/VS Code Resume Website (195).PNG>)
    
    
    
   
2. Create S3 bucket Go to the AWS S3 console .
• Create a bucketIf you want to use a custom domain name (e.g. ), the bucket should be named exactly like your domainwww.example.com.
• Make sure that the settings for blocking public access are disabled. In the "Permissions" tab, click "Block Public Access" and uncheck "Block all public access". Confirm the changes.
3. Upload files
• Upload all your website files to the S3 bucket.
• Make sure you maintain the folder structure when uploading your filesYou can do this via the S3 console, the AWS CLI, or a CI/CD pipeline.
4. Configure static website hosting This is a crucial step to make your website accessible .
• In the S3 console, go to your bucket and click on the "Properties" tab.
• Scroll to the "Static website hosting" section.
• Activate hosting.
• Set your "Index document" , usuallyindex.html.
• Optionally, you can specify an "Error document" (e.g. ) or leave this field blankerror.html.
• Click "Save".
5. Set a bucket policy for public read access A bucket policy is required to enable anonymous access (public read access) to your website files .
• In the S3 console, go to your bucket and click on the "Permissions" tab.
• Scroll down to the Bucket Policy section.
• Insert the following JSON directive. Replace YOUR_BUCKET_NAME with the actual name of your S3 bucket. In the example of the previous conversation, this would bedenispersonalwebsite.
• Click "Save changes".
6. Test the website
• After configuration, you will receive a public S3 website URL. This typically has the formathttp://YOUR_BUCKET_NAME.s3-website-REGION.amazonaws.com.
• In the conversation example, your URL was:http://denispersonalwebsite.s3-website.eu-central-1.amazonaws.com/.
• Open this URL in your browser to check if your website is displayed correctly.
Optional steps for advanced configurations
• Custom Domain + HTTPS : You can use AWS Route 53 (or another DNS provider) to point your custom domain (e.g. ) to the S3 websitewww.example.comFor HTTPS, you need AWS CloudFront and AWS Certificate Manager (ACM). Create a CloudFront distribution with your S3 bucket as the origin, request an SSL certificate through ACM, and use the custom domain with the distribution..
• "Clean URLs" (without .html) : S3 does not support rewrite rules by default. However, with CloudFront in combination with Lambda@Edge or CloudFront Functions, you can rewrite URLs like/about/about.html.
Common problems and their solutions
Issue 1: “Expected params.WebsiteConfiguration.RoutingRules to be an Array” error
• Cause : This error occurs when you try to insert the bucket policy (which is a JSON object) into a location that expects website hosting settings , such as the static website hosting configuration area. In particular, it occurs when you specify in an AWS CLI, SDK, or CloudFormation configuration and these are not formatted as an arrayRoutingRulesThe bucket policy itself does not cause this error if it is inserted in the correct location.
• Solution :
    1. Double-check the insertion location of the JSON file : The JSON you provided is a bucket policy. It must be added exclusively in the "Bucket Policy editor" under the "Permissions" tab of your S3 bucket.
    2. DO NOT include them in the static website hosting configuration sectionThis area expects specific website hosting settings (index and error documents, redirect rules).
    3. Correct configuration of static website hosting via the AWS console :
        ▪ Go to your S3 bucket and the "Properties" tab.
        ▪ Scroll to "Static website hosting".
        ▪ Select "Enable".
        ▪ Enter your "Index document" (e.g. ) and optionally your "Error document" (e.g. )index.htmlerror.html.
        ▪ Click "Save".
    4. If you are using AWS CLI or SDK : Make sure your website configuration has the correct JSON format for website settings, in case you want to specify them. If you don't have any redirect rules, just use an empty array forRoutingRules[]RoutingRules.
Problem 2: The website is not displayed or is not accessible
• Cause : If your website does not work as expected under the generated S3 URL, it is usually due to a missing or incorrect configuration of the previously mentioned steps.
• Solution : Check each of the above steps carefully:
    ◦ Files uploaded : Make sure that all your website files have been correctly uploaded to the bucket and the folder structure has been maintained.
    ◦ Block Public Access disabled : Make sure that "Block all public access" is disabled in your bucket's permissionsThis is crucial for public access.
    ◦ Static website hosting enabled : Check in the "Properties" tab if "Static website hosting" is enabled and your has been set as "Index document"index.html.
    ◦ Bucket policy correct : Ensure that the bucket policy (as described in step 5) is correct, contains the correct bucket name , and has been inserted in the correct area (Permissions > Bucket Policy). The policy must allow the on the correct resource ( ) so that users can access the filess3:GetObjectPrincipal "*"arn:aws:s3:::YOUR_BUCKET_NAME/*.
By systematically checking and correcting these configuration points, you should be able to successfully host your website on Amazon S3.
