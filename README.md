# AWS S3 Static Website Hosting with CloudFront, ACM Certificate, and Route 53

This project demonstrates how to host a static website using AWS S3, enhance performance and security with AWS CloudFront, and configure a custom domain using Route 53. An ACM SSL certificate is used to ensure secure HTTPS connections.

---

## Features

- **S3 Static Website Hosting**: Stores and serves static web files (`index.html` and `style.css`).
- **CloudFront Integration**: Distributes content globally with improved performance and security.
- **ACM SSL Certificate**: Secures the website with HTTPS.
- **Route 53 Custom Domain**: Maps the website to a custom domain using DNS routing.
- **Scalable and Cost-Effective Solution**: Uses serverless resources for efficiency.

---

## Steps to Recreate

### 1. **Create an S3 Bucket**
   - Go to **S3** and create a new bucket:
     - **Bucket name**: Use a globally unique name.
     - Enable **block all public access** (for CloudFront integration).
   - Upload your static web files (`index.html`, `style.css`, etc.) to the bucket.
   - **Properties**: Enable static website hosting:
     - Enter `index.html` as the default document.

### 2. **Configure AWS CloudFront**
   - Create a new CloudFront distribution:
     - **Origin**: Select the S3 bucket.
     - **Viewer Protocol Policy**: Redirect HTTP to HTTPS.
   - Use the default behavior for caching and content delivery.
   - After the distribution is created, note the CloudFront domain name (e.g., `dxyz1234.cloudfront.net`).

### 3. **Request an ACM SSL Certificate**
   - Navigate to **AWS Certificate Manager (ACM)** and request a certificate:
     - Enter your custom domain (e.g., `www.example.com`).
     - Use DNS validation:
       - Add the CNAME record to your Route 53 hosted zone.

### 4. **Link CloudFront with ACM Certificate**
   - Update the CloudFront distribution settings:
     - Add the ACM SSL certificate for HTTPS support.
     - Configure the alternate domain name (CNAME) to match your custom domain.

### 5. **Set Up Route 53 Hosted Zone**
   - Create or use an existing hosted zone for your custom domain.
   - Add an **Alias record**:
     - Target: The CloudFront distribution domain name.
     - Record type: `A` (IPv4).

### 6. **Access Your Website**
   - Navigate to your custom domain in a browser (e.g., `https://www.example.com`).
   - The static content is served securely and globally through CloudFront.

---

## How It Works

1. **S3** stores the static website files.
2. **CloudFront** ensures global content delivery with caching and HTTPS.
3. **ACM** provides an SSL certificate for secure connections.
4. **Route 53** handles domain name resolution and DNS routing.

---

## Folder Structure

```plaintext
aws-s3-cloudfront-acm-dns-hosting/
├── Static_Website_Files/       # Contains your static files (index.html, style.css, etc.)
├── README.md                   # Project documentation
└── Screenshots/                # Folder with setup screenshots for S3, CloudFront, ACM, and Route 53


Requirements
AWS Free Tier Account or equivalent.
Custom Domain for Route 53 configuration.
Basic Knowledge of AWS services (S3, CloudFront, ACM, and Route 53).

Screenshots
S3 Bucket Configuration
CloudFront Distribution Settings
ACM Certificate Validation
Route 53 Hosted Zone Configuration

Future Enhancements
Automate deployment using AWS CloudFormation or Terraform.
Add a CI/CD pipeline for continuous updates to the S3 bucket.
Implement versioning for static website files.
