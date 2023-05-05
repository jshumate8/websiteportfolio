<h2> Launching a Static Website using AWS S3 Buckets</h2>

<h3>The aim of this project is to launch a static website using AWS S3 buckets and Route53.</h3> 

#### Step One
<p>
1. Setup an AWS account (I already had one).</br>
2. Find a website template you would like to use and download the files. I used one from https://html5up.net/.<br>
3. Register a domain name through whatever DNS service you like. You can use Route53 to register a domain name, but I already had the domain registered through Google.<br>
3. Setup an S3 Bucket in AWS<br>
<br>
    1) Search for S3 in console. <br>
    2) Click "Create Bucket" <br>
    3) <i>Critical</i>: name the bucket the same as the domain name. e.g. If domain name is myawsomedomain.com, the bucket name should be myawesomedomain.com.<br>
    4) Select an AZ (if you do not know what AWS AZs are, see <a href="https://aws.amazon.com/about-aws/global-infrastructure/regions_az/"> AWS's site</a>. If in doubt, select the one nearest your geolocation (where you live).<br>
    5) Scroll down to "Block Public Access settings for this bucket" and <i>UNCHECK</i> "Block all public access." This is because AWS by default blocks public access to S3 storage.<br>
    6) Scroll down to the bottom and click "Create Bucket"<br>
    7) Create a second bucket following the same procedures, but this time name the bucket the same name as before, but with the prefix "www." So if your domain name is myawesomedomain.com, this bucket should be named www.myawesomedomain.com. <br>
    8) After both buckets are created and both set to public, go into the first one by clicking on it. We need to make 2 critical updates to the bucket.
    9) First, under the Properties tab, scroll down to the bottom, to where it says, "Static website hosting." Click the EDIT button. <br>
    10) In this menu, click the button to enable static website hosting. Under hosting type, select host a static website.<br>
    11) In the field titled "index document," type index.html.<br>
    12) In the field titled "error document," also type index.html.<br>
    13) Save changes<br>
    14) Go back to the previous menu with your bucket. This time click the Permissions tab. AWS will allow us to set limits on what can be done to this bucket and the data inside. We have set it to public, which means anyone on the internet now has access to what is in this bucket. You need this if you want to host a website. However, we do not want an internet user to be able to make changes to any of the files in our bucket, so we are going to add a bucket policy that will only allow public users to read the files stored in the S3 bucket and nothing more. (They are not actually reading them, but their computer is.) <br>
    15) To do this, scroll to Bucket Policy and click the EDIT button. In the form, insert the code found <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html">HERE</a>.<br>
    16) Now go to the second bucket you created and repeat step 9. This time, in the edit menu, select to enable Static website hosting, but in the next option, select Redirect requests for an object. This is going to redirect traffic from www.myawesomedomain.com to your main s3 storage bucket where the files will be kept. <br>
    17) Repeat step 15 for this bucket as well.</p>
    <br>
    4. Upload files to your primary S3 bucket (the first one you created). <i>IMPORTANT!</i> Make sure when you upload the files, you upload them directly into the S3 main directory. If you have the files in a folder on your computer, do not uplod the folder into the main directory of your S3 drive with all of the files in a subdirectory within this folder. This will cause your website not to work. Make sure the folder files for your website are loaded directly into the main S3 storage directory. This means that if I click on the bucket, the items from your template folder on your computer should be directly available.<br>
    5. Let's see how we're doing. Go to your main bucket and into the Properties tab once again. Scroll all the way to the bottom. In Static Web Hosting section, at the bottom, you should see a hyperlink starting with HTTP://myawesomedomain.com.s3......" Copy this link and paste it into your web browser. Your site should now come up. If it doesn't, there is an error somewhere and you need to check the steps above to see where there is a failure.
    6. If everything is working, we now need to set up your custom domain to go with the site. Depending on who your site is registered with, these instructions will vary. 
    1) Go to Route53 in the AWS Console menu.
    2) On the left-hand menu, select Hosted Zones. 
    3) In the next menu, select Create hosted zone.
    4) 
    
   

