# multipagewebsiteAWSS3
Hosting a multi-page website on Amazon S3

Here is a detailed step-by-step guide on how i hosted my static Resume website on Amazon S3, also included are the  common issues i faced and how to resolved them:

![alt text](<bilder/Screenshot (377).png>)



1. I used VS code to deploy and edit my website. I build the  Website in HTML, CSS AND Javascript. 

I customized an already made theme to my liking to get the mobile friendly responsiveness and also added the cascading project segment as well as the multipage aspect of the website. 

![alt text](<bilder/VS Code Resume Website (195).PNG>)
    
    
2. I worked on the website, changed the CSS, HTML and Javascript to achieve a prefered design and layout.

Then Logged into AWS and created an S3 bucket and named the bucket named 

denisriungu.de bucket
![alt text](<bilder/Screenshot (230).png>)




 
3. Then made sure hat the settings for blocking publish access are disabled 
![alt text](<bilder/Screenshot (229).png>)

Uploaded the website files to the S3 bucket, making sure we maintain the folder structure.

I uploaded the files using Githubactions CI/CD pipeline 

(Link to github actions cicd project) To show how we uploaded website files to AWS S3 Bucket

![alt text](<bilder/Screenshot (231).png>) 


4. Configure static website hosting This is a crucial step to make your website accessible .

In the S3 console, we activated the "stastic website hosting section"

![alt text](<bilder/Screenshot (232).PNG>)
![alt text](<bilder/Screenshot (233).png>)


5. Then I Set a bucket policy for public read access A bucket policy which is required to enable anonymous access (public read access) to your website files.

In the S3 console, on the bucket on "Permissions" Tab
"Bucket Policy" section, I programmed a JSON directive specificly for my S3 Bucket.

![alt text](<bilder/Screenshot (236).png>)


6. Test the website

After the configuration i received a public S3 website URL. 

and i test the URL 
and it shows my website

![alt text](<bilder/Screenshot (235).png>)

and confirmed that my website is displayed correctly.


Problems experienced

Experienced issues when the website was not able to show because the website files wer not uploaded on the rootfolder since i had created a new folder called denisriungu and uploaded the website folders inside there which made the website now show. 

Asked on Stackoverflow and also Chatgpt

Solution?

Migrated the folders from denisriungu folder to denispersonalwebsite folder which is the root 
s3 Bucket folder and voila. the website was visible.


Problem experienced.

I was able to accedd the website using the s3 bucket link but couldn'T seem to be able to access when clicking them on the navbar other pages on the website eg the portfolio.html, Blog.html and contact.html 


Asked github co pilot on vscode.

Solution.

It happened to be a Case Sensitivity issue as S3 is case-sensitive so 

Contact.html ≠ contact.html

Blog.html ≠ blog.html

so had to update the links on my html to match the case exactly and the 

website and all the other pages wer visible.