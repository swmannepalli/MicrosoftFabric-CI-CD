# Module 1: Environment Setup - Getting Started

## 🎯 Module Objectives

By the end of this module, you will have:
- ✅ Installed all required tools (Git, Python)
- ✅ Set up fabric-cli and fabric-cicd packages
- ✅ Connected to Microsoft Fabric portal
- ✅ Cloned the workshop repository
  
## 📝 Exercise 1: Install Git

> **Goal:** Install Git version control system on your machine.
>
> Git is your version control system - essential for tracking changes and collaborating on code.

Git is essential for version control and CI/CD workflows.

### Windows 

1. Open Command Line Interface and run below command to install git,
   
   ```powershell
   winget install --id Git.Git -e --source winget
   ```
2. Verify installation:
   ```bash
   git --version
   ```
> [!TIP]
> If you already have Git installed, ensure it's version 2.25 or later for optimal compatibility with Microsoft Fabric git integration.

## 📝 Exercise 2: Access Microsoft Fabric Portal

> **Goal:** Log into Microsoft Fabric with workshop credentials.


### Navigate to Microsoft Fabric
Visit the Microsoft Fabric website at [https://fabric.microsoft.com/](https://fabric.microsoft.com/).

### Enter Your Password and Sign In
Input your password in the designated field and click the `Sign In` button.

## 📝 Exercise 3: Get the Workshop Code

> **Goal:** Clone the workshop repository to your local machine.
>
> You'll work with a pre-built solution that demonstrates best practices for Fabric CI/CD.
>
> You'll use this solution only once to deploy the solution to the workspace.

### Set Up GitHub Account
1. **If you don't have a GitHub account:**
   - Visit [github.com](https://github.com)
   - Click "Sign up" and create a free account
   - Verify your email address

2. **If you have an existing GitHub account:**
   - Sign in at [github.com](https://github.com)

### 📦 Clone the Workshop Repository

1. **Open the workshop repository:**
   
   🔗 [https://github.com/swmannepalli/MicrosoftFabric-CICD](https://github.com/swmannepalli/MicrosoftFabric-CICD)

2. **Copy it to your machine:**
   
   **Using Git Command Line (Recommended)**
   ```bash
   # Navigate to your desired directory
   cd ~/Documents  # or your preferred location
   
   # Clone the repository
   git clone https://github.com/swmannepalli/MicrosoftFabric-CICD
   
   # Navigate into the cloned directory
    cd MicrosoftFabric-CICD
   ```

**[→ Click here to start Module 2: First Deployment](../deployment/module2.md)**
