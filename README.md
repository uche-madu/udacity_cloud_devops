
# Deploy Static Website on AWS

In this project, I have deployed a static website to AWS using S3, CloudFront, and IAM.

The files included are: 

* `index.html` - The Index document for the website.
* `/img` - The background image file for the website.
* `/vendor` - Bootssrap CSS framework, Font, and JavaScript libraries needed for the website to function.
* `/css` - CSS files for the website.

The above files and folders have all been uploaded into an S3 bucket,
which has been configured to support static website hosting. 

![image](https://user-images.githubusercontent.com/29081638/205428397-e434c09a-c085-426b-aa6c-dbb743802975.png)

The full configuration steps have been illustrated in the `udacity_screenshots.pdf` file

## Web Browser Access
The website is publicly available via the following addresses:
* Website Endpoint: [http://uche-project1-bucket.s3-website.us-east-2.amazonaws.com/](http://uche-project1-bucket.s3-website.us-east-2.amazonaws.com/)
* CloudFront Domain Name: [https://d3l4sgv1auytwu.cloudfront.net/](https://d3l4sgv1auytwu.cloudfront.net/)
* S3 object URL: [https://uche-project1-bucket.s3.amazonaws.com/index.html](https://uche-project1-bucket.s3.amazonaws.com/index.html)







