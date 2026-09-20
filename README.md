# cart-management-application
Cart Management / Shopping List app + Cloud Deployment (AWS/Azure)
# Cart Management Application (Shopping List)

 Deploying Cart Management Application to Cloud

## Project Overview
This is a simple Shopping List / Cart Management web application where users can add and delete products from the cart.

The company wants to host this internet-facing website on a public cloud (AWS or Azure) with the following requirements:
- Global traffic should be load-balanced at DNS level
- Static assets should be served fast from a CDN
- Internal employees need an easy way to share common files from a Virtual Machine

## Application Files
- `index.html` – Main page
- `script.js` / `script.ts` – Application logic
- `app.js` – Additional script
- `package.json` – Project metadata

## Cloud Deployment Solution

### Chosen Platform
You can choose either **AWS** or **Azure**. Below is a high-level approach for both.

### AWS Solution
| Requirement | AWS Service |
|-------------|-------------|
| DNS-level load balancing for global traffic | **Route 53** |
| Store static content (HTML, JS, images, etc.) | **S3 Bucket** |
| Fast delivery of static files worldwide | **CloudFront** (CDN) |
| Virtual Machine for internal use | **EC2** |
| Shared file storage for teammates | **S3** (or EFS attached to EC2) |

### Azure Solution
| Requirement | Azure Service |
|-------------|---------------|
| DNS-level load balancing | **Azure Traffic Manager** + **Azure DNS** |
| Host the web application | **Azure App Service** |
| Serve static files fast | **Azure CDN** |
| Virtual Machine | **Azure Virtual Machine** |
| Shared storage for employees | **Azure Files** or **Blob Storage** |

### Governance & Cost Management
1. **Resource Governance**
   - Use Resource Groups (Azure) or separate AWS Accounts / Tags for:
     - Development
     - Testing
     - Production
   - Apply naming conventions and tags on every resource.

2. **Billing & Cost Tracking**
   - Enable Cost Explorer / Cost Management + Billing
   - Create separate budgets and alerts for Dev / Test / Prod
   - Use tags (Environment, Project, Owner) so costs can be filtered easily

### Implementation Steps Required by the Project
1. Upload all static content of the website to cloud storage (S3 / Azure Blob)
2. Create a CDN endpoint and point it to the static files
3. Create shared storage for teammates
4. Connect a Windows or Linux VM to the shared storage

## How to Run Locally
1. Open `index.html` in any browser
2. Or use a simple local server if needed

## Author
Deepthi
