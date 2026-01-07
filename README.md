# azure-slot-swapping

# Azure App Service Deployment with Slot Swap

![Azure](https://img.shields.io/badge/Azure-App%20Service-0089D6?logo=microsoftazure&logoColor=white)
![Deployment Slots](https://img.shields.io/badge/Blue--Green%20Deployment-Enabled-brightgreen)
![Status](https://img.shields.io/badge/Project-Completed-success)

This project demonstrates how to deploy a static HTML web application to **Azure App Service**, configure a **staging deployment slot**, deploy updated code to staging, and perform a **slot swap** to safely promote changes to production.

This workflow demonstrates a real-world **blue–green deployment strategy**, ensuring zero downtime, safe rollbacks, and controlled testing.

---

## 📘 Overview

This project includes:

- Deployment of a sample HTML website using Azure CLI  
- Creation of a staging deployment slot  
- Updating and deploying code to the staging slot  
- Swapping staging and production slots  
- Verifying deployment in production  
- Cleaning up Azure resources  

---

## 📂 Project Structure

/azure-slot-deployment-project
│
├── index.html
├── stagingcode.zip
├── README.md
├── Azure Deployment Guide.pdf
└── screenshots/


---

## 🏗️ Architecture

           +----------------------+
           |  Azure App Service   |
           +----------+-----------+
                      |
      +---------------+----------------+
      |                                |
+---------v----------+ +----------v---------+
| Production Slot | <----> | Staging Slot |
| (Live Website) | Swap | (Test Changes) |
+--------------------+ +---------------------+


---

## 🔧 Tech Stack

| Component | Purpose |
|----------|---------|
| Azure App Service | Web hosting |
| Deployment Slots | Blue-green deployment |
| Azure CLI | Resource creation & deployment |
| Cloud Shell | Browser-based CLI |
| HTML/CSS | Static web content |

---

## 🚀 Steps to Deploy

### **1️⃣ Clone the Sample App**

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git

Set Variables:-
resourceGroup=rg-mywebapp
appName=mywebapp$RANDOM
echo $appName

Deploy to Azure:-
cd html-docs-hello-world
az webapp up -g $resourceGroup -n $appName --sku P0V3 --html

Create a Deployment Slot:-
az webapp deployment slot create -n $appName -g $resourceGroup --slot staging

Update & Deploy Code to Staging:-
Edit the HTML file:
code index.html

Create a ZIP package:
zip -r stagingcode.zip .

Deploy to the staging slot:
az webapp deploy -g $resourceGroup -n $appName --src-path ./stagingcode.zip --slot staging

Swap Staging ↔ Production
In Azure Portal:

Go to Deployment Slots

Click Swap

Select Source = staging

Select Target = production

Click Start Swap

Verify Deployment
Open the production URL

Refresh to confirm updated content is live

Clean Up Resources:
az group delete -n $resourceGroup

Learning Outcomes
You will learn:

How to deploy apps using Azure App Service

How deployment slots work

How to perform blue–green deployments

How to swap environments with zero downtime

How to use Azure CLI effectively


## 📸 Screenshots

### 1️⃣ Deployment Overview
images/Screenshot%202026-01-07%20135456.png

### 2️⃣ Azure Portal – Staging Slot
![Staging Slot](images/Screenshot%202026-01-07%20135516.png)

### 3️⃣ Code Deployment to Staging
![Deploy to Staging](images/Screenshot%202026-01-07%20135540.png)

### 4️⃣ Slot Swap Confirmation
![Slot Swap](images/Screenshot%202026-01-07%20135623.png)




