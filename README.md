# Cart Management Application (Shopping List)

**Deploying Cart Management Application to Cloud**

## Project Overview

This is a simple **Cart Management / Shopping List** web application where users can:
- Add products to the cart
- Delete products from the cart
- Mark items as done

The application is a static website (HTML + JavaScript).  
As a Cloud Architect, the main task is to deploy this internet-facing website on a public cloud so that:

- Users from different parts of the world get fast loading of static assets
- Traffic is load-balanced at the DNS level
- Internal employees can easily share common files from a Virtual Machine

---

## Application Files

| File            | Description                          |
|-----------------|--------------------------------------|
| `index.html`    | Main page of the Shopping List       |
| `script.js`     | Main application logic (JavaScript)  |
| `script.ts`     | TypeScript version of the logic      |
| `app.js`        | Additional script                    |
| `package.json`  | Project metadata                     |
| `tsconfig.json` | TypeScript configuration             |
| `style.css`     | Styling for the application          |

---

## Cloud Deployment Solution

You can use **either AWS or Azure**. Both solutions are given below.

### Option 1: AWS Solution

| Requirement                              | AWS Service              | Purpose                                      |
|------------------------------------------|--------------------------|----------------------------------------------|
| DNS-level load balancing for global traffic | **Amazon Route 53**     | Route users to the nearest/healthy endpoint  |
| Store static content (HTML, JS, CSS, images) | **Amazon S3**          | Cheap and reliable object storage            |
| Fast delivery of static files worldwide  | **Amazon CloudFront**    | CDN – caches content at edge locations       |
| Virtual Machine for internal employees   | **Amazon EC2**           | Windows or Linux virtual machine             |
| Shared storage for teammates             | **Amazon S3** or **EFS** | Common place to store and share files        |

**High-level Architecture (AWS)**
1. Upload all static files (`index.html`, JS files, etc.) to an **S3 bucket**
2. Create a **CloudFront distribution** pointing to the S3 bucket
3. Use **Route 53** for DNS and health-based routing
4. Create an **EC2 instance** for internal employees
5. Attach shared storage (S3 or EFS) so employees can access common files

### Option 2: Azure Solution

| Requirement                              | Azure Service                  | Purpose                                      |
|------------------------------------------|--------------------------------|----------------------------------------------|
| DNS-level load balancing                 | **Azure Traffic Manager** + **Azure DNS** | Global traffic routing                    |
| Host the web application                 | **Azure App Service**          | Easy PaaS hosting                            |
| Serve static files fast                  | **Azure CDN**                  | Content Delivery Network                     |
| Virtual Machine                          | **Azure Virtual Machine**      | Windows or Linux VM                          |
| Shared storage for employees             | **Azure Files** or **Blob Storage** | Shared file access from VMs             |

---

## Governance of Resources (Dev / Test / Production)

### Approach
- Create **separate environments**:
  - Development
  - Testing / Staging
  - Production

**AWS**
- Use different AWS Accounts **or**
- Use the same account with strict **Tags** (`Environment=Dev`, `Environment=Test`, `Environment=Prod`)
- Use AWS Organizations + Service Control Policies for better governance

**Azure**
- Create separate **Resource Groups** for Dev, Test and Prod
- Apply **Tags** on every resource (`Environment`, `Project`, `Owner`)
- Use Azure Policy to enforce rules

This way all resources are clearly separated and easy to manage.

---

## Billing & Cost Management

### Approach
1. Enable cost tracking tools:
   - **AWS**: Cost Explorer + Budgets
   - **Azure**: Cost Management + Billing
2. Create separate **budgets and alerts** for:
   - Development
   - Testing
   - Production
3. Apply consistent **tags** on every resource so costs can be filtered by environment and project
4. Review costs regularly and set spending limits

This keeps a clear track of the billing life cycle of the company’s website.

---

## Implementation Steps (What needs to be done)

1. **Upload all static content** of the website to cloud storage (S3 Bucket or Azure Blob Storage)
2. **Create a CDN endpoint** (CloudFront or Azure CDN) and configure it to serve the static files
3. **Use a storage service** and upload files so teammates can share them easily
4. **Connect a Windows or Linux VM** to the shared storage service so internal employees can access the common files

---

## How to Run the Application Locally

1. Open the folder in VS Code or any editor
2. Open `index.html` directly in a browser  
   **or**
3. Use a simple local server (optional):
   ```bash
   npx serve .
